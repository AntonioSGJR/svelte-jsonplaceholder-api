<script>
  import {onMount} from 'svelte'  


  onMount(() => {
    fetch("https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=Bourbon")
    .then(response => response.json())
    .then(data => {
      console.log(data);
    }).catch(error => {
      console.log(error);
      return [];
    });
  })
</script>