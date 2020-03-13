<template>
  <div class="about">
    <div class="results">
      <div v-for="item in items" :key="item.param" class="result-item">
        <img class="result-item__poster" :src="item.Poster" :alt="item.Title" />
        <h3>{{ item.Title }}</h3>
        <p>{{ item.Year }}</p>
      </div>
    </div>
  </div>
</template>
<style scoped>
.about {
  max-width: 1170px;
  margin: 0 auto;
}
.result-item {
  flex-basis: calc(25% - 20px);
  box-shadow: 2px 0px 9px -2px rgba(0, 0, 0, 0.75);
  margin: 20px 10px;
}
.result-item img {
  width: 100%;
  height: 400px;
  object-fit: cover;
}
.results {
  display: flex;
  flex-wrap: wrap;
  /* justify-content: space-between; */
}
</style>

<script>
export default {
  name: "Results",
  props: ["items"]
};
</script>
