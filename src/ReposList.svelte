<script>
  import { afterUpdate } from "svelte";
  import axios from "axios";
  import Repo from "./Repo.svelte";

  export const github_api = axios.create({
    baseURL: "https://api.github.com/search/"
  });

  export const searchResultsCount = 5;
  export let query;

  let githubSearchPromise = Promise.resolve([]);

  afterUpdate(() => {
    if (query != NaN) {
      githubSearchPromise = getGithubData();
    }
  });

  async function getGithubData() {
    const githubSearchResponse = await github_api
      .get("repositories?q=" + query + "&sort=stars&order=desc")
      .catch(error => {
        if (error.response.status == "403") {
          throw new Error(
            "There are to many requests to Github. \n Just relax for a second and continue :)"
          );
        } else {
          throw new Error("We got a strange error from Github :(");
        }
      });
    let githubData = githubSearchResponse.data.items;
    let topGithubResults = [];
    for (let i = 0; i < Math.min(githubData.length, searchResultsCount); i++) {
      const rawObject = githubData[i];
      if (rawObject["size"] > 0) {
        topGithubResults.push({
          name: rawObject["full_name"],
          starsCount: rawObject["stargazers_count"],
          description: rawObject["description"],
          lastUpdate: rawObject["updatet_at"],
          repoUrl: rawObject["html_url"],
          language: rawObject["language"],
          license: rawObject["license"]
        });
      }
    }
    return topGithubResults;
  }
</script>

<style>
  .repos-list {
    padding: 0;
    list-style-type: none;
  }

  .search-status {
    font-size: 2em;
  }

  .search-error {
    color: #fa8072;
  }

  @media (max-width: 1280px) {
    .search-status {
      font-size: 1em;
    }
  }
</style>

<div class="github_results">
  {#await githubSearchPromise}
    <p class="search-status">...searching on Github</p>
  {:then repos}
    {#if repos.length > 0}
      <p class="search-status">These are the top search results from Github:</p>
      <ul class="repos-list">
        {#each repos as repo}
          <li>
            <Repo
              repoFullName={repo['name']}
              repoUrl={repo['repoUrl']}
              language={repo['language']}
              licence={repo['license']}
              lastUpdate={repo['lastUpdate']}
              description={repo['description']}
              starsCount={repo['starsCount']} />
          </li>
        {/each}
      </ul>
    {/if}
    {#if repos.length == 0}
      <p class="search-title">
        A search on GitHub turned up nothing
        <nobr>( ͡° ͜ʖ ͡°)</nobr>
      </p>
    {/if}
  {:catch error}
    <p class="search-status search-error">{error.message}</p>
  {/await}
</div>
