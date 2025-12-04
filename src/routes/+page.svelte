<script>
	import { fade } from "svelte/transition";
	import "../app.css";

	import Github from "@iconify-svelte/simple-icons/github";
	import { onMount } from "svelte";

	const projects = [
		{
			name: "Server Agent Threat Detection (SATD)",
			description:
				"Distributed threat detection with Go agents and dashboard.",
			link: "https://github.com/Francois-Coleongco/SATD",
			demo: "/assets/SATD.mp4",
		},
		{
			name: "Multithreaded Encrypted File Server/Client",
			description: "Threaded file storage server & client.",
			link: "https://github.com/Francois-Coleongco/MEFSC",
			demo: "/assets/MEFSC.mp4",
		},
		{
			name: "Speech-Driven AI Video Preprocessor",
			description: "AI-assisted cutting & preprocessing.",
			link: "https://github.com/Francois-Coleongco/KeepItRolling",
			demo: "/assets/KeepItRolling.mp4",
		},
		{
			name: "HTTP Load Balancer",
			description: "Simple RR load balancer.",
			link: "https://github.com/Francois-Coleongco/LoadBalancer",
			demo: "/assets/LoadBalancer.mp4",
		},
		{
			name: "Encrypted Steganography Suite",
			description: "GUI tool to hide encrypted messages.",
			link: "https://github.com/Francois-Coleongco/Steganography_Suite",
			demo: "/assets/SteganographySuite.mp4",
		},
		{
			name: "DNS Data Exfiltration Detector",
			description: "ML model to detect DNS tunneling.",
			link: "https://github.com/Francois-Coleongco/DNS_Tunneling",
			demo: "/assets/DNS_Tunneling.mp4",
		},
		{
			name: "Network Encryption Interface",
			description: "C++ systems programming encryption interface.",
			link: "https://github.com/Francois-Coleongco/Network-Encryption-Interface",
			demo: "/assets/NetworkEncInterface.mp4",
		},
	];

	let videos = [];

	onMount(() => {
		const obs = new IntersectionObserver((entries) => {
			entries.forEach((e) => {
				const v = e.target;
				if (e.isIntersecting) v.play();
				else v.pause();
			});
		});

		videos.forEach((v) => v && obs.observe(v));
	});
</script>

<!-- NAVBAR -->
<nav
	class="w-full border-b border-neutral-800 bg-neutral-950/60 backdrop-blur-sm"
>
	<div class="max-w-6xl mx-auto px-6 py-4 flex justify-between items-center">
		<a class="text-cyan-400 font-semibold text-lg" href="/"
			>Francois Coleongco</a
		>

		<div class="hidden md:flex gap-6 text-sm">
			<a href="#projects" class="text-cyan-400 hover:text-cyan-300"
				>Projects</a
			>
			<a href="#contact" class="text-cyan-400 hover:text-cyan-300"
				>Contact</a
			>
		</div>
	</div>
</nav>

<!-- HERO -->
<section class="max-w-3xl mx-auto px-6 py-16 text-center">
	<h1 class="text-3xl font-medium text-white mb-4">Hello, I'm Francois :)</h1>
	<p class="text-neutral-300">
		Honors CS major @ University of Alberta focused on building secure,
		efficient, and reliable systems.
	</p>
</section>

<!-- PROJECTS -->
<section id="projects" class="max-w-6xl mx-auto px-6 py-12">
	<h2 class="text-center text-3xl font-medium text-cyan-400 mb-12">
		Projects
	</h2>

	<div class="grid gap-8 sm:grid-cols-2 lg:grid-cols-3">
		{#each projects as p, i}
			<div
				class="bg-neutral-900 border border-neutral-800 rounded-xl p-5 shadow-sm hover:shadow-lg hover:border-cyan-400/50 transition duration-200"
			>
				<a href={p.link} target="_blank">
					<h3 class="text-lg font-semibold text-white mb-2">
						{p.name}
					</h3>
					<p class="text-neutral-400 text-sm mb-4">{p.description}</p>

					{#if p.demo}
						<video
							bind:this={videos[i]}
							src={p.demo}
							muted
							loop
							playsinline
							class="rounded-md w-full border border-neutral-800"
						/>
					{/if}
				</a>

				<div class="flex items-center gap-2 mt-4 text-sm">
					<a href={p.link} target="_blank">
						<Github
							class="text-neutral-300 hover:text-cyan-400"
							height="22"
						/>
					</a>
					<a
						href={p.link}
						target="_blank"
						class="text-neutral-300 hover:text-cyan-400 truncate"
					>
						{p.link.slice(19)}
					</a>
				</div>
			</div>
		{/each}
	</div>
</section>

<!-- CONTACT -->
<section id="contact" class="max-w-3xl mx-auto px-6 py-16 text-center">
	<h2 class="text-3xl text-cyan-400 font-medium mb-6">Contact</h2>

	<div class="flex flex-col sm:flex-row justify-center gap-4">
		<a
			href="mailto:francois.coleongco@gmail.com"
			class="px-6 py-3 rounded-lg border border-neutral-800 bg-neutral-900 text-cyan-400 hover:border-cyan-400 transition"
		>
			Email Me
		</a>
		<a
			href="https://linkedin.com/in/francois-coleongco"
			target="_blank"
			class="px-6 py-3 rounded-lg border border-neutral-800 bg-neutral-900 text-cyan-400 hover:border-cyan-400 transition"
		>
			LinkedIn
		</a>
	</div>
</section>

<!-- FOOTER -->
<footer class="py-6 text-center text-neutral-500 border-t border-neutral-800">
	© 2025 Francois Coleongco
</footer>
