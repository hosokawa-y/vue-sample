<script setup lang="ts">
import { ref, reactive } from 'vue'

// itemName1の値が変わったらtemplateを読みなおしてほしいのでrefを使う
const itemName1 = ref<string>('Desk')
const itemName2 = 'bike'

//  オブジェクトそのものをリアクティブにしたい場合はreactive
const item1 = reactive({
    name: 'sofa',
    price: 40000
})
const price2 = 800
const url1 = "https://www.amazon.co.jp/【国内正規品-メーカー保証1年】FELLOW-Stagg-温度調整機能付き電気ケトル-【PSE認証済】/dp/B09MKFCKYY"

const buy = (itemName: string) => {
    alert('Are you sure to buy ' + itemName + '?')
}

const input = (event: any) => {
    // itemName1.value = event.target.value
    item1.name = event.target.value
}

const inputPrice = (event: any) => {
    item1.price = event.target.value
}
</script>

<template>
    <div class="container">
        <label>Payment.js</label>
        <input v-on:input="input" />
        <input v-on:input="inputPrice" />
        <h1>最近の支出</h1>
        <div class="payment">
            <label>{{ item1.name }}</label>
            <label>{{ item1.price }}円</label>
            <!-- v-bind  でscript内に書かれた変数を呼び出す-->
            <a v-bind:href="url1">bought at...</a>
            <!-- v-on  でscript内に書かれた関数を呼び出す-->
            <button v-on:click="buy(item1.name)">BUY</button>
        </div>
        <div class="payment">
            <label>{{ itemName2 }}</label>
            <label>{{ price2 }}円</label>
        </div>
        <div class="payment">
            <label>そば</label>
            <label>800円</label>
        </div>

    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.payment {
    display: flex;
    justify-content: space-between;
    height: 80px;
    width: 800px;
    align-items: center;
    background-color: aliceblue;
    margin-bottom: 8px;
}

input {
    margin-bottom: 8px;
    height: 30px;
    width: 300px;
}

label {
    font-size: 20px;
    font-weight: bold;
}
</style>