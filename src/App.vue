<template>
  <main class="page_content">
    <Accordion v-bind:items="items" />
  </main>
</template>

<script setup>

  import Accordion from "./components/Accordion.vue";

  // load the data to pass to the Accordion component

  const items = [
    {
      id: 1,
      title: "title 1",
      content: "Lorem ipsum dolor sit amet."
    },
    {
      id: 2,
      title: "title 2",
      content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis sagittis libero dui, in lacinia lacus porttitor at. Quisque ut accumsan magna. Donec at dui vitae."
    },
    {
      id: 3,
      title: "title 3",
      content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras eget magna aliquam, aliquet nulla eu, commodo felis. Ut a nibh magna. Nullam sit amet urna eu diam efficitur feugiat sit amet non sapien. Proin libero ante, dapibus vitae fringilla quis, scelerisque id elit. Aliquam erat volutpat. Maecenas quis felis in."
    }
  ];

</script>

<style lang="css" scoped>
  .page_content {
    max-width: 40rem;
    width: 100%;
    margin: 6rem auto auto auto;
  }

  @media only screen and (max-width: 600px) {
    .page_content {
      padding: 1rem;
      margin: 3rem 0 auto 0;
    }
  }
</style>
