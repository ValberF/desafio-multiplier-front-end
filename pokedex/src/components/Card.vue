<template>
    <b-card
      :title="title"
      :img-src="image"
      :img-alt="imageAlt"
      img-top
      style="max-width: 11rem"
      class="mb-5 text-center"
    >
      <b-button href="#" variant="primary">Capturar</b-button>
    </b-card>
</template>

<script>
export default {
  name: "Card",
  props: {
    title: String,
    image: String,
    imageAlt: String,
  },
};
</script>

<style scope>
.mb-5 {
  padding: 0.7rem;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);

  align-items: center;
}
</style>