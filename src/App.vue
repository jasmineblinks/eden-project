<script setup></script>

<template>
  <div class="app">
    <header>
      <nav>
        <div class="logo">
         
          <h1>Edenlife Dog Care</h1>
        </div>
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">Services</a></li>
          <li><a href="#">Gallery</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <section class="hero">
        <div class="hero-content">
          <h2>Welcome to Edenlife Dog Care</h2>
          <p>Your dog's home away from home.</p>
          <a href="#" class="btn btn-primary">Learn More</a>
        </div>
      </section>
      <section class="dog-list">
        <h2>Our Gallery</h2>
        <div class="dog-images-container">
          <div class="dog-image" v-for="dogImage in dogImages" :key="dogImage" @click="showDogInfo(dogImage)">
            <img :src="dogImage" alt="Dog Image">
          </div>
        </div>
      </section>
    </main>
    <footer>
      <p>&copy; 2023 Edenlife Dog Care. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dogImages: [],
    };
  },
  created() {
    this.fetchDogImages();
  },
  methods: {
    fetchDogImages() {
      const apiUrl = 'https://dog.ceo/api/breeds/image/random/100';
      fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
          this.dogImages = data.message;
        })
        .catch(error => {
          console.error('Error:', error);
        });
    },
    showDogInfo(dogImage) {
      // Navigate to the dog info page
      this.$router.push({
        name: 'DogInfo',
        params: {
          dogImage: dogImage
        }
      });
    }
  }
};
</script>

<style>
/* Reset some default styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Global styles */
body {
  font-family: Arial, sans-serif;
  background-color: #f2f2f2;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

/* Header styles */
header {
  background-color: #333;
  color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 10px 0;
}

nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
}

nav .logo {
  display: flex;
  align-items: center;
}

nav .logo img {
  width: 50px;
  margin-right: 10px;
}

nav ul {
  display: flex;
  list-style: none;
}

nav ul li {
  margin-left: 20px;
}

nav ul li a {
  color: #333;
  text-decoration: none;
  font-weight: 600;
}

/* Main content styles */
main {
  padding: 40px 0;
}

.hero {
  background-image: url("./assets/hero-bg.jpg");
  background-size: cover;
  background-position: center;
  padding: 100px 0;
  text-align: center;
  color: #fff;
}

.hero-content h2 {
  color: #333;
  font-size: 36px;
  margin-bottom: 20px;
}

.hero-content p {
  color: #333;
  font-size: 18px;
  margin-bottom: 30px;
}

.btn {
  display: inline-block;
  padding: 10px 20px;
  border-radius: 4px;
  color: #fff;
  font-weight: 600;
  text-decoration: none;
}

.btn-primary {
  background-color:#3A5F0B;
}

.dog-list {
  background-color: #fff;
  padding: 40px;
  text-align: center;
}

.dog-list h2 {
  color: #333;
  font-size: 30px;
  margin-bottom: 30px;
}

.dog-images-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}

.dog-image img {
  width: 100%;
  border-radius: 4px;
  cursor: pointer;
}

/* Footer styles */
footer {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 20px;
}
</style>
