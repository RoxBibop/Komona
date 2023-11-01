<template>
  <div class="slider" ref="sliderElement">
    <div class="scrollable" ref="scrollableElement">
      <div class="scrollable-container">
        <div v-for="projet in projets">
          <img :src="projet.img" alt="">
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
const projets = ref([]);
const api_url = 'http://localhost:1337'
const sliderElement = ref(null);
const scrollableElement = ref(null);

const getProjets = async () => {
  try {
    const response = await fetch('http://localhost:1337/api/projets2?populate=*');
    const data = await response.json();
    data.data.forEach(d => {
      console.log( api_url + d.attributes.img.data.attributes.url)
      projets.value.push({
        'label': d.attributes.label,
        'desc' : d.attributes.desc,
        'img': api_url + d.attributes.img.data.attributes.url,
      })
    });

    setListener()
  } catch (error) {
    console.error('Erreur lors de la récupération des données :', error);
  }
} 

const setListener = () => {
  window.addEventListener('scroll', function (e) {
    const elSlider = sliderElement.value;
    const elSliderScroll = scrollableElement.value;
    const scrollTop = window.scrollY - elSlider.offsetTop;

    if (scrollTop <= 0) {
      elSliderScroll.scrollLeft = 0;
    } else if (scrollTop > 0) {
      const scrollH = elSliderScroll.scrollWidth - elSliderScroll.offsetWidth;
      const ratio = (scrollTop) / (elSlider.offsetHeight - window.innerHeight);
      elSliderScroll.scrollTo(scrollH * ratio, 0);
    } else {
      elSliderScroll.scrollLeft = elSliderScroll.scrollWidth;
    }

  })

}

onMounted(getProjets);

</script>

<style lang="scss" scoped>
  .slider {
  height: 500vh;
  .scrollable {
    height: 100vh;
    display: flex;
    align-items: center;
    overflow-x: auto;
  }
  .scrollable-container {
    display: flex;
    align-items: center;
  }
  img {
    flex-shrink: 0;
    margin: 0 2rem;
    max-height: 60vh;
    max-width: none;
  }
  & {
    background-color: rgb(0, 0, 0);
    .scrollable {
      overflow: hidden;
      position: -webkit-sticky;
      position: sticky;
      top: 0;
    }
  }
}

body {
  padding: 10vh 20px;
  font-family: 'Gugi', cursive;
}

h1 {
  text-align: center;
  padding: 100px 0;
  font-size: 10vw;
}

p {
  margin: 25vh 0;
  font-size: calc(6vw + 12px);
  &.small {
    font-size: calc(4vw + 12px);
  }
}


</style>
