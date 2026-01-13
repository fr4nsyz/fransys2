<script>
	import "../app.css";
	import Github from "@iconify-svelte/simple-icons/github";
	import { onMount } from "svelte";

	const experiences = [
		{
			title: "Software Engineer Intern",
			place: "IBM",
			when: "Jan 2026 — Present",
			description: "",
		},
		{
			title: "AI Engineer",
			place: "Undergraduate Artificial Intelligence Society",
			when: "Oct 2025 — Jan 2026",
			description: "",
		},
		{
			title: "Full Stack Developer",
			place: "UofA Blueprint Chapter",
			when: "Oct 2025 — Jan 2026",
			description: "",
		},
	];

	const projects = [
		{
			name: "SATD",
			description:
				"Distributed threat detection with agents + analysis server",
			link: "https://github.com/fr4nsyz/SATD",
			demo: "/assets/SATD.mp4",
		},
		{
			name: "MEFSC",
			description: "Multithreaded encrypted file server and client",
			link: "https://github.com/fr4nsyz/MEFSC",
			demo: "/assets/MEFSC.mp4",
		},
		{
			name: "Keep It Rolling",
			description: "Speech-driven AI video preprocessing pipeline",
			link: "https://github.com/fr4nsyz/KeepItRolling",
			demo: "/assets/KeepItRolling.mp4",
		},
		{
			name: "Load Balancer",
			description: "Round-robin HTTP load balancer",
			link: "https://github.com/fr4nsyz/LoadBalancer",
			demo: "/assets/LoadBalancer.mp4",
		},
		{
			name: "Steganography Suite",
			description: "GUI tool for encrypted steganographic messaging",
			link: "https://github.com/fr4nsyz/Steganography_Suite",
			demo: "/assets/SteganographySuite.mp4",
		},
		{
			name: "DNS Exfiltration Detector",
			description: "ML-based detector for DNS tunneling",
			link: "https://github.com/fr4nsyz/DNS_Tunneling",
			demo: "/assets/DNS_Tunneling.mp4",
		},
		{
			name: "Network Encryption Interface",
			description:
				"C++ systems-level network encryption interface (with libsodium)",
			link: "https://github.com/fr4nsyz/Network-Encryption-Interface",
			demo: "/assets/NetworkEncInterface.mp4",
		},
	];

	let videos = [];
	let waving_hand = "/";

	setInterval(() => {
		waving_hand = waving_hand === "/" ? "l" : "/";
	}, 600);

	onMount(() => {
		const btn = document.getElementById("menu-btn");
		const menu = document.getElementById("mobile-menu");

		btn.addEventListener("click", () => {
			menu.classList.toggle("hidden");
		});
		const canvas = document.getElementById("board");
		const ctx = canvas.getContext("2d");

		const stars = [];
		const STAR_COUNT = 80;

		function spawnStar() {
			const speed = Math.random() * 4;
			const angle = Math.PI * (Math.random() * 0.25 - 0.125);
			return {
				x: Math.random() * canvas.width,
				y: Math.random() * canvas.height,
				vx: Math.cos(angle) * speed,
				vy: Math.sin(angle) * speed,
				life: 10,
			};
		}

		function resize() {
			canvas.width = window.innerWidth;
			canvas.height = window.innerHeight;
		}

		resize();
		window.addEventListener("resize", resize);

		for (let i = 0; i < STAR_COUNT; i++) stars.push(spawnStar());

		function update() {
			const t = performance.now() * 0.001;

			const grd = ctx.createLinearGradient(
				0,
				0,
				canvas.width,
				canvas.height,
			);

			grd.addColorStop(0, `hsl(${180 + Math.sin(t) * 40}, 90%, 10%)`);
			grd.addColorStop(
				1,
				`hsl(${200 + Math.sin(t + Math.PI / 2) * 40}, 90%, 20%)`,
			);

			ctx.fillStyle = grd;
			ctx.fillRect(0, 0, canvas.width, canvas.height);

			ctx.lineWidth = 1.5;
			ctx.shadowBlur = 10;
			ctx.shadowColor = "cyan";

			for (let s of stars) {
				ctx.beginPath();
				ctx.strokeStyle = `rgba(0,255,255,${s.life})`;
				ctx.moveTo(s.x, s.y);
				ctx.lineTo(s.x - s.vx * 6, s.y - s.vy * 6);
				ctx.stroke();

				s.x += s.vx;
				s.y += s.vy;
				s.life -= 0.01;

				if (
					s.life <= 0 ||
					s.x < 0 ||
					s.y < 0 ||
					s.x > canvas.width ||
					s.y > canvas.height
				) {
					Object.assign(s, spawnStar());
				}
			}
		}

		function run() {
			update();
			requestAnimationFrame(run);
		}

		run();

		const obs = new IntersectionObserver((entries) => {
			entries.forEach((e) => {
				const v = e.target;
				e.isIntersecting ? v.play() : v.pause();
			});
		});

		videos.forEach((v) => v && obs.observe(v));
	});
