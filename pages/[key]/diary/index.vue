<template>
    <div class="card-wrapper">
      <div style="display: flex; gap: 1rem; width: 100%;">
          <div class="nav-item"><a :href="`/${route.params.key}/diary`">일기장</a></div>
          <div class="nav-item"><a :href="`/${route.params.key}/`">메모장</a></div>
      </div>
        <h1 style="text-align: center;">일기 랜덤박스</h1>
        <div style="text-align: center;"><span @click="pickRandom" class="button">랜덤 뽑기</span></div>
        <h2 style="text-align: center;">최근 30일간</h2>
        <div class="card card-main">
            <div style="text-align: center;"><span >{{ result[result.length-1][1] }} ({{ result[result.length-1][2] }}) - {{ result[0][1] }} ({{ result[0][2] }})</span></div>
            <div style="text-align: center; font-size: 1.7rem;"><span>평점: {{ rate }}점</span></div>
            <div style="text-align: center; font-size: 2rem;"><span v-for="star of Math.round(rate)">🌟</span></div>
            <div style="display: flex; gap: 1px; align-items: flex-end; flex-direction: row-reverse;">
                <div v-for="row of result" :style="`flex-grow: 1; height: calc( 100px * ${parseInt(row[3])} / ${Math.max(...rateToday)}); background: #ff9899; color: white; overflow: hidden;`">
                </div>
            </div>
            <div style="text-align: center;">(+)</div>
            <div v-for="reason of goodDayPicked" class="textbox">
                <div>{{ reason[4] }} - {{ reason[1] }} <span v-for="star of parseInt(reason[3])">🌟</span></div>
            </div>
            <div style="text-align: center;">(-)</div>
            <div v-for="reason of badDayPicked" class="textbox">
                <div>{{ reason[4] }} - {{ reason[1] }} <span v-for="star of parseInt(reason[3])">🌟</span></div>
            </div>
        </div>
        <h2 style="text-align: center;">건강 상태</h2>
        <div class="card center card-main">
            <div style="font-size: 1.7rem;">약 복용</div>
            <div>이 기간 동안...</div>
            <div style="font-size: 2rem;">총 {{medicine[0]}} 회</div>
            <div>아침 약</div>
            <div><span class="tag">콘서타OROS서방정 36mg</span></div>
            <div style="font-size: 2rem;">{{medicine[1]}} 회</div>
            <div style="font-size: 2rem;"><span v-for="pills of medicine[1]">💊</span></div>
            <div>점심 약</div>
            <div><span class="tag">메디키넷리타드캡슐 10mg</span></div>
            <div style="font-size: 2rem;">{{medicine[2]}} 회</div>
            <div style="font-size: 2rem;"><span v-for="pills of medicine[2]">💊</span></div>
            <div>저녁 약</div>
            <div><span class="tag">파록스씨알정 25mg</span></div>
            <div style="font-size: 2rem;">{{medicine[3]}} 회</div>
            <div style="font-size: 2rem;"><span v-for="pills of medicine[3]">💊</span></div>
            <div style="font-family: 'Cafe24Lovingu'; font-size: 2rem; margin-top: 20px;">🩺 Mental Issues 🩺</div>
            <div v-for="reason of result.filter((re)=> re[8])" class="textbox">
                <div>{{ reason[8] }} - <span>{{reason[1]}}</span></div>
            </div>
            <div style="font-family: 'Cafe24Lovingu'; font-size: 2rem; margin-top: 20px;">🩺 Physical Issues 🩺</div>
            <div v-for="reason of result.filter((re)=> re[9])" class="textbox">
                <div>{{ reason[9] }} - <span>{{reason[1]}}</span></div>
            </div>
        </div> 
        <h2 style="text-align: center;">랜덤 업무 내역</h2>
        <div class="card center card-main">
            <div v-for="row of dayPicked" class="textbox">
                <div>{{ row[11] }} - {{ row[1] }}</div>
            </div>
        </div>
        <h2 style="text-align: center;">미래를 위한 랜덤 계획</h2>
        <div class="card center card-main">
            <div v-for="row of dayPicked" class="textbox">
                <div>{{ row[12] }} - {{ row[1] }}</div>
            </div>
        </div>
        <h2 style="text-align: center;">소비 상태</h2>
        <div class="card center card-main">
            <div>최대 {{ Math.max(...moneyLeft) }} 원</div>
            <div style="display: flex; gap: 1px; align-items: flex-end; flex-direction: row-reverse;">
                <div v-for="row of result" :style="`flex-grow: 1; height: calc( 400px * ${row[15]} / ${Math.max(...moneyLeft)}); background: #ff9899; color: white;`">
                </div>
            </div>
            <div>0</div>
            <div v-for="row of feedDayPicked" class="textbox">
                <div>{{ row[17] }} - {{ row[1] }}</div>
            </div>
        </div>
    </div>
</template>
<script setup>
const route = useRoute()

const sheet = await $fetch('https://sheets.googleapis.com/v4/spreadsheets/1QGkH5j3ZNo3ms7YGFdYTeW2mEoWwxcnMy8bbEXgbVa0/values/diary!A2:R?key='+route.params.key)
const values = await sheet.values
const result = await values.reverse().slice(0, 30)
const resultReverse = [...result].reverse()

let rate = 0
let rateToday = []
let medicine = [0, 0, 0, 0]
let moneyLeft = []

for await(let row of result) {
    rate = rate + parseInt(row[3])
    rateToday.push(parseInt(row[3]))
    medicine[0] = medicine[0] + row[6].split(',').length
    medicine[1] = medicine[1] + row[6].split('아침').length - 1
    medicine[2] = medicine[2] + row[6].split('점심').length - 1
    medicine[3] = medicine[3] + row[6].split('저녁').length - 1
    moneyLeft.push(parseInt(row[15]))
}

rate = rate / result.length

let goodDay = result.filter((re)=> re[3] >= 3)
let goodDayPicked = []
for (let i=0; i<3; i++) {
    if (goodDay.length > 0 ) {
        let randomDay = Math.floor(Math.random()*goodDay.length)
        goodDayPicked.push(goodDay[randomDay])
        goodDay = goodDay.filter((day, index)=>index != randomDay)
    }
}
console.log(goodDayPicked)
let badDay = result.filter((re)=>re[3] < 3)
let badDayPicked = []
for (let i=0; i<3; i++) {
    if (badDay.length > 0) {
        let randomDay = Math.floor(Math.random()*badDay.length)
        badDayPicked.push(badDay[randomDay])
        badDay = badDay.filter((day, index)=>index != randomDay)
    }
}

let feedDay = result.filter((re) => re.length == 18)
let feedDayPicked = []
for (let i=0; i<5; i++) {
    if (feedDay.length > 0) {
        let randomDay = Math.floor(Math.random()*feedDay.length)
        feedDayPicked.push(feedDay[randomDay])
        feedDay = feedDay.filter((day, index)=>index != randomDay)
    }
}

let day = [...result]
let dayPicked = []
for (let i=0; i<5; i++) {
    if (day.length > 0) {
        let randomDay = Math.floor(Math.random()*day.length)
        dayPicked.push(day[randomDay])
        day = day.filter((d, index)=>index != randomDay)
    }
}

function pickRandom() {
    location.href = location.href
}

</script>