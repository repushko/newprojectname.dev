<script>
  export let repoUrl;
  export let repoFullName;
  export let language;
  export let license;
  export let lastUpdate;
  export let description;
  export let starsCount;
</script>

<style>
  .svg-icon {
    display: inline-flex;
    align-self: center;
  }
  .svg-icon svg {
    height: 2em;
    width: 2em;
  }

  .repo-name {
    font-size: 1.5em;
  }

  @media (max-width: 1280px) {
    .repo-name {
        font-size: 1em;
    }

    .svg-icon svg {
      height: 1.5em;
      width: 1.5em;
  }

  }
  .repo {
    margin-bottom: 3em;
  }
</style>

<div class="repo">
  <div class="svg-icon">
    <svg viewBox="0 0 50 50">
      <path
        style="text-indent:0;text-align:start;line-height:normal;text-transform:none;block-progression:tb;-inkscape-font-specification:Sans"
        d="M 10 2 C 8.3550302 2 7 3.3550302 7 5 L 7 41 C 7 42.64497 8.3550302 44
        10 44 L 13 44 L 13 47 L 13 48.625 L 14.4375 47.90625 L 18 46.125 L
        21.5625 47.90625 L 23 48.625 L 23 47 L 23 44 L 40 44 C 41.64497 44 43
        42.64497 43 41 L 43 5 C 43 3.3550302 41.64497 2 40 2 L 10 2 z M 10 4 L
        40 4 C 40.56503 4 41 4.4349698 41 5 L 41 34 L 9 34 L 9 5 C 9 4.4349698
        9.4349698 4 10 4 z M 13 7 L 13 8 L 13 12 L 13 13 L 14 13 L 18 13 L 19 13
        L 19 12 L 19 8 L 19 7 L 18 7 L 14 7 L 13 7 z M 15 9 L 17 9 L 17 11 L 15
        11 L 15 9 z M 13 16 L 13 17 L 13 21 L 13 22 L 14 22 L 18 22 L 19 22 L 19
        21 L 19 17 L 19 16 L 18 16 L 14 16 L 13 16 z M 15 18 L 17 18 L 17 20 L
        15 20 L 15 18 z M 13 25 L 13 26 L 13 30 L 13 31 L 14 31 L 18 31 L 19 31
        L 19 30 L 19 26 L 19 25 L 18 25 L 14 25 L 13 25 z M 15 27 L 17 27 L 17
        29 L 15 29 L 15 27 z M 9 36 L 41 36 L 41 41 C 41 41.56503 40.56503 42 40
        42 L 23 42 L 23 39 L 23 38 L 22 38 L 14 38 L 13 38 L 13 39 L 13 42 L 10
        42 C 9.4349698 42 9 41.56503 9 41 L 9 36 z M 15 40 L 21 40 L 21 45.375 L
        18.4375 44.09375 L 18 43.875 L 17.5625 44.09375 L 15 45.375 L 15 40 z" />
    </svg>
    <a class="repo-name" href={repoUrl} target="_blank">{repoFullName}</a>
    &nbsp;&nbsp;&nbsp;&nbsp;
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
      <path
        d="M12 .587l3.668 7.568 8.332 1.151-6.064 5.828 1.48
        8.279-7.416-3.967-7.417 3.967 1.481-8.279-6.064-5.828 8.332-1.151z" />
    </svg>
    <span class="repo-name">{starsCount}</span>
  </div>
  {#if description}
    <p>{description.slice(0, 500)}</p>
  {/if}
  <p>
    {#if language}{language}{/if}
    {#if license}&nbsp;&nbsp;&nbsp;&nbsp;{license}{/if}
  </p>

</div>
