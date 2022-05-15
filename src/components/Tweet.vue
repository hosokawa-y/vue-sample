<script setup lang="ts">
import { ref } from 'vue'
import TweetPostForm from './TweetPostForm.vue';
import TweetList from './TweetList.vue';

const tweets = ref([{ id: 0, description: 'hello world' }, { id: 1, description: 'this is second tweet' }])

const inputtingDescription = ref<string>('')
const postTweet = (description: string) => {
    const tweet = { id: Math.random(), description}
    tweets.value.push(tweet)
}

const deleteTweet = (id: number) => {
    // 引数で受け取ったidに一致しないtweets.idをもつ要素をフィルターすることで、配列から該当idの要素を削除しているのと同じ動きになる
    tweets.value = tweets.value.filter(t => t.id !== id)
}

</script>

<template>
    <div class="container">
        <h1>Tweeter</h1>
        <!-- TweetPostFormから受け取ったpost-tweet（実際の値はinputtingDescription.value）をpostTweet関数に渡している -->
        <TweetPostForm @post-tweet="postTweet"/>
        <div class="tweet-container">
            <!-- tweets.lengthが0以下ならメッセージを表示 v-showでも同じことができる-->
            <p v-if="tweets.length <= 0">No tweets have been added</p>
            <!-- tweets.lengthが1以上ならリストを表示 v-elseはなくてもよいが、あったほうが明示的-->
            <ul v-else>
                <!-- 親コンポーネントTweetが持っているtweetsを子コンポーネントTweetListに渡す -->
                <!-- TweetListから受け取ったdelete-tweet(実際の値はid)をdeleteTweetにわたす -->
                <TweetList :tweets="tweets" @delete-tweet="deleteTweet"/>
                <!-- emitを使わずに子から親にイベントを渡す方法 -->
                <!-- :delete-tweetはTweetListで定義したPropsのdeleteTweetのこと。ケバブ記法で書き換えただけ。 -->
                <!-- TweetListでPropsで渡ってきたdeleteTweetはTweet.vueのdeleteTweetのことなので削除ボタンが押されたらdeleteTweetが呼ばれる -->
                <!-- <TweetList :tweets="tweets" :delete-tweet="deleteTweet"/> -->
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