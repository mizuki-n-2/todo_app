<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <Draggable group="cards" :list="cards" @end="$emit('change')">
      <Card
        v-for="(item, index) in cards"
        :key="item.id"
        :body="item.body"
        :cardIndex="index"
        :listIndex="listIndex"
      />
    </Draggable>
    <CardAdd :listIndex="listIndex" />
  </div>
</template>

<script>
import CardAdd from "./CardAdd.vue";
import Card from "./Card.vue";
import { mapState } from "vuex";
import Draggable from "vuedraggable";

export default {
  components: {
    CardAdd,
    Card,
    Draggable,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    listIndex: {
      type: Number,
      required: true,
    },
    cards: {
      type: Array,
      required: true,
    },
  },
  computed: {
    ...mapState(["lists"]),
    totalCardInList() {
      return this.cards.length;
    },
  },
  methods: {
    removeList() {
      if (confirm("本当にこのリストを削除しますか？")) {
        this.$store.dispatch("removeList", { listIndex: this.listIndex });
      }
    },
  },
};
</script>