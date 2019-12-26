<template>
  <ul>
    <li v-for="item in items" :key="item.time">
      <button @click="itemDone(item.time)">done</button
      >{{ item.text | captitalize }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "InputForm",
  props: {
    items: {
      type: Array
    }
  },
  methods: {
    itemDone(id) {
      this.$emit("onItemDone", id);
    }
  }
};
</script>

<style></style>
