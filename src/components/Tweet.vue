<script setup lang="ts">
import { ref } from 'vue'
import TweetPostForm from './TweetPostForm.vue';
import TweetList from './TweetList.vue';

const tweets = ref([{ id: 0, description: 'hello world' }, { id: 1, description: 'this is second tweet' }])

const inputtingDescription = ref<string>('')
const postTweet = () => {
    const tweet = { id: Math.random(), description: inputtingDescription.value }
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
        <TweetPostForm />
        <div class="tweet-container">
            <!-- tweets.lengthが0以下ならメッセージを表示 v-showでも同じことができる-->
            <p v-if="tweets.length <= 0">No tweets have been added</p>
            <!-- tweets.lengthが1以上ならリストを表示 v-elseはなくてもよいが、あったほうが明示的-->
            <ul v-else>
                <!-- 親コンポーネントTweetが持っているtweetsを子コンポーネントTweetListに渡す -->
                <TweetList :tweets="tweets" />
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

</style>