<script setup lang="ts">
import { defineProps } from 'vue';

type Tweet = {
    id: number,
    description: string,
}
// 親コンポーネントから子コンポーネントに値を渡したいときはpropsをつかう
type Props = {
    tweets: Tweet[]
}
const deleteTweet = (id: number ) => {}

// definePropsでPropsを使える
// 子コンポーネントは受けとったpropsを画面に表示するだけにしておくべき。何らかの処理を加えるべきじゃない。
defineProps<Props>()

</script>

<template>
    <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
        <span>{{ tweet.description }}</span>
        <button class="delete-button" @click="deleteTweet(tweet.id)">delete</button>
    </li>
</template>

<style scoped>
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