<template>
  <div id="pokemon-card">
    <div class="card">
          <div class="card-image">
            <figure>
              <img :src=pokemon.sprite alt="Placeholder image" />
            </figure>
          </div>
          <div class="card-content">
            <div class="media">
              <div class="media-content">
                <p class="title is-4">{{'#' + num + ' '}}{{upper}}</p>
                <p class="subtitle is-6">{{'Type: '}}{{pokemon.type}}</p>
              </div>
            </div>
            <div class="content"></div>
          </div>
        </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Pokemon',
  props: {
    num: Number,
    name: String,
    url: String,
  },
  computed: {
    upper: function () {
      return this.name.charAt(0).toUpperCase() + this.name.slice(1);
    }
  },
  data() {
    return {
      pokemon: {
        type: undefined,
        sprite: undefined
      }
    }
  },
  created: function () {
    axios.get(this.url).then((res) => {
      // eslint-disable-next-line no-undef
      this.pokemon.sprite = res.data.sprites.front_default;
      this.pokemon.type = res.data.types[0].type.name;
    }).catch((error) => {
      console.log(error)
    });
  }
}
</script>

<style scoped>
#pokemon-card {
  margin-top: 2.5%;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
