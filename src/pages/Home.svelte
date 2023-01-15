<script>
  import { onMount } from 'svelte'
  import { writable } from 'svelte/store'

  let albumsState = writable([])

  onMount(() => {
    fetch('https://jsonplaceholder.typicode.com/albums/')
      .then(response => response.json())
      .then(albums => {
        albumsState.set(albums)
      })
      .catch(error => {
        console.log(error)
        return []
      })
  })
</script>

<div class="home">
  <h1>Albuns</h1>

  <div class="card-wrapper">
    {#each $albumsState as album}
      <a href="albuns/{album.id}" class="card">{album.title}</a>
    {/each}
  </div>
</div>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');

  .home {
    padding: 1em;
    background-color: rgb(0, 0, 0);
  }

  .card-wrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    row-gap: 1em;
  }

  .card {
    border-radius: 10px;
    box-shadow: 0px 0px 0px 4px rgba(44, 0, 114, 0.8);
    padding: 30px;
    margin: 20px;
    width: 200px;
    transition: all 0.3s ease-out;
  }

  .card:hover {
    transform: translateY(-5px);
    cursor: pointer;
    color: blueviolet;
    box-shadow: 0px 0px 0px 4px rgba(195, 0, 255, 0.8);
  }

  h1 {
    color: white;
    margin-left: 18px;
  }

  .card::first-letter {
    text-transform: uppercase;
  }
</style>
