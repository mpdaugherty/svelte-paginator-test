<script>
 import Paginator from 'svelte-paginator'

 let letters = '1234567890abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('')
 const loadLetters = (page=1, perPage=10) => {
   const start = perPage * (page-1)
   const end = start + perPage
   return {
     items: letters.slice(start, end),
     numItems: letters.length
   }
 }
</script>

<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">

<main>
  <h1>Svelte-Paginator!</h1>

  <Paginator endpoint={loadLetters} let:items perPage={4} numPageLinks={12}>
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

  <br/>

  <h1>
    Svelte-Paginator!
    <span>&laquo;With Bootstrap Class Overrides&raquo;</span>
  </h1>

  <Paginator endpoint={loadLetters}
                      let:items perPage={4}
                      numPageLinks={12}
             class_button="btn btn-outline-secondary"
             class_current_page="btn btn-secondary"
             class_button_group="btn-group">
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
   margin-bottom: 20px;
 }

 h1>span {
   display: block;
   font-size: 0.333em;
   font-style: italic;
   margin-top: -0.167em
 }

 @media (min-width: 640px) {
   main {
     max-width: none;
   }
 }
</style>
