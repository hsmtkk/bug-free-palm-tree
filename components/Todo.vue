<template>
    <v-container>
        <v-text-field label="New Todo" v-model="newTodo"></v-text-field>
        <v-btn v-on:click="addTodo">Submit</v-btn>
    </v-container>
    <v-container>
        <v-list>
            <v-list-item v-for="(todo, index) in todos" v-bind:key="index">
                <v-row>
                    <v-col cols="1">
                        <v-checkbox v-on:change="toggleTodo(index)" v-bind:model-value="todo.done" />
                    </v-col>
                    <v-col>
                        <v-list-item-title>
                            <s v-if="todo.done">
                                <span>{{ todo.done }} {{ todo.content }}</span>
                            </s>
                            <span v-else>{{ todo.done }} {{ todo.content }}</span>
                        </v-list-item-title>
                    </v-col>
                    <v-col cols="1">
                        <v-icon icon="mdi-delete" v-on:click="deleteTodo(index)" />
                    </v-col>
                </v-row>
            </v-list-item>
        </v-list>
    </v-container>
</template>

<script setup lang="ts">
class Todo {
    done: boolean
    content: string
    constructor(done: boolean, content: string) {
        this.done = done
        this.content = content
    }
}

const newTodo = ref("")

const todos = ref([new Todo(true, "Alpha"), new Todo(false, "Bravo")])

const addTodo = () => {
    console.log("newTodo")
    const newItem = new Todo(false, newTodo.value)
    todos.value.push(newItem)
}

const toggleTodo = (index: number) => {
    console.log("toggleTodo")
    const todo = todos.value[index]
    todo.done = !todo.done
}

const deleteTodo = (index: number) => {
    console.log("deleteTodo")
    console.log("index")
    console.log(index)
    todos.value.splice(index, 1)
}
</script>
