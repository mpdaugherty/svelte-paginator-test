<script>
 import Paginator from 'svelte-paginator'

 let letters = '1234567890abcdefghijklmnopqrstuvwxyz'.split('')
 const loadLetters = (page=1, perPage=10) => {
   const start = perPage * (page-1)
   const end = start + perPage
   return {
     items: letters.slice(start, end),
     numItems: letters.length
   }
 }
</script>

<main>
  <h1>Svelte-Paginator!</h1>

  <Paginator endpoint={loadLetters} let:items perPage={5}>
    {#if items === null}
      Loading...
    {:else}
      <div>
        {#each items as letter}
          {letter}&nbsp;
        {/each}
      </div>
    {/if}
  </Paginator>
</main>

<style>
 main {
   text-align: center;
   padding: 1em;
   max-width: 240px;
   margin: 0 auto;
 }

 h1 {
   color: #ff3e00;
   text-transform: uppercase;
   font-size: 4em;
   font-weight: 100;
 }

 @media (min-width: 640px) {
   main {
     max-width: none;
   }
 }
</style>
