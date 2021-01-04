<script>
    import { afterUpdate } from 'svelte';
    import axios from "axios";

	export const github_api = axios.create({
		baseURL: "https://api.github.com/search/"
	})

	export const searchResultsCount = 5;
    export let query;
    
    let githubSearchPromise = Promise.resolve([]);

    afterUpdate(() => {
        if (query != NaN) {
            githubSearchPromise = getGithubData();
        }
    })
    
	async function getGithubData() {
        console.log("query is:", query)
        const githubSearchResponse = await github_api.get('repositories?q=' + query + '&sort=stars&order=desc')
        console.log(githubSearchResponse.status)
        if (githubSearchResponse.status != '200') {
            throw new Error(githubSearchResponse.statusText);
        }
        else {
            console.log(githubSearchResponse)
            let githubData = githubSearchResponse.data.items; 
            let topGithubResults = []
            for (let i = 0; i < Math.min(githubData.length, searchResultsCount); i++) {
                const rawObject = githubData[i];
                console.log(rawObject.fullname)
                topGithubResults.push({
                    'name' : rawObject['full_name'],
                    'stars': rawObject['stargazers_count'],
                })
            }
            return topGithubResults;
        }
	}
</script>

<div class="github_results">
    {#await githubSearchPromise}
        <p>...waiting for {query}</p>
    {:then repos}
        <ul>
            {#each repos as repo}
                <li>
                    {repo['name']} : {repo['stars']}
                </li>
            {/each}
        </ul>
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}
</div>