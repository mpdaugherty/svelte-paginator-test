<script>
 import Paginator from 'svelte-paginator'

 let letters = '1234567890abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('')
 const loadLetters = async (page=1, perPage=10) => {
   await new Promise(resolve => setTimeout(resolve, 1500))
   const start = perPage * (page-1)
   const end = start + perPage
   return {
     items: letters.slice(start, end),
     numItems: letters.length
   }
 }

 let reset = null
 const switchToGreek = () => {
   letters = 'αβγδεζηθικλμνξοπρστυφχψωΑΒΓΔΕΖΗΘΙΚΛΜΝΞΟΠΡΣΤΥΦΧΨΩ'
   reset()
 }
</script>

<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">

<div class="main">
  <h1>Svelte-Paginator!</h1>

  <Paginator loadItems={loadLetters} perPage={4} numPageLinks={12} currentPage={2} let:items let:loading bind:reset>
    <div>
      {#if loading}
        Loading...
      {:else}
        {#each items as letter}
          {letter}&nbsp;
        {:else}
          None
        {/each}
      {/if}
    </div>
  </Paginator>

  <br/>
  <button on:click={switchToGreek}>Switch to Greek</button>

  <h1>
    Svelte-Paginator!
    <span>&laquo;With Bootstrap Class Overrides&raquo;</span>
  </h1>

  <Paginator loadItems={loadLetters}
             let:items
             let:loading
             perPage={4}
             numPageLinks={5}
             class_button="btn btn-outline-secondary"
             class_current_page="btn btn-secondary"
             class_button_group="btn-group">
    <div class="my-3">
      {#if loading}
        Loading...
      {:else}
        {#each items as letter}
          {letter}&nbsp;
        {:else}
          None
        {/each}
      {/if}
    </div>
  </Paginator>
</div>

<style>
 .main {
   text-align: center;
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
