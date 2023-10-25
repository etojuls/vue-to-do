<template>
  <div class="todo">
    <div class="todo__container">
      <div class="todo__inner">
        <div class="todo__title-wrapper">
          <h1 class="todo__title">My To-Do list</h1>
        </div>
        <app-list :items="items" @item-delete="itemDelete"></app-list>
        <app-enter :placeholder="placeholder" @add-item="addItem"></app-enter>
      </div>
    </div>
  </div>
</template>

<script>
import AppList from "./components/AppList.vue";
import AppEnter from "./components/AppEnter.vue";

export default {
  name: 'App',
  components: {
    AppList, AppEnter
  },
  data() {
    return {
      items: [
        {
          title: 'brush my teeth',
          checked: true
        },
        {
          title: 'drink my coffee',
          checked: false
        },
        {
          title: 'check out the inbox',
          checked: true
        },
      ],
      placeholder: 'enter a new item'
    }
  },
  methods: {
    addItem(data) {
      let newArr = {
        title: data.additionalItem,
        checked: false,
      };
      console.log(data)
      this.items.push(newArr);
      console.log(this.items)
    },
    itemDelete(item) {
      console.log('gfdg')
      let index = this.items.indexOf(item);
      this.items.splice(index, 1);
      console.log(item, index)
    }
  }
}
</script>

<style>
body {
  font-family: 'Roboto', sans-serif;
  background-color: #4f95b2;
}

.todo {
  text-align: center;
}

.todo__container {
  padding: 0 calc(((100vw/12)*.974)*3);
}

.todo__title-wrapper {
  background: #fff;
  padding: 15px;
  border-radius: 15px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, .3);
  margin-bottom: 4rem;
}
</style>
