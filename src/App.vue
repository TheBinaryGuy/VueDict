<template>
  <div id="app">
    <Header/>
    <TermInput v-on:search="search"/>
    <TermDefinition v-bind:termDef="termDefinition" v-if="err.notFound == false && termDefinition.list.length >= 1"/>
    <TermDefinitionNotFound v-if="err.notFound == true || termDefinition.list.length <= 0"/>
  </div>
</template>

<script>
import axios from "axios";
import TermInput from "./components/TermInput.vue";
import TermDefinition from "./components/TermDefinition.vue";
import TermDefinitionNotFound from "./components/TermDefinitionNotFound.vue";
import Header from "./components/layout/Header.vue";
import { _ } from 'underscore';

export default {
  name: "app",
  data() {
    return {
      termDefinition: {
        list: []
      },
      err: {
        notFound: false,
        sTerm: ""
      }
    };
  },
  components: {
    TermInput,
    TermDefinition,
    Header,
    TermDefinitionNotFound
  },
  methods: {
    search(sTerm) {
      axios
        .get(`https://api.urbandictionary.com/v0/define?term=${sTerm}`)
        .then(res => {
          this.termDefinition.list = _.sortBy(res.data.list, 'written_on').reverse();
        })
        .catch(err => (this.err = { notFound: true, sTerm: sTerm }));
    }
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 10px;
  padding-top: 0;
  background-color: #060606;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
