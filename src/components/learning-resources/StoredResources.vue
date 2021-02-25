<template>
  <ul>
    <learning-resource
      v-for="item in resources"
      :id="item.id"
      :key="item.id"
      :title="item.title"
      :link="item.link"
      :description="item.description"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from './LearningResource.vue';

export default {
	components: {
		LearningResource
	},
	inject: ['resources']
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>