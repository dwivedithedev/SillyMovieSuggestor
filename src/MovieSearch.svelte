<script>
    import Movie from './Movie.svelte';
    import 'bulma/css/bulma.css';
    import { Field, Input, Button } from "svelma";
    import { onMount } from 'svelte';
    let movies;

	async function handleSubmit(e){
    e.preventDefault();
        let userQuery = document.getElementById('user_input').value;
		    let response = await fetch(`http://www.omdbapi.com/?apikey=fb030055&s=${userQuery}`);
        movies = await response.json();
        //console.log(movies.Search);
    }

    onMount(()=>{
     
    })

</script>

<main>
  <div class="hero-body buttons">
    <div class="container">
      <h1 class="subtitle">Enter a random Word</h1>
      <form on:submit={handleSubmit}>
        <Field>
          <Input id="user_input" placeholder="Your random word here..." type="is-success" size="is-large"/>
        </Field>
        <Field>
          <Button id="sbmt" type="submit is-primary" size="is-large" on:click={handleSubmit}>Suggest</Button> 
        </Field> 
      </form>
      {#if movies}
      <ul class='movie-list'>
      {#each movies.Search as movie}
      <li>
      <Movie Title={movie.Title} Poster={movie.Poster} Year={movie.Year}/>
      </li>
      {/each}
      </ul>
      {/if}
    </div></div>
</main>

 <style>
        .movie-list {
    display: flex;
    flex-flow: wrap;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .movie-list li {
	justify-content: space-between;
    width: 50%;
    padding: 10px;
  }
      .movie-search {
        padding: 20px;
        border-radius: 10px;
        margin-bottom: 50px;
        background: #efefef;
      }
    
      h2 {
        margin: 0 0 15px;
      }
    </style>