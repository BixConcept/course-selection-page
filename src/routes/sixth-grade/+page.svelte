<script lang="ts">
	import { goto } from '$app/navigation';
	import Logo from '../../assets/logo.svg';

	const choices = [
		{ id: 0, title: 'Latein', large: '📜', active: true },
		{ id: 1, title: 'Französisch', large: '🇫🇷', active: true }
		/* { id: 2, title: 'Oberstufe', large: 'S2', active: false } */
	];

	$: idError = id !== null && id < 1000;
	$: birthDateError = birthDate !== null && new Date().getTime() < new Date(birthDate).getTime();

	let id: null | number = null;
	let birthDate: null | any = null;

	let selected: number | null = null;

	function selectThing(choice: number) {
		const filtered = choices.filter((x) => x.id == choice);
		if (filtered && filtered[0].active) {
			selected = choice;
		}
	}

	$: submitEnabled = id && birthDate && !(idError || birthDateError);

	function submit() {
		if (!submitEnabled) return;
		alert('TODO');
	}

	$: console.log(new Date(birthDate));
</script>

<main class="flex flex-col justify-center items-center w-screen h-screen bg-zinc-100 px-8">
	<div class="flex absolute top-4 items-center gap-2">
		<div class="w-8 h-8 text-gray-600">
			<img src={Logo} alt="Gymhaan Logo" />
		</div>
		<h1 class="uppercase text-gray-600 ">Gymnasium Haan</h1>
	</div>
	<div
		class="p-12 w-[min(800px,90vw)] drop-shadow-2xl bg-white flex items-center justify-center flex-col rounded-2xl "
	>
		<h1 class="text-center text-4xl text-indigo-600">Kurswahlen 6. Klasse</h1>
		<h2 class="text-center text-gray-500">Städtisches Gymnasium Haan</h2>
		<form
			on:submit={(e) => {
				e.preventDefault();
			}}
			class="flex gap-4 w-full mt-8"
		>
			<div class="flex flex-col flex-1 gap-1">
				<label class="text-gray-500 text-sm" class:text-red-400={idError} for="id">Schüler-ID</label
				>
				<input
					bind:value={id}
					class="border-gray-200 border-4 rounded-lg px-2 text-gray-500"
					class:ring-red-400={idError}
					class:ring-4={idError}
					name="id"
					type="number"
					placeholder="1235"
				/>
			</div>
			<div class="flex flex-col flex-1 gap-1">
				<label class="text-gray-500 text-sm" class:text-red-400={birthDateError} for="id"
					>Geburtsdatum</label
				>
				<input
					bind:value={birthDate}
					class="border-gray-200 border-4 rounded-lg px-2 text-gray-500"
					class:ring-red-400={birthDateError}
					class:ring-4={birthDateError}
					name="id"
					type="date"
				/>
			</div>
		</form>

		<div class="flex flex-col sm:flex-row gap-4 mt-12 w-full">
			{#each choices as choice}
				<button
					class="flex-1 w-full sm:w-auto shadow-lg rounded-md flex flex-col justify-center p-8 h-[250px] ring-indigo-600 active:ring-2 transition-all ease-in-out"
					disabled={!choice.active}
					class:ring-4={selected == choice.id}
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
		<button
			class="mt-8 enabled:bg-indigo-500 bg-gray-400 text-gray-100 px-8 py-2 font-bold uppercase rounded-md"
			disabled={!submitEnabled}
			on:click={submit}>Abschicken</button
		>
		<p class="mt-16 text-gray-500 font-light">© Nia Schlegel 2023, AGPLv3</p>
	</div>
</main>
