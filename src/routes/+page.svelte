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
			link: "https://github.com/fr4nsyz/SATD",
			demo: "/assets/SATD.mp4",
		},
		{
			name: "Multithreaded Encrypted File Server/Client",
			description: "Threaded file storage server & client.",
			link: "https://github.com/fr4nsyz/MEFSC",
			demo: "/assets/MEFSC.mp4",
		},
		{
			name: "Speech-Driven AI Video Preprocessor",
			description: "AI-assisted cutting & preprocessing.",
			link: "https://github.com/fr4nsyz/KeepItRolling",
			demo: "/assets/KeepItRolling.mp4",
		},
		{
			name: "HTTP Load Balancer",
			description: "Simple RR load balancer.",
			link: "https://github.com/fr4nsyz/LoadBalancer",
			demo: "/assets/LoadBalancer.mp4",
		},
		{
			name: "Encrypted Steganography Suite",
			description: "GUI tool to hide encrypted messages.",
			link: "https://github.com/fr4nsyz/Steganography_Suite",
			demo: "/assets/SteganographySuite.mp4",
		},
		{
			name: "DNS Data Exfiltration Detector",
			description: "ML model to detect DNS tunneling.",
			link: "https://github.com/fr4nsyz/DNS_Tunneling",
			demo: "/assets/DNS_Tunneling.mp4",
		},
		{
			name: "Network Encryption Interface",
			description: "C++ systems programming encryption interface.",
			link: "https://github.com/fr4nsyz/Network-Encryption-Interface",
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

	let waving_hand = "/";

	setInterval(() => {
		if (waving_hand === "/") {
			waving_hand = "l";
		} else {
			waving_hand = "/";
		}
	}, 500);
</script>

<!-- NAVBAR -->
<nav class="bg-black text-white p-4 font-mono">
	<div class="max-w-6xl mx-auto flex justify-between items-center">
		<a href="/" class="text-white font-semibold text-lg"
			>Francois Coleongco</a
		>
		<div>
			<a href="#projects" class="text-white hover:text-gray-300 mr-6"
				>Projects</a
			>
			<a href="#contact" class="text-white hover:text-gray-300">Contact</a
			>
		</div>
	</div>
</nav>

<!-- HERO -->
<section class="max-w-3xl mx-auto p-8 text-center bg-black text-white">
	<h1 class="text-4xl font-semibold">Hi o{waving_hand}</h1>
	<p class="text-gray-300 mt-4">
		I'm a Honors CS major at the University of Alberta, focusing on systems
		programming and cybersecurity.
	</p>
</section>

<!-- PROJECTS -->
<section id="projects" class="max-w-6xl mx-auto p-8 bg-black text-white">
	<h2 class="text-2xl text-center mb-8 font-semibold">Projects</h2>

	<div class="grid gap-8 sm:grid-cols-2 lg:grid-cols-3">
		{#each projects as p, i}
			<div
				class="group bg-gray-900 p-6 rounded-lg shadow-lg transition duration-300 border-2 border-transparent hover:border-indigo-500"
			>
				<a href={p.link} target="_blank" class="block">
					<h3 class="text-xl font-semibold text-white mb-2">
						{p.name}
					</h3>
					<p class="text-gray-400 text-sm mb-4">{p.description}</p>

					{#if p.demo}
						<video
							bind:this={videos[i]}
							src={p.demo}
							muted
							loop
							playsinline
							class="w-full rounded-md border border-gray-700"
						/>
					{/if}
				</a>

				<div class="mt-4 flex items-center gap-2 text-sm text-gray-400">
					<a href={p.link} target="_blank">
						<Github
							height="20"
							class="text-gray-400 hover:text-white"
						/>
					</a>
					<a href={p.link} target="_blank" class="truncate">
						{p.link.slice(19)}
					</a>
				</div>
			</div>
		{/each}
	</div>
</section>

<!-- CONTACT -->
<section
	id="contact"
	class="max-w-3xl mx-auto p-8 text-center bg-black text-white"
>
	<h2 class="text-2xl mb-6 font-semibold">Contact</h2>

	<div class="flex justify-center gap-4">
		<a
			href="mailto:francois.coleongco@gmail.com"
			class="bg-gray-800 text-cyan-400 py-2 px-6 rounded-lg
			   border-2 border-transparent transition-all duration-300
			   hover:border-cyan-400 hover:-translate-y-0.5 hover:shadow-lg"
		>
			Email Me
		</a>

		<a
			href="https://linkedin.com/in/francois-coleongco"
			target="_blank"
			class="bg-gray-800 text-cyan-400 py-2 px-6 rounded-lg
			   border-2 border-transparent transition-all duration-300
			   hover:border-cyan-400 hover:-translate-y-0.5 hover:shadow-lg"
		>
			LinkedIn
		</a>
	</div>
</section>

<!-- FOOTER -->
<footer class="bg-black text-center text-gray-500 py-4">
	© 2025 Francois Coleongco
</footer>
