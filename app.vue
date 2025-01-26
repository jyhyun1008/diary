<template>
  <div id="app">
    <div id="wrapper">
      <h1 style="text-align: center;">메모장</h1>
      <NuxtPage />
    </div>
  </div>
</template>
<style lang="css">

:root {
  --fg: #121212;
}

@font-face {
    font-family: 'ONE-Mobile-POP';
    src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/noonfonts_2105_2@1.0/ONE-Mobile-POP.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}

body{
  background-color: #fffcf8;
  background-image:  linear-gradient(#ff989944 1px, transparent 1px), linear-gradient(to right, #ff989944 1px, #fffcf8 1px);
  background-size: 20px 20px;
  font-family: 'ONE-Mobile-POP';
  color: var(--fg);
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

#card-main {
  font-size: 1.2em;
  color: var(--fg);
}

.timestamp {
  font-size: 0.8em;
}

.category, .button {
  background: #ff9899;
  color: white;
  border-radius: 5px;
  padding: 3px;
}

</style>