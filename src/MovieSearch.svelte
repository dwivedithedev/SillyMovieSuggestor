<script>
    import Movie from './Movie.svelte';
    import 'bulma/css/bulma.css';
    import { Button } from "svelma";
    let userQuery="brother";
    let movies;

	async function handleSubmit(e){
		e.preventDefault();
		let response = await fetch(`http://www.omdbapi.com/?apikey=fb030055&s=${userQuery}`);
        movies = await response.json();
        console.log(movies.Search);
    }

</script>

<main>
  <div class="hero-body">
    <div class="container">
      <h2>Enter a random Word</h2>
      <form on:submit={handleSubmit}>
        <input type="text" bind:value={userQuery}/>
        <button>Suggest!</button>
      </form>
      {#if movies}
      <ul class='movie-list'>
      {#each movies.Search as movie}
      <li>
      <Movie Title={movie.Title} Poster={movie.Poster} Year={movie.Year} />
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