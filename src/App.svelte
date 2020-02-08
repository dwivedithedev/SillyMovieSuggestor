<script>
  import { onMount } from "svelte";
  import 'bulma/css/bulma.css'
  import { Dialog, Button, Icon } from "svelma";

	import Movie from './Movie.svelte';
	import MovieSearch from './MovieSearch.svelte';
	let userQuery="you";
	let randQueryArray=["Fast", "Avengers", "Marvel", "recently", "discovered", "could", "make", "fudge", "with", "just", "chocolate", "chips", "sweet", "mission", "milk", "vanilla", "extract", "and", "thick", "pot", "on", "slow", "heat", "tried", "it", "dark", "chunks", "semi", "sweet", "It's", "better", "both", "kinds", "It", "comes", "out", "pretty", "bad", "The", "best", "are", "crushed", "almonds", "marshmallows", "what", "you", "get", "from", "that", "is", "Rocky", "Road", "takes", "about", "twenty", "minutes", "start", "to", "fridge", "then", "six", "months", "work", "off", "pounds", "gain", "eating", "All", "things", "in", "moderation", "friends"];
	
	let randQuery = randQueryArray[Math.floor(Math.random() * randQueryArray.length)];
	let movies;

	const types = ['is-primary', 'is-success', 'is-danger', 'is-warning', 'is-info', 'is-link']
	let type = 'is-primary'

	// movie from word, you enter a word and get movie wiht that word in title
	// generate a random word in bg, and show movies with that random word in title
	//http://www.omdbapi.com/?apikey=fb030055?s= search term, this is API which returns list of movie containing that word
	 

	onMount(()=>{
		  getMovieList();
		  update();
	})

	async function getMovieList(){
   		let response = await fetch(`http://www.omdbapi.com/?apikey=fb030055&page=1&s=${randQuery}`);
        let text = await response.json(); //Convert the data into JSON format with .json() function
		movies = text; // The converted response I am assigning to 'movies' variable ie the array of response
		console.log(movies.Search) //just testing bruh
	}

	async function update() {
		type = ''

		setTimeout(() => {
		type = types[Math.floor(Math.random() * types.length)];
		}, 1000)
	}
</script>

<main>
<section class="hero {type}">
    <div class="hero-body">
      <div class="container">
        <h1 class="title">
          Silly, Movie Suggester!
        </h1>
        <h2 class="subtitle">
          This Webapp suggests you movies to watch, based on a word you input.
        </h2>
      </div>
    </div>
  </section>
<MovieSearch/>
	<br/>
<span></span>
<section class="hero {type}">
    <div class="hero-body">
      <div class="container">
        <h1 class="subtitle">
          Or Choose from Randomly selected Word...
        </h1>
        <h2 class="title">
          {randQuery}
        </h2>
      </div>
    </div>
  </section>
  
    <div class="hero-body">
      <div class="container">
				{#if movies}
				<ul class='movie-list'>
				{#each movies.Search as movie}
				<li>
				<Movie Title={movie.Title} Poster={movie.Poster} Year={movie.Year} />
				</li>
				{/each}
				</ul>
				{/if}
	<a href="/"><Button type="is-primary" size="is-medium">Not Happy? Give it a Refresh!</Button></a>
	</div>
	</div>
	<footer>
		<span>Made with ❤️ by <a href="http://www.twitter.com/realdesigntack" target='_blank'>VD @ Designtack</a>.</span>
		<br/>
	</footer>
</main>

<style>
	span {
	font-size:small;
	}

	a:hover, a:visited, a:link, a:active
	{
		text-decoration: none;
	}

	.footerText {
		text-align: center;
		color: blue;
	}

	main {
		text-align: center;
		
	}
	
  .movie-list {
    display: flex;
    flex-flow: wrap;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .movie-list li {
	justify-content: center;
    width: 50%;
    padding: 10px;
  }

</style>