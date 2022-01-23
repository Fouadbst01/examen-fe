<script>
  export let movie;
</script>


<tr>
  <th>{movie.title}</th>
  <td>{movie.year}</td>
  <td><img class="img"  src="{movie.poster}"/></td>
  <td>{movie.runtime} min</td>
  <td>{movie.imdb.rating}</td>
</tr>


<style>
  .img{
    height:200px;
    width: 150px;
    object-fit: cover;
  }

</style>