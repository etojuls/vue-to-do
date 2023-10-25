<template>
    <div class="todo__info">
        <div class="todo__summary">
            <p v-if="items.length > 0">
                {{ itemsCount }} items left from {{ items.length }}
            </p>
            <p v-else>no items left</p>
        </div>
        <div class="todo__list">
          <transition-group name="list" tag="ul">
            <li class="todo__item" v-for="item in items" :key="item">
              <div class="todo__item-inner">
                <div class="todo__title" :class="{ 'todo__checked': item.checked }">
                  {{ item.title }}
                </div>
                <input type="checkbox" v-model="item.checked">
              </div>
              <button class="todo__delete" @click="onDeleteItem(item)">delete me</button>
            </li>
          </transition-group>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ListApp',
    props: ['items'],
    emits: ['item-delete'],
    data() {
        return {
            itemsChecked: ''
        }
    },
    methods: {
        onDeleteItem(item) {
            this.$emit('item-delete', item);
        }
    },
    computed: {
        itemsCount() {
            let itemsChecked = this.items.filter(item => item.checked).length;
            console.log(itemsChecked);
            return itemsChecked
        }
    }
}
</script>

<style>
.todo__info {
    color: #fff;
}

button {
    cursor: pointer;
}

.todo__checked {
    text-decoration: line-through;
}

.todo__list {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    background-color: #efa43e;
    overflow: hidden;
    border-radius: 15px;
}

.todo__title {
    margin-right: 1rem;
}

.todo__item {
    display: flex;
    align-items: center;
    min-height: 50px;
    padding: 5px 20px;
    font-size: 20px;
    width: 95%;
    justify-content: space-between;
}

.todo__item-inner {
    display: flex;
}

.todo__item:not(:last-child) {
    border-bottom: 1px solid #ebebeb;
}

.todo__summary {
    font-size: 2rem;
    text-align: end;
}

.todo__delete {
    background-color: #fff;
    border-radius: 15px;
    border: 1px solid #ccc;
    padding: 5px 10px;
    transition: .3s ease all;
}

.todo__delete:hover {
    box-shadow: 0 5px 10px rgba(0, 0, 0, .3);
}
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style> 