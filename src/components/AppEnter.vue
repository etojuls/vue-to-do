<template>
    <div class="todo__log">
        <textarea v-model="additionalItem" :placeholder="placeholder" @keydown.enter="onAddItem"></textarea>
        <button @click="onAddItem">Add new item</button>
    </div>
</template>

<script>
export default {
    name: 'EnterApp',
    props: ['placeholder'],
    emits: ['add-item'],
    data() {
        return {
            additionalItem: ''
        }
    },
    methods: {
        onAddItem() {
            this.$emit('add-item', {
                additionalItem: this.additionalItem
            });
            return this.additionalItem = ''
        }
    }
}
</script>