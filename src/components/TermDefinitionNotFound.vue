<template>
  <div class="termDef">
    <h2 class="word">Nothing to report chief...</h2>
  </div>
</template>

<script>
import { _ } from "underscore";
export default {
  name: "TermDefinitionNotFound"
};
</script>

<style scoped>
.termDef {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.word {
  margin: 0;
  font-weight: bold;
  color: white;
}
</style>
