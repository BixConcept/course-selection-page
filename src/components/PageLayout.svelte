<script lang="ts">
	import Logo from '../assets/logo.svg';
	import { fade } from 'svelte/transition';
</script>

<main
	class="flex flex-col items-center w-screen min-h-screen bg-zinc-100 px-8 gap-4"
	transition:fade
>
	<a class="block text-center mt-4" href="/">
		<div class="flex items-center gap-2">
			<div class="w-8 h-8 text-gray-600">
				<img src={Logo} alt="Gymhaan Logo" />
			</div>
			<h1 class="uppercase text-gray-600 ">Gymnasium Haan</h1>
		</div>
	</a>
	<div
		class="p-12 w-[min(800px,90vw)] drop-shadow-2xl bg-white flex items-center justify-center flex-col rounded-2xl my-auto"
	>
		<slot />
		<a
			href="https://github.com/BixConcept/course-selection-page"
			class="mt-16 text-gray-500 font-light">© Nia Schlegel 2023, AGPLv3</a
		>
	</div>
</main>
