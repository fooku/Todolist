<template>
  <div id="app">
    <ToDoList :items="sortedItem" @onItemDone="done" />

    <InputForm @onSave="save" />
  </div>
</template>

<script>
import ToDoList from "@/components/ToDoList";
import InputForm from "@/components/InputForm";
import { mapState, mapMutations } from "vuex";
export default {
  name: "app",
  components: {
    ToDoList,
    InputForm
  },
  filters: {
    captitalize(val) {
      return val.toUpperCase();
    }
  },
  mounted() {
    // this.items = JSON.parse(localStorage["items"]);
    this.initItem(JSON.parse(localStorage["items"]));
  },
  computed: {
    ...mapState(["items"]),
    sortedItem() {
      return this.items
        .slice()
        .sort((a, b) => {
          return b.time - a.time;
        })
        .filter(item => {
          return item.complete === false;
        });
    }
  },
  methods: {
    ...mapMutations(["addItem", "initItem"]),
    done(id) {
      this.items = this.items.map(item => {
        if (item.time === id) {
          item.complete = true;
        }
        return item;
      });
      localStorage.setItem("items", JSON.stringify(this.items));
    },
    save(text) {
      this.addItem({
        text: text,
        time: Date.now(),
        complete: false
      });
      localStorage.setItem("items", JSON.stringify(this.items));
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
