<template>
  <!-- ★ここから追記 -->
  <form :class="classList" @submit.prevent="addList">
    <input
      v-model="title"
      type="text"
      class="text-input"
      placeholder="Add new list"
      @focusin="startEditing"
      @focusout="finishEditing"
    />
    <button type="submit" class="add-button" v-if="isEditing || titleExists">
      Add
    </button>
  </form>
  <!-- ★ここまで追記 -->
</template>

<script>
export default {
  data: function () {
    return {
      title: "",
      isEditing: false, // ★追記
    };
  },
  computed: {
    classList() {
      const classList = ["addlist"];
      if (this.isEditing) {
        classList.push("active");
      }
      if (this.titleExists) {
        classList.push("addable");
      }
      return classList;
    },
    titleExists() {
      return this.title.length > 0;
    },
  },
  // ★ここから追記
  methods: {
    addList: function () {
      this.$store.dispatch("addlist", { title: this.title });
      this.title = "";
    },
    startEditing() {
      this.isEditing = true;
    },
    finishEditing() {
      this.isEditing = false;
    },
  },
  // ★ここまで追記
};
</script>
