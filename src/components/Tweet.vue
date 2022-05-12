<script setup lang="ts">
import { ref } from 'vue'

const tweets = ref([{ id: 0, description: 'hello world' }, { id: 1, description: 'this is second tweet' }])

const inputtingDescription = ref<string>('')
const postTweet = () => {
    const tweet = {id: Math.random(), description: inputtingDescription.value} 
    tweets.value.push(tweet)
    inputtingDescription.value = ''
}

const deleteTweet = (id: number) => {
    // 引数で受け取ったidに一致しないtweets.idをもつ要素をフィルターすることで、配列から該当idの要素を削除しているのと同じ動きになる
    tweets.value = tweets.value.filter(t => t.id !== id)
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
            <!-- tweets.lengthが0以下ならメッセージを表示 v-showでも同じことができる-->
            <p v-if="tweets.length <= 0">No tweets have been added</p>
            <!-- tweets.lengthが1以上ならリストを表示 v-elseはなくてもよいが、あったほうが明示的-->
            <ul v-else>
                <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
                    <span>{{ tweet.description }}</span>
                    <button class="delete-button" @click="deleteTweet(tweet.id)">delete</button>
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
.save-button {
    background-color: #68c9c9;
    color: #fff;
    border-radius: 2px;
    border: none;
    width: 60px;
    height: 22px;
    margin: 8px;
}

.save-button:hover {
    background-color: #37bdbd;
}
.delete-button {
    background-color: #d17959;
    color: #fff;
    border-radius: 2px;
    border: none;
    width: 60px;
    height: 22px;
    margin: 8px;
}

.delete-button:hover {
    background-color: #e45b29;
}
</style>