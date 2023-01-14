<script>
  import { onMount } from 'svelte'  
  import { writable } from 'svelte/store';

  let albumsState = writable([])

  onMount(() => {
    fetch("https://jsonplaceholder.typicode.com/albums/")
    .then(response => response.json())
    .then(albums => {
      albumsState.set(albums)
    }).catch(error => {
      console.log(error);
      return [];
    });
  })
</script>

<div class="home">
  <h1>Albums</h1>

  <div class="card-wrapper">
    {#each $albumsState as album}
      <a href="albuns/{album.id}" class="card">{album.title}</a>
    {/each}
  </div>
</div>

<style>
  .home {
    padding: 1em;
  }

  .card-wrapper {
    display: flex;
    flex-wrap: wrap;

    justify-content: space-between;
    row-gap: 1em;
  }

  .card {
    border: 1px solid #ccc;
    width: 20%;
    height: 200px;

    display: flex;
    justify-content: center;
    align-items: center;

    color: #444;

    border-radius: 6px;
  }
</style>