<template>
  <div>
    <h2>Selected Dog</h2>
    <div class="dog-info">
      <img :src="dogImage" alt="Selected Dog Image" width="400" height="400" />
      <p>Breed: {{ dogInfo.breed }}</p>
      <p v-if="dogInfo.subBreeds.length > 0">Sub-breeds: {{ dogInfo.subBreeds.join(', ') }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dogInfo: {
      type: Object,
      required: true
    }
  },
  computed: {
    dogImage() {
      // Assuming the breed is always the first part of the dog image URL
      const breed = this.dogInfo.breed
      return `https://images.dog.ceo/breeds/${breed}/n021${breed}_001.jpg`
    }
  }
}
</script>

<style scoped>
.dog-info {
  text-align: center;
}

.dog-info img {
  width: 400px;
  height: 400px;
  object-fit: cover;
}
</style>
