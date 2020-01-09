<template>
  <div class="home" v-if="loaded">
    <h1>{{ displayedCardData.question }}</h1>

    <div class="content" v-html="markdown.toHTML(displayedCardData.answer)">
    </div>

    <a id="random-button" @click="displayRandomCard">Random</a>
  </div>
</template>

<script>
// @ is an alias to /src
import data from '@/data.json'
import {markdown} from 'markdown'

export default {
  name: 'home',

  data() {
    return {
      markdown,
      loaded: false,
      allCards: data,
      allCardIds: [],
      displayedCardId: 0,
      displayedCardData: null,
    }
  },

  created() {
    this.allCardIds = Object.keys(this.allCards).map(x => Number(x))
  },

  mounted() {
    this.displayRandomCard()
    this.loaded = true
  },

  methods: {
    getRandomCardID() {
      return Math.floor(Math.random() * this.allCardIds.length)
    },

    displayInfo() {
      this.displayedCardData = this.allCards[this.displayedCardId]
    },

    displayRandomCard() {
      this.displayedCardId = this.getRandomCardID()
      this.displayInfo()
    }
  }
}
</script>

<style lang="scss">

.home {
  max-width: 700px;
  padding: 1rem;
  margin: 0 auto;

  p {
    font-size: 1.5em;
  }
}

#random-button {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  z-index: 30;
  border: 1px solid black;
  padding: 1rem;
  border-radius: 2px;
  cursor: pointer;

  &:hover {
    color: white;
    background-color: black;
  }
}
</style>
