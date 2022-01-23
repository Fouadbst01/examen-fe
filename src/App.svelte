<script>
	import Movie from "./movie.svelte";
	import { onMount } from 'svelte';
	let movies=[];
	let url ="";
	let pagination={
		skip : 0,
		take : 3
	};
	const getData =async ()=>{
		movies=[];
		url = 'http://localhost:3000/movies?take='+pagination.take+'&skip='+pagination.skip;
		console.log(url);
		const res = await fetch('http://localhost:3000/movies?take='+pagination.take+'&skip='+pagination.skip);
		const {data} = await res.json();
		movies = data;
		console.log(movies.length);
	}
	onMount(getData)

	function handleClick() {
		pagination.skip = pagination.skip + pagination.take;
		getData();
	}
</script>

<div class="container">
	<h1>Movies List</h1>
	<table class="table table-bordered table-striped">
		<thead>
			<tr>
				<th >Title</th>
				<th >Year</th>
				<th >Poster</th>
				<th >Time</th>
				<th >Rating</th>
			</tr>
		</thead>
		<tbody>
			{#each movies as movie ,i (movie.id)}
			<Movie movie={movie}/>
			{:else}
			<h1>... Loding</h1>
			{/each}
		</tbody>
		</table>
		<button type="btn btn-info">
			<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-left-circle" viewBox="0 0 16 16">
				<path fill-rule="evenodd" d="M1 8a7 7 0 1 0 14 0A7 7 0 0 0 1 8zm15 0A8 8 0 1 1 0 8a8 8 0 0 1 16 0zm-4.5-.5a.5.5 0 0 1 0 1H5.707l2.147 2.146a.5.5 0 0 1-.708.708l-3-3a.5.5 0 0 1 0-.708l3-3a.5.5 0 1 1 .708.708L5.707 7.5H11.5z"/>
			</svg>
		</button>

		<button on:click={handleClick} type="btn btn-info">
			<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-right-circle" viewBox="0 0 16 16">
				<path fill-rule="evenodd" d="M1 8a7 7 0 1 0 14 0A7 7 0 0 0 1 8zm15 0A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM4.5 7.5a.5.5 0 0 0 0 1h5.793l-2.147 2.146a.5.5 0 0 0 .708.708l3-3a.5.5 0 0 0 0-.708l-3-3a.5.5 0 1 0-.708.708L10.293 7.5H4.5z"/>
			</svg>
		</button>
</div>

<style>
</style>