<template>
  <div class="termDef">
    <div class="sorter">
      Sort by:
      <a href class="link" @click="sort(0, $event)">Newest</a> |
      <a href class="link" @click="sort(1, $event)">Oldest</a> |
      <a href class="link" @click="sort(2, $event)">Likes</a> |
      <a href class="link" @click="sort(3, $event)">Dislikes</a>
    </div>
    <div v-for="def in termDef.list" :key="def.defid" class="def">
      <h2 class="word">{{ def.word }} - {{ new Date(def.written_on).getFullYear() }}</h2>
      <p>
        <font-awesome-icon icon="arrow-right"/>
        {{ def.definition }}
      </p>
      <div class="extras">
        <a :href="def.permalink" class="sourceLink" target="_blank">
          <font-awesome-icon icon="link"/>Source
        </a>
        <div class="other">
          <span class="likes">
            <font-awesome-icon icon="thumbs-up"/>
            : {{ def.thumbs_up }}
          </span>
          <span class="dislikes">
            <font-awesome-icon icon="thumbs-down"/>
            : {{ def.thumbs_down }}
          </span>
          <span class="author">
            <font-awesome-icon icon="user"/>
            : {{ def.author.toLowerCase() }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { _ } from "underscore";
export default {
  name: "TermDefinition",
  props: ["termDef"],
  methods: {
    sort(sorter, e) {
      e.preventDefault();
      switch (sorter) {
        case 0:
          this.termDef.list = _.sortBy(
            this.termDef.list,
            "written_on"
          ).reverse();
          break;
        case 1:
          this.termDef.list = _.sortBy(this.termDef.list, "written_on");
          break;
        case 2:
          this.termDef.list = _.sortBy(
            this.termDef.list,
            "thumbs_up"
          ).reverse();
          break;
        case 3:
          this.termDef.list = _.sortBy(
            this.termDef.list,
            "thumbs_down"
          ).reverse();
          break;
        default:
          console.log("Something went wrong!");
          break;
      }
    }
  }
};
</script>

<style scoped>
.termDef {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.sorter {
  color: white;
}

.def {
  background-color: rgba(106, 90, 205, 0.5);
  color: white;
  padding: 10px;
  margin-bottom: 10px;
  margin-top: 10px;
  width: calc(100% - 30px);
}

.def .word {
  margin: 0;
  font-weight: bold;
}

.def p {
  padding-left: 10px;
}

.extras {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.sourceLink,
.link {
  color: rgb(0, 136, 255);
  text-decoration: none;
}

.likes {
  margin-right: 10px;
}

.fa-thumbs-up {
  color: rgb(0, 255, 0);
}

.dislikes {
  margin-right: 10px;
}

.fa-thumbs-down {
  color: rgb(255, 0, 0);
}

.fa-user {
  color: rgb(0, 136, 255);
}

@media screen and (max-width: 600px) {
  .extras {
    flex-direction: column;
    align-items: flex-end;
  }

  .other {
    margin-top: 10px;
  }
}
</style>
