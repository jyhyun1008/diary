<template>
    <div class="card-wrapper">
        <div style="text-align: center;"><span @click="pickRandom" class="button">랜덤 아이디어</span></div>
        <div class="card" id="card-main">
            <div ><span class="category" v-text="result[randomnumber][1]"></span></div>
            <div v-text="result[randomnumber][2]"></div>
            <div v-text="result[randomnumber][0]" class="timestamp"></div>
        </div> 
        <h3 style="text-align: center;">최신 메모들</h3>
        <div v-for="row of result" class="card">
            <div><span class="category">{{ row[1] }}</span></div>
            <div>{{ row[2] }}</div>
            <div class="timestamp">{{ row[0] }}</div>
        </div>
    </div>
</template>
<script setup>

const route = useRoute()

const sheet = await $fetch('https://sheets.googleapis.com/v4/spreadsheets/1QGkH5j3ZNo3ms7YGFdYTeW2mEoWwxcnMy8bbEXgbVa0/values/notepad!A2:C?key='+route.params.key)
const result = await sheet.values.reverse()
let randomnumber = Math.floor(Math.random() * result.length)

function pickRandom() {
    location.href = location.href
}

</script>