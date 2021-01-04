<script>
	import { beforeUpdate } from 'svelte';
	import * as data from './data.json';
	import axios from "axios";
	import GithubList from './GithubList.svelte';

	beforeUpdate(async () => {
		selectNewGod();
	})

	const values = data.values;
	const count = values.length;

	export let name;
	let pantheon;
	let info;
	let url
	let alternatives;


	function selectNewGod() {
		const randomIndex = Math.floor(Math.random() * count);
		const selectedGod = values[randomIndex];
		name = selectedGod.name;
		pantheon = selectedGod.pantheon;
		info = selectedGod.title;
		url = selectedGod.url;
		alternatives = selectedGod.alternatives;
	}

	async function handleNextClick() {
		selectNewGod();
	}
</script>

<main>
	<h1>newprojectname.dev</h1> 
	<h5>The project is named after</h5> <h1>{name}</h1>
	<h3>{pantheon}</h3>
	<h3>{info}</h3>
	<h3>{url}</h3>
	<h3>{alternatives}</h3>
	<button on:click={handleNextClick}>Next god</button>

	<GithubList query={name}/>

</main>