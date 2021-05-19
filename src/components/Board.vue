<template>
  <div>
    <header>my toDo</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <div class="list-index">
        <List
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :listIndex="index"
          :cards="item.cards"
        />
        <ListAdd />
      </div>
    </main>
  </div>
</template>

<script>
import ListAdd from "./ListAdd.vue";
import List from "./List.vue";
import { mapState } from "vuex";

export default {
  components: {
    ListAdd,
    List,
  },
  computed: {
    ...mapState(["lists"]),
    totalCardCount() {
      return this.$store.getters.totalCardCount;
    },
  },
};
</script>
