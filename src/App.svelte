<script>
  import { beforeUpdate } from "svelte";

  import * as data from "./data.json";
  import ReposList from "./ReposList.svelte";

  const values = data.values;

  let name;
  let pantheon;
  let info;
  let url;
  let alternatives;

  function selectNewGod() {
    const selectedGod = values[Math.floor(Math.random() * values.length)];
    name = selectedGod.name;
    pantheon = selectedGod.pantheon;
    info = selectedGod.title;
    url = selectedGod.url;
    alternatives = selectedGod.alternatives;
  }

  beforeUpdate(async () => {
    selectNewGod();
  });

  async function handleNextClick() {
    selectNewGod();
  }
</script>

<style>
  :root {
    --border-size: 0.125rem;
    --font-family: monospace;
    --color-primary: white;
    --color-secondary: black;
    --shadow: rgba(0, 0, 0, 0.1);
    --space: 1rem;
  }
  footer {
    bottom: 40px;
  }
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .god-info-text {
    font-size: 2em;
  }
  .next-button {
    width: 300px;
    box-shadow: var(--shadow) 4px 4px;
    margin-bottom: 25px;
    cursor: pointer;
    position: relative;
    padding: calc(var(--space) / 1.125) var(--space) var(--space);
    border: var(--border-size) solid black;
    color: var(--color-secondary);
    background-color: var(--color-primary);
    font-size: 1.5em;
    font-family: var(--font-family);
    text-transform: lowercase;
    text-shadow: var(--shadow) 2px 2px;
  }
  .next-button:hover {
    flex-grow: 2;
    color: white;
    outline: none;
    text-shadow: none;
    background-color: var(--color-secondary);
  }
  .project-header {
    margin-bottom: 150px;
  }
  .project-title {
    font-family: "Staatliches";
    font-size: 2em;
  }
  .god-pantheon {
    color: rgb(173, 173, 173);
  }
  .container {
    width: 50%;
    display: flex;
    flex-direction: column;
  }
  .god-info {
    margin-bottom: 50px;
    align-items: flex-start;
    flex: 1 0 auto;
  }
  .god-name {
    font-family: "Staatliches";
    font-size: 9em;
  }
  .god-name-alternatives {
    font-family: "Staatliches";
    font-size: 2em;
  }
  .info {
    min-height: calc(100vh - 60px);
  }
  @media (max-width: 1280px) {
    .container {
      width: 90%;
    }
    .god-name {
      font-size: 3em;
    }
    .project-header {
      margin-bottom: 50px;
    }
    .next-button {
      width: 200px;
    }
    .god-info-text {
      font-size: 1em;
    }
  }
</style>

<main>
  <div class="container">
    <div class="info">
      <p class="project-header">
        <span class="project-title">newprojectname.dev</span>
        <br />
        <span>Your next project/library name inspired by mythology</span>
      </p>

      <div class="god-info">
        <span class="god-pantheon">{pantheon}</span>
        <div>
          <span class="god-name">{name}</span>
          {#if alternatives !== 'nan'}
            <span class="god-name-alternatives">{alternatives}</span>
          {/if}
        </div>
        <span class="god-info-text">
          {info}
          <br />
          <a href={url} target="_blank">Read more</a>
        </span>
      </div>

      <button class="next-button" on:click={handleNextClick}>
        meh, go next
      </button>

      <ReposList query={name} />
    </div>

    <footer>
      Made with ❤️ by
      <a href="https://github.com/repushko">Anton Repushko</a>
      , 2021
      <br />
      All data are based on
      <a href="https://godchecker.com">godchecker.com</a>
    </footer>
  </div>
</main>
