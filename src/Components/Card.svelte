<script>
  /* props */
  export let name;
  export let pic;
</script>

<div class="card">
  <p class="name">{name}</p>
  <img src={pic} alt="pokemon">
</div>

<style>
    .card {
        width: 300px;
        height: 200px;
        background: rgba(238,130,238,0.23);
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin: 5px;
    }
    .card img {
        width: 100px;
    }
    .card p {
        font-size: 25px;
    }
</style>