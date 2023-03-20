<template>
  <div class="card" @mouseenter="showBack()" @mouseleave="showFront()">
    <div class="card-image">
      <figure class="image">
        <img
          :src="pokemon.currentImg"
          alt="Placeholder image"
        />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{num}}. {{name}}</p>
          <p class="subtitle is-6">{{pokemon.type}}</p>
        </div>
      </div>
      <div class="content">
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      pokemon: {
        type: '',
        front: '',
        back: '',
        currentImg: ''
      },
    };
  },
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.pokemon.currentImg = res.data.sprites.front_default;
    });
  },
  props: {
    name: String,
    url: String,
    num: Number,
  },
  methods: {
    showFront: function() {
        this.pokemon.currentImg = this.pokemon.front;
    },
    showBack: function() {
        this.pokemon.currentImg = this.pokemon.back;
    }
  }
};
</script>

<style scoped>
.card {
    max-width: 400px;
    margin: 0 auto;
    margin-top: 20px;
}
</style>