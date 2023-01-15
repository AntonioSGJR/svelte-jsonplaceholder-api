<script>
  export let id
  import { onMount } from 'svelte'
  import { writable } from 'svelte/store'

  let albumState = writable({})
  let photosState = writable([])
  let album

  albumState.subscribe(value => (album = value))

  onMount(() => {
    fetch(`https://jsonplaceholder.typicode.com/albums/${id}`)
      .then(response => response.json())
      .then(albums => {
        albumState.set(albums)
      })
      .catch(error => {
        console.log(error)
        return []
      })

    fetch(`https://jsonplaceholder.typicode.com/albums/${id}/photos`)
      .then(response => response.json())
      .then(photos => {
        photosState.set(photos)
      })
      .catch(error => {
        console.log(error)
        return []
      })
  })
</script>

<main>
  <h2>Album</h2>
  <div class="info">
    <h1>{album.title}</h1>
    <p>Albúm: {album.id}</p>
    <p>Usuário: {album.userId}</p>
  </div>
  <div>
    <h2>Fotos</h2>
    <div class="photos">
      {#each $photosState as photo}
        <img src={photo.thumbnailUrl} alt="Album photo" class="card" />
      {/each}
    </div>
  </div>
</main>

<style>
  main {
    padding: 1em;
    background-color: rgb(0, 0, 0);
    padding: 10px;
    transition: all 0.3s ease-out;
  }

  .info {
    border-radius: 10px;
    box-shadow: 0px 0px 0px 4px rgba(44, 0, 114, 0.8);
    padding: 30px;
    margin: 20px;
    transition: all 0.3s ease-out;
  }

  h1 {
    color: white;
  }

  h2 {
    color: white;
    margin-left: 18px;
  }

  p {
    color: white;
  }

  h2 {
    color: white;
  }

  .photos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(9rem, 1fr));
    gap: 1rem;
    border-radius: 10px;
    box-shadow: 0px 0px 0px 4px rgba(44, 0, 114, 0.8);
    padding: 30px;
    margin: 20px;
    transition: all 0.3s ease-out;
  }

  .photos,
  img {
    border-radius: 6px;
  }

  main::first-letter {
    text-transform: uppercase;
  }

  .info::first-letter {
    text-transform: uppercase;
  }
</style>
