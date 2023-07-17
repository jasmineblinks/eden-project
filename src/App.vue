<script setup></script>

<template>
  <div class="app">
    <h1>Dog API Example</h1>
    <div class="dog-list">
      <div v-for="dogImage in dogImages" :key="dogImage" class="dog-image">
        <img :src="dogImage" alt="Dog Image" @click="showDogInfo(dogImage)" />
      </div>
    </div>
    <router-view v-if="selectedDog" :dog-info="selectedDogInfo"></router-view>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dogImages: [],
      selectedDog: null,
      selectedDogInfo: null
    }
  },
  created() {
    this.fetchDogImages()
  },
  methods: {
    fetchDogImages() {
      const apiUrl = 'https://dog.ceo/api/breeds/image/random/100'
      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          this.dogImages = data.message
        })
        .catch((error) => {
          console.error('Error:', error)
        })
    },
    showDogInfo(dogImage) {
      this.selectedDog = dogImage
      this.fetchDogInfo(dogImage)
    },
    fetchDogInfo(dogImage) {
      const breed = dogImage.split('/')[4]
      const apiUrl = `https://dog.ceo/api/breed/${breed}/list`
      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          this.selectedDogInfo = {
            breed: breed,
            subBreeds: data.message
          }
        })
        .catch((error) => {
          console.error('Error:', error)
        })
    }
  }
}
</script>

<style scoped>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.dog-list {
  display: flex;
  flex-wrap: wrap;
}

.dog-image {
  flex: 0 0 25%;
  padding: 10px;
  text-align: center;
}

.dog-image img {
  width: 100%;
  cursor: pointer;
}
</style>
