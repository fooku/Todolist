<template>
  <form @submit.prevent="save()">
    <input type="text" v-model="inputText" />
    <button type="summit">save</button>
  </form>
</template>

<script>
export default {
  name: "ToDoList",
  data() {
    return {
      inputText: ""
    };
  },
  methods: {
    save() {
      this.$emit("onSave", this.inputText);
    }
  }
};
</script>

<style></style>
