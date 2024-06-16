<template>
    <p>
    <div>
        <input type="text" v-model="newItem" placeholder="Add new todo" @keyup.enter="addNewItem">

        <button type="button" @click="addNewItem"> Add Todo </button>
    </div>
    </p>
    <br />
    <p>
    <h1>TODO:</h1>
    <br>
    <ul>
        <li v-for="item in todoItems" :key="item.key">
            <input type="checkbox" v-model="item.status" v-on:change="() => toggle(item.key, true)" />
            {{ item.value }}
        </li>
    </ul>
    </p>
    <p>
    <h1>Completed:</h1>
    <br>
    <ul>
        <li v-for="item in completedItems" :key="item.key">
            <input type="checkbox" v-model="item.status" v-on:change="() => toggle(item.key, false)" />
            {{ item.value }}
        </li>
    </ul>
    </p>
</template>

<script>
export default {
    name: "HomeView",
    data() {
        return {
            items: [
                {
                    key: 1,
                    value: "Get groceries",
                    status: true
                },
                {
                    key: 2,
                    value: "Get Fan",
                    status: false
                },
            ]
        }
    },
    computed: {
        completedItems() {
            return this.items.filter((item) => item.status);
        },
        todoItems() {
            return this.items.filter((item) => !item.status);
        }
    },
    methods: {
        toggle(key, status) {
            this.items.forEach(element => {
                if (element.key === key) {
                    element.status = status;
                }
            });
        },
        addNewItem() {
            this.items.push({
                key: 100,
                value: this.newItem,
                status: false
            });
            this.newItem = "";
        }
    }
}

</script>