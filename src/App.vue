<script setup> 
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
</script>

<template>
<div class="backgroundColor">
<Header/>
  <div>
    <div class="centering">
    <button @click="getCuteDogs">Get your cute dogs </button>
    </div>
    <div class="centerAll">
    <div class="centerImage">
    <div v-for="item in cuteDogs" class="adjust">
    <img :src="item.url" alt="" class="imageAdjust">
    </div>
    </div>
    </div>
  </div>
  <Footer/>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cuteDogs: [],
    };
  },
  methods: {
    getCuteDogs() {
      fetch('https://api.thedogapi.com/v1/images/search?limit=10')
        .then((response) => response.json())
        .then((data) => {
          this.cuteDogs = data;
        })
        .catch((error) => {
          console.error('Error when searching for dogs:', error);
        });
    },
  },
};
</script>

<style scoped>

*,html,body{
  margin:0;
  padding:0;
}

.backgroundColor{
  background-image: url('background.jpg');
  background-size:cover;
  background-repeat:no-repeat;
  min-width: 100vw;
  padding-right: 40px;
}

button {
  margin-top:4px;
  background-color: rgba(46, 204, 113, 0.7);
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background: linear-gradient(to bottom, #87CEFA, #FFC0CB);
}

.centerAll{
  display:flex;
  align-items:center;
  justify-content:center;
  min-height:576px;
}

.centering{
  display:flex;
  align-items:center;
  justify-content:center;
}

.centerImage{
  display:flex;
  align-items:center;
  justify-content:center;
  flex-wrap:wrap;
  max-width:1200px;
}

.adjust {
  display:inline-flex;
  align-items:center;
  justify-content:center;
  text-align: center;
  margin-top: 20px;
  padding-left:37px;
}

.imageAdjust{
  width:200px;
  height:200px;
  border-radius:20px;
  border: 2px solid black;
}

.imageAdjust:hover{
  box-shadow: 2px 2px 200px 2px white;
}

</style>
