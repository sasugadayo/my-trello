<template>
  <div>
    <header>my Trello</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <div class="list-index">
        <draggable :list="lists" @end="movingList" class="list-index">
          <list
            v-for="(item, index) in lists"
            :key="item.id"
            :title="item.title"
            :cards="item.cards"
            :listIndex="index"
            @change="movingCard"
          />
          <list-add />
        </draggable>
      </div>
      <!-- ★ここに追記 -->
    </main>
  </div>
</template>

<script>
// ★ここに追記
import draggable from "vuedraggable";
import ListAdd from "./ListAdd.vue";
import List from "./List";
import { mapState } from "vuex";

export default {
  // ★ここから追記
  components: {
    draggable,
    ListAdd,
    List,
  },
  // ★ここまで追記
  computed: {
    ...mapState(["lists"]),
    totalCardCount() {
      return this.$store.getters.totalCardCount;
    },
  },
  methods: {
    movingCard: function () {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
    movingList: function () {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
  },
};
</script>
