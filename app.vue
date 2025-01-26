<template>
  <div id="app">
    <div id="wrapper">
      <h1 style="text-align: center;">아이디어 랜덤박스</h1>
      <NuxtPage />
    </div>
  </div>
</template>
<style lang="css">

:root {
  --fg: #121212;
}

@font-face {
    font-family: 'GangwonEduSaeeum_OTFMediumA';
    src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/noonfonts_2201-2@1.0/GangwonEduSaeeum_OTFMediumA.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}

@font-face {
    font-family: 'Cafe24Lovingu';
    src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/2405-3@1.1/Cafe24Lovingu.woff2') format('woff2');
    font-weight: normal;
    font-style: normal;
}

body{
  background-color: #fffcf8;
  background-image:  linear-gradient(#ff989944 1px, transparent 1px), linear-gradient(to right, #ff989944 1px, #fffcf8 1px);
  background-size: 20px 20px;
  font-family: 'GangwonEduSaeeum_OTFMediumA';
  font-size: 20px;
  color: var(--fg);
  line-height: 1.2;
}

.nav-item {
  background-color: #ff9899; color: white; flex-grow: 1; text-align: center; padding: 1.4rem 0; border-radius: 10px;
}

.nav-item a {
  text-decoration: none;
  color: inherit;
}

#app{
  width: 100%;
  margin: 0;
  padding: 0;
}

#wrapper{
  width: 100%;
  max-width: 800px;
  margin: 2rem auto;
}

.card-wrapper {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.card {
  padding: 2rem;
  border-radius: 2rem;
  background: #ffffff99;
  color: gray;
  border: #ff989966 2px dotted;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.card-main {
  font-size: 1.2em;
  color: var(--fg);
}

.center > * {
  text-align: center;
}

.timestamp {
  font-size: 0.8em;
}

.category, .button, .tag {
  background: #ff9899;
  color: white;
  border-radius: 5px;
  padding: 3px;
}

.textbox {
  border-radius: 1rem;
  background: #eeeeee;
  padding: 20px;
  text-align: left;
}

</style>