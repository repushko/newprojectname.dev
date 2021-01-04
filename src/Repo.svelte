<script>
    export let repoUrl;
    export let repoFullName;
    export let language;
    export let license;
    export let lastUpdate;
    export let description;
    export let starsCount;
</script>

<p>{repoFullName} : {starsCount}</p>
<p>{description}:{license}:{language}</p>