</script>

<canvas id="board" class="fixed inset-0 -z-10"></canvas>

<!-- NAV -->
<nav class="max-w-6xl mx-auto px-6 py-6 text-sm font-mono text-gray-400">
	<div class="flex justify-between items-center">
		<span>francois@local</span>

		<!-- Desktop links -->
		<div class="hidden sm:flex space-x-6">
			<a href="#experience" class="hover:text-cyan-400">experience</a>
			<a href="#projects" class="hover:text-cyan-400">projects</a>
			<a href="#contact" class="hover:text-cyan-400">contact</a>
		</div>

		<!-- Hamburger button -->
		<button
			id="menu-btn"
			class="sm:hidden focus:outline-none"
			aria-label="Toggle menu"
		>
			<svg
				class="w-6 h-6"
				fill="none"
				stroke="currentColor"
				stroke-width="2"
				viewBox="0 0 24 24"
			>
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					d="M4 6h16M4 12h16M4 18h16"
				/>
			</svg>
		</button>
	</div>

	<!-- Mobile menu -->
	<div id="mobile-menu" class="hidden flex-col mt-4 space-y-4 sm:hidden">
		<a href="#experience" class="hover:text-cyan-400">experience</a>
		<a href="#projects" class="hover:text-cyan-400">projects</a>
		<a href="#contact" class="hover:text-cyan-400">contact</a>
	</div>
</nav>

<!-- HERO -->
<section class="max-w-3xl mx-auto px-6 py-24 font-mono text-gray-200">
	<h1 class="text-3xl mb-4">
		hi o{waving_hand}
	</h1>

	<p class="text-gray-400 leading-relaxed">
		swe @ IBM<br />
		honors cs @ university of alberta<br />
		systems programming • cybersecurity
	</p>

	<p class="text-xs text-gray-500 mt-4">
		rust | c/c++ | go | linux | networking
	</p>
</section>

<section class="max-w-3xl mx-auto px-6 py-12 font-mono" id="experience">
	<h2 class="text-sm uppercase tracking-widest text-gray-500 mb-6">
		experience
	</h2>

	{#each experiences as e, i}
		<div class="space-y-6 text-sm">
			<div class="border-l border-gray-700 pl-4">
				<div class="flex justify-between flex-wrap gap-2">
					<span class="text-gray-200">
						{e.title}
					</span>
					<span class="text-gray-500">{e.when}</span>
				</div>

				<p class="text-gray-400 mt-1">{e.place}</p>

				<p>{e.description}</p>
			</div>
		</div>
		<br />
	{/each}
</section>

<!-- PROJECTS -->
<section id="projects" class="max-w-6xl mx-auto px-6 py-16 font-mono">
	<h2 class="text-sm uppercase tracking-widest text-gray-500 mb-8">
		selected builds
	</h2>

	<div class="grid gap-8 sm:grid-cols-2 lg:grid-cols-2">
		{#each projects as p, i}
			<div
				class="bg-black/60 border border-gray-800 rounded-lg p-5
				       hover:border-cyan-400 transition"
			>
				<a href={p.link} target="_blank" class="block">
					<h3 class="text-gray-200 mb-2">{p.name}</h3>
					<p class="text-sm text-gray-400 mb-4">{p.description}</p>

					{#if p.demo}
						<video
							bind:this={videos[i]}
							src={p.demo}
							muted
							loop
							playsinline
							class="rounded border border-gray-800"
						/>
					{/if}
				</a>

				<div class="mt-4 flex items-center gap-2 text-xs text-gray-500">
					<Github height="16" />
					<span class="truncate">{p.link.slice(19)}</span>
				</div>
			</div>
		{/each}
	</div>
</section>

<!-- CONTACT -->
<section id="contact" class="max-w-3xl mx-auto px-6 py-24 font-mono">
	<h2 class="text-sm uppercase tracking-widest text-gray-500 mb-6">
		reach me
	</h2>

	<div class="flex gap-6 text-sm">
		<a
			href="mailto:francois.coleongco@gmail.com"
			class="text-cyan-400 hover:underline"
		>
			email
		</a>

		<a
			href="https://linkedin.com/in/francois-coleongco"
			target="_blank"
			class="text-cyan-400 hover:underline"
		>
			linkedin
		</a>
	</div>
</section>

<footer class="text-center text-xs text-gray-600 py-6 font-mono">
	© 2025
</footer>
