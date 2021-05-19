<template>
  <div>
    <header>my toDo</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <Draggable class="list-index" :list="lists" @end="movingList">
        <List
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :listIndex="index"
          :cards="item.cards"
          @change="movingCard"
        />
        <ListAdd />
      </Draggable>
    </main>
  </div>
</template>

<script>
import ListAdd from "./ListAdd.vue";
import List from "./List.vue";
import { mapState } from "vuex";
import Draggable from "vuedraggable";

export default {
  components: {
    ListAdd,
    List,
    Draggable,
  },
  computed: {
    ...mapState(["lists"]),
    totalCardCount() {
      return this.$store.getters.totalCardCount;
    },
  },
  methods: {
    movingCard() {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
    movingList() {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
  },
};
</script>
