<script>
  import { beforeUpdate } from "svelte";
  import * as data from "./data.json";
  import axios from "axios";
  import ReposList from "./ReposList.svelte";

  beforeUpdate(async () => {
    selectNewGod();
  });

  const values = data.values;
  const count = values.length;

  export let name;
  let pantheon;
  let info;
  let url;
  let alternatives;

  function selectNewGod() {
    const selectedGod = values[Math.floor(Math.random() * count)];
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

<style>
  :root {
    --border-size: 0.125rem;
    --duration: 250ms;
    --ease: cubic-bezier(0.215, 0.61, 0.355, 1);
    --font-family: monospace;
    --color-primary: white;
    --color-secondary: black;
    --color-tertiary: dodgerblue;
    --shadow: rgba(0, 0, 0, 0.1);
    --space: 1rem;
  }
  .multi-button {
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
    transition: flex-grow var(--duration) var(--ease);
  }
  .multi-button:hover {
    flex-grow: 2;
    color: white;
    outline: none;
    text-shadow: none;
    background-color: var(--color-secondary);
  }

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .header {
    margin-bottom: 150px;
  }

  .pantheon {
    font-size: 16px;
    color: rgb(173, 173, 173);
  }

  .title {
    font-family: "Staatliches";
    font-size: 32px;
  }

  .container {
	width: 50%;
    display: flex;
    flex-direction: column;
  }

  @media (max-width: 1280px) {
    .container {
      width: 90%;
    }
  }

  .god_info {
    margin-bottom: 50px;
    align-items: flex-start;
    flex: 1 0 auto;
  }
  .description {
    font-size: 32px;
  }

  .name {
    font-family: "Staatliches";
    font-size: 150px;
  }

  .alternatives {
    font-family: "Staatliches";
    font-size: 32px;
  }

</style>

<main>
  <div class="container">

    <p class="header">
      <span class="title">newprojectname.dev</span>
      <br />
      <span class="subtitle">
        Your next project/library name inspired by mythology
      </span>
      <br />
    </p>

    <div class="god_info">
      <span class="pantheon">{pantheon}</span>
      <div class="name_section">
        <span class="name">{name}</span>
        {#if alternatives !== 'nan'}
          <span class="alternatives">{alternatives}</span>
        {/if}
      </div>
      <span class="description">
        {info}
        <br />
        <a href={url} target="_blank">Read more</a>
      </span>
    </div>

    <button class="multi-button" on:click={handleNextClick}>
      meh, go next
    </button>

    <ReposList query={name} />

    <!---<footer>
      Made with ❤️ by
      <a href="https://github.com/repushko">Anton Repushko</a>
      , 2021. All data are based on
      <a href="https://godchecker.com">godchecker.com</a>
    </footer>-->
  </div>
</main>
