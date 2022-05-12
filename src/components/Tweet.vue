<script setup lang="ts">
import { ref } from 'vue'
const tweets = ref([{ id: 0, description: 'hello world' }, { id: 1, description: 'this is second tweet' }])
const inputtingDescription = ref<string>('')
const postTweet = () => {
    const tweet = {id: Math.random(), description: inputtingDescription.value} 
    tweets.value.push(tweet)
    inputtingDescription.value = ''
    console.log('inputtingDescription:' + inputtingDescription.value)
}
</script>

<template>
    <div class="container">
        <h1>Tweeter</h1>
        <div class="form-container">
            <input v-model="inputtingDescription" />
            <button class="save-button" @click="postTweet">post</button>
        </div>
        <div class="tweet-container">
            <ul>
                <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
                    <span>{{ tweet.description }}</span>
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.form-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: aliceblue;
    padding: 24px 0;
    width: 60%;
    margin-bottom: 12px;
    border-radius: 4px;
}

.tweet-list {
    list-style: none;
    margin-bottom: 12px;
    border-radius: 4px;
    font-size: 12px;
    display: flex;
    justify-content: space-between;
    background-color: rgb(170, 203, 233);
    padding: 8px 20px;
    width: 300px;
}

button {
    background-color: #68c9c9;
    color: #fff;
    border-radius: 2px;
    border: none;
    width: 60px;
    height: 22px;
    margin: 8px;
}

button:hover {
    background-color: #37bdbd;
}
</style>