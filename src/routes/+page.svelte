<script lang="ts">
	const choices = [
		{ id: 0, title: 'Sechste Klasse', large: '6', active: true },
		{ id: 1, title: 'Neunte Klasse', large: '9', active: true },
		{ id: 2, title: 'Oberstufe', large: 'S2', active: false }
	];

	let selected: number | null = null;

	function selectThing(choice: number) {
		const filtered = choices.filter((x) => x.id == choice);
		if (filtered && filtered[0].active) {
			selected = choice;
		}
	}
</script>

<main class="flex flex-col justify-center items-center w-screen h-screen bg-slate-300">
	<div
		class="p-12 drop-shadow-2xl bg-white max-w-screen-lg flex items-center justify-center flex-col w-full rounded-2xl"
	>
		<h1 class="text-center text-4xl text-indigo-600">Kurswahlen</h1>
		<h2 class="text-center text-gray-500">Städtisches Gymnasium Haan</h2>
		<div class="flex gap-4 mt-12">
			{#each choices as choice}
				<button
					class="flex-1 shadow-lg rounded-md flex flex-col  justify-center p-8 w-72 h-[250px] ring-indigo-600"
					on:click={() => selectThing(choice.id)}
					class:ring-2={selected === choice.id}
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
		<p class="mt-16 text-gray-500 font-light">© Nia Schlegel 2023, AGPLv3</p>
	</div>
</main>
