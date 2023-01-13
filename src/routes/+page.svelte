<script lang="ts">
	import { goto } from '$app/navigation';
	import Logo from '../assets/logo.svg';
	import { fade } from 'svelte/transition';
	import PageLayout from '../components/PageLayout.svelte';

	const choices = [
		{ id: 0, href: '/sixth-grade', title: 'Sechste Klasse', large: '6', active: true },
		{ id: 1, href: '/ninth-grade', title: 'Neunte Klasse', large: '9', active: true },
		{ id: 2, title: 'Oberstufe', large: 'S2', active: false, href: null }
	];

	let selected: number | null = null;

	function selectThing(choice: number) {
		const filtered = choices.filter((x) => x.id == choice && x.active);
		if (filtered && filtered[0].active) {
			selected = choice;
			goto(filtered[0].href as string);
		}
	}
</script>

<svelte:head>
	<title>Kurswahlen Gymhaan</title>
</svelte:head>

<PageLayout>
	<h1 class="text-center text-4xl text-indigo-600">Kurswahlen</h1>
	<h2 class="text-center text-gray-500">Städtisches Gymnasium Haan</h2>
	<div class="flex flex-col sm:flex-row gap-4 mt-12 w-full">
		{#each choices as choice}
			<button
				class="flex-1 w-full sm:w-auto shadow-lg rounded-md flex flex-col justify-center items-center p-8 h-[250px] ring-indigo-600 active:ring-2 transition-all ease-in-out"
				disabled={!choice.active}
				on:click={() => selectThing(choice.id)}
			>
				<h2
					class="flex-1 text-7xl font-bold "
					class:text-indigo-600={choice.active}
					class:text-gray-600={!choice.active}
				>
					{choice.large}
				</h2>
				<h3
					class="mt-12 text-center text-lg"
					class:text-indigo-600={choice.active}
					class:text-gray-600={!choice.active}
				>
					{choice.title}
				</h3>
			</button>
		{/each}
	</div>
</PageLayout>
