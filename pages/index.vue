<template>
  <div class="container">
    <div class="pokemon">ポケモン タイプ一覧</div>
    <div class="top">
      <div class="top__no">No</div>
      <div class="top__name">名前</div>
      <div class="top__type--1">タイプ1</div>
      <div class="top__type--2">タイプ2</div>
    </div>
    <div v-for="(pokemon, index) in pokemons" :key="index" class="content">
      <div class="content__no">{{ pokemon.no }}</div>
      <div class="content__name">{{ pokemon.name }}</div>
      <div class="content__type--1">{{ pokemon.types[0] }}</div>
      <div v-if="pokemon.types[1]" class="content__type--2">
        {{ pokemon.types[1] }}
      </div>
      <div v-else class="content__type--2">{{ none }}</div>
    </div>
  </div>
</template>

<script>
const axios = require('axios')
const url =
  'https://raw.githubusercontent.com/kotofurumiya/pokemon_data/master/data/pokemon_data.json'

export default {
  asyncData({ params, error }) {
    return axios
      .get(url)
      .then((res) => {
        return { pokemons: res.data }
      })
      .catch((e) => {
        error({ pokemon: e.response.status, message: 'ERROR!!' })
      })
  },
  data() {
    return {
      none: '　'
    }
  }
}
</script>

<style lang="scss">
.container {
  margin: 50px auto;
  padding: 0;
}

.pokemon {
  font-size: 25px;
  margin-bottom: 10px;
  font-weight: bold;
  text-align: center;
}

@mixin text {
  display: inline-block;
  text-align: center;
  letter-spacing: normal;
  border-bottom: solid 1px #000;
  border-right: solid 1px #000;
  height: 34px;
}

.top {
  letter-spacing: -0.4em;
  line-height: 30px;
  width: 400px;
  margin: 0 auto;
  &__no {
    @include text;
    border-top: solid 1px #000;
    border-left: solid 1px #000;
    width: 50px;
    font-weight: bold;
  }
  &__name {
    @include text;
    border-top: solid 1px #000;
    width: 150px;
    font-weight: bold;
  }
  &__type--1 {
    @include text;
    border-top: solid 1px #000;
    width: 100px;
    font-weight: bold;
  }
  &__type--2 {
    @include text;
    border-top: solid 1px #000;
    width: 100px;
    font-weight: bold;
  }
}

.content {
  letter-spacing: -0.4em;
  line-height: 30px;
  width: 400px;
  margin: 0 auto;
  &__no {
    @include text;
    border-left: solid 1px #000;
    width: 50px;
  }
  &__name {
    @include text;
    width: 150px;
  }
  &__type--1 {
    @include text;
    width: 100px;
  }
  &__type--2 {
    @include text;
    width: 100px;
  }
}
</style>
