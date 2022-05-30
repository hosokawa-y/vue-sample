<script setup lang="ts">
import { ref, Ref } from "vue"
import PersonPostForm from './PersonPostForm.vue'
import PersonList from './PersonList.vue'

export type Person = {
    id: number,
    name: string,
    age: number
}

const persons: Ref<Person[]> = ref([{ id: 0, name: "john", age: 30 }, { id: 1, name: "hoso", age: 34 }])
</script>

<template>
    <div class="container">
        <h1>test</h1>
        <PersonPostForm />
        <div class="list-container"></div>
        <ul>
            <PersonList :persons="persons" />
        </ul>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>