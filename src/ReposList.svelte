<script>
    import { afterUpdate } from 'svelte';
    import axios from "axios";
    import Repo from "./Repo.svelte";

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
        const githubSearchResponse = await github_api.get('repositories?q=' + query + '&sort=stars&order=desc')
        if (githubSearchResponse.status != '200') {
            throw new Error(githubSearchResponse.statusText);
        }
        else {
            let githubData = githubSearchResponse.data.items; 
            let topGithubResults = []
            for (let i = 0; i < Math.min(githubData.length, searchResultsCount); i++) {
                const rawObject = githubData[i];
                topGithubResults.push({
                    'name' : rawObject['full_name'],
                    'starsCount': rawObject['stargazers_count'],
                    'description': rawObject['description'],
                    'lastUpdate': rawObject['updatet_at'],
                    'repoUrl': rawObject['html_url'],
                    'language': rawObject['language'],
                    'license': rawObject['license'],
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
        <ul class="repos_list">
            {#each repos as repo}
                <li>
                    <Repo 
                        repoFullName={repo['name']} 
                        repoUrl={repo['repoUrl']} 
                        language={repo['language']} 
                        licence={repo['license']} 
                        lastUpdate={repo['lastUpdate']} 
                        description={repo['description']}
                        starsCount={repo['starsCount']}
                    />
                </li>
            {/each}
        </ul>
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}
</div>

<style>
    .repos_list {
        padding: 0;
        list-style-type: none;
    }

</style>