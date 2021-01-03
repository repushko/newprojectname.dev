<script>
	import * as data from './data.json';
	import axios from "axios";

	export const github_api = axios.create({
		baseURL: "https://api.github.com/search/"
	})

	export const values = data.values;
	export const count = values.length;
	export let github_data;
	export let randomNumber = newRandomIndex();

	function newRandomIndex() {
		return Math.floor(Math.random() * count);
	}

	async function handleNextClick() {
		randomNumber = newRandomIndex();
		await getGithubData();
	}

	async function getGithubData() {
		const githubSearchResponse = await github_api.get('repositories?q=' + values[randomNumber].name + '&sort=stars&order=desc')
		github_data  = githubSearchResponse.data.items; 
		
		console.log(github_data)
	}


</script>

<main>
	<h1>Hello count is {count}!</h1> 
	<h2>Random number is: {randomNumber}</h2>
	<h2>Random name is: {values[randomNumber].name}</h2>
	<button on:click={handleNextClick}>Next god</button>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>