<script>
	import { fade } from "svelte/transition";
	import "../app.css";

	import Github from "@iconify-svelte/simple-icons/github";
	import { onMount } from "svelte";

	const projects = [
		{
			name: "Multithreaded Encrypted File Server/Client",
			description: "A terminal-based file storage server and client",
			link: "https://github.com/Francois-Coleongco/MEFSC",
			demo: "/assets/MEFSC.mp4",
		},
		{
			name: "Speech-Driven AI Video Preprocessor",
			description:
				"An AI-powered video preprocessing for the lazy video editor",
			link: "https://github.com/Francois-Coleongco/KeepItRolling",
			demo: "/assets/KeepItRolling.mp4",
		},
		{
			name: "HTTP Load Balancer",
			description: "A Round-Robin HTTP load balancer",
			link: "https://github.com/Francois-Coleongco/LoadBalancer",
			demo: "/assets/LoadBalancer.mp4",
		},
		{
			name: "Encrypted Steganography Suite",
			description: "A GUI tool to encode encrypted messages in PNG files",
			link: "https://github.com/Francois-Coleongco/Steganography_Suite",
			demo: "/assets/SteganographySuite.mp4",
		},
		{
			name: "DNS Data Exfiltration Detector",
			description:
				"A Machine Learning Model to detect threat-actor communication over the DNS protocol",
			link: "https://github.com/Francois-Coleongco/DNS_Tunneling",
			demo: "/assets/DNS_Tunneling.mp4",
		},
		// {
		// 	name: "Distributed Threat Detection System",
		// 	description: "A distributed threat detection framework",
		// 	link: "https://github.com/Francois-Coleongco/SATD",
		// },
		{
			name: "Network Encryption Interface",
			description: "A C++ systems programming & encryption interface",
			link: "https://github.com/Francois-Coleongco/Network-Encryption-Interface",
			demo: "/assets/NetworkEncInterface.mp4",
		},
	];

	let menuOpen = false;

	const toggleHamburger = () => {
		menuOpen = !menuOpen;
	};

	let videos = [];

	onMount(() => {
		const observer = new IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				const video = entry.target;
				if (entry.isIntersecting) {
					video.play();
				} else {
					video.pause();
					console.log("paused");
				}
			});
		});

		videos.forEach((video) => {
			if (video) observer.observe(video);
		});
	});

	let scrollY = 0;
	// Track scroll
	function handleScroll() {
		scrollY = window.scrollY;
		document.body.style.backgroundPosition = `center ${scrollY * -0.05}px`;
	}
</script>

<svelte:window on:scroll={handleScroll} />;

<div class="min-h-screen bg-bg text-gray-200 font-mono">
	<nav
		class="flex justify-between items-center px-6 py-4 border-b border-border"
	>
		<a href="/" class="text-cyan-400 text-xl tracking-widest"
			>Francois Coleongco</a
		>
		<div class="hidden md:flex space-x-6">
			<a href="#projects" class="text-cyan-400 transition">Projects</a>
			<a href="#contact" class="text-cyan-400 transition">Contact</a>
		</div>
		<div class="md:hidden">
			<button id="menu-btn" on:click={toggleHamburger}>
				<svg
					class="w-6 h-6 text-accent"
					fill="none"
					stroke="currentColor"
					stroke-width="2"
					viewBox="0 0 24 24"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M4 6h16M4 12h16M4 18h16"
					></path>
				</svg>
			</button>
		</div>
	</nav>
	{#if menuOpen}
		<div
			class="md:hidden flex flex-col items-end mt-2 px-6 font-mono text-right"
		>
			<div
				class="w-40 backdrop-blur-sm bg-panel/80 border border-border rounded-md shadow-lg flex flex-col divide-y divide-white/40"
			>
				<a
					href="#projects"
					class="py-2 px-3 hover:text-accent transition">Projects</a
				>
				<a
					href="#contact"
					class="py-2 px-3 hover:text-accent transition">Contact</a
				>
			</div>
		</div>
	{/if}
	<main class="p-6">
		<h2
			class="text-cyan-400 font-mono text-center text-lg md:text-2xl mb-4 whitespace-pre-wrap break-words"
		>
			77 65 27 72 65 20 61 6c 6c 20 76 6f 69 64 20 70 6f 69 6e 74 65 72 73
		</h2>
		<p class="text-gray-200 text-center max-w-2xl mx-auto mb-12">
			Hi, I'm Francois, an Honors CS major @ the University of Alberta
			focused on building secure, efficient, and reliable tools and
			applications.
		</p>

		<section
			id="projects"
			class="min-h-screen flex flex-col justify-center items-center text-center px-4 py-16 md:py-24"
		>
			<h2 class="pipboy-flicker text-cyan-400 text-4xl mb-8">Projects</h2>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-6 w-full max-w-6xl">
				{#each projects as project, i (project.name)}
					<div
						class="project-panel bg-[#1C1C33] backdrop-blur-lg opacity-90 border border-[#222244] rounded-lg shadow-lg p-6 flex flex-col justify-between transform transition-transform duration-200 hover:-translate-y-1 hover:shadow-[0_12px_25px_rgba(0,255,255,0.2)]
               {i % 2 === 0 ? 'hover-left' : 'hover-right'}"
					>
						<a href={project.link} target="_blank" class="block">
							<h3
								class="text-cyan-400 text-xl font-mono mb-2 leading-snug"
							>
								{project.name}
							</h3>
							<p
								class="text-gray-200 text-sm leading-relaxed mb-4"
							>
								{project.description}
							</p>
							{#if project.demo}
								<div
									class="video-wrapper w-full aspect-video overflow-hidden rounded-md border border-[#222244] shadow-lg"
								>
									<video
										bind:this={videos[i]}
										src={project.demo}
										autoplay
										muted
										loop
										class="w-full h-full object-cover rounded-md"
									/>
								</div>
							{/if}
						</a>
						<div class="flex items-center space-x-2 mt-4">
							<a href={project.link}>
								<Github
									height="24"
									class="text-gray-200 block -translate-y-2 hover:text-cyan-400 animate-pulse transition-all duration-1000 drop-shadow-[0_0_5px_rgba(0,255,255,0.5)] hover:drop-shadow-[0_0_10px_rgba(0,255,255,0.9)] cursor-pointer mt-4"
								/>
							</a>

							<a
								href={project.link}
								class="text-gray-200 hover:text-cyan-400 truncate max-w-full"
							>
								{project.link.slice(19)}
							</a>
						</div>
					</div>
				{/each}
			</div>
		</section>

		<section id="contact" class="mt-16 text-center">
			<h2 class="text-4xl text-cyan-400 mb-6">CONTACT</h2>
			<div class="flex flex-col md:flex-row justify-center gap-4">
				<a
					href="mailto:francois.coleongco@gmail.com"
					class="bg-panel border border-border rounded-lg px-6 py-3 hover:shadow-lg hover:translate-y-[-2px] transition-all text-cyan-400"
					>Email Me</a
				>
				<a
					href="https://linkedin.com/in/francois-coleongco"
					target="_blank"
					class="bg-panel border border-border rounded-lg px-6 py-3 hover:shadow-lg hover:translate-y-[-2px] transition-all text-cyan-400"
					>LinkedIn</a
				>
			</div>
		</section>
	</main>

	<footer class="mt-16 border-t border-border py-6 text-center text-gray-200">
		© 2025 Francois Coleongco
	</footer>
</div>
