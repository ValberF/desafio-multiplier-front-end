<template>
  <div>
    <b-navbar
      class="shadow p-3 mb-5"
      toggleable="lg"
      type="dark"
      variant="danger"
    >
      <b-navbar-brand>
        <b-link to="/">
          <b-img
            src="http://1.bp.blogspot.com/-0V4itR_v87M/UtsCF-ehNYI/AAAAAAAABjU/UEQ5Jiy_85o/s1600/pokedex-3d-logo.png"
            fluid
            alt="Pokedex logo"
          />
        </b-link>
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item to="/">Pokémons</b-nav-item>
          <b-nav-item to="/pokedex">PokéDex</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img {
  width: 150px;
}

a {
  font-size: 1.5rem;
  text-decoration: none;
  color: #fff;
}
</style>
