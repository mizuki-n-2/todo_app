<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <div class="card-index">
      <Card
        v-for="(item, index) in cards"
        :key="item.id"
        :body="item.body"
        :cardIndex="index"
        :listIndex="listIndex"
      />
      <CardAdd :listIndex="listIndex" />
    </div>
  </div>
</template>

<script>
import CardAdd from "./CardAdd.vue";
import Card from "./Card.vue";
import { mapState } from "vuex";

export default {
  components: {
    CardAdd,
    Card,
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
      required: true
    }
  },
  computed: {
    ...mapState(["lists"]),
    totalCardInList() {
      return this.cards.length
    }
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