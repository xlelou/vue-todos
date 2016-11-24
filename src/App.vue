<template>
  <div id="app">
    <div class='logo'>
        <img src="./assets/logo.jpg">
    </div>
    <todo></todo>
  </div>
</template>

<script>
import todo from './components/Hello'
export default {
  name: 'app',
  components: {
    todo
  }
}
</script>
<style src='./assets/css/app.css'></style>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.logo{
    width:140px;
    height:140px;
    border-radius:50%;
    overflow:hidden;
    margin:0 auto;
    margin-bottom: 20px;
    transition:all ease-in 1s;
     animation: disRound 1s backwards;
}
.logo:hover{
  animation: round 1s forwards;
}
img{
  width:100%;
  height:100%;
}
@keyframes round{
  from {
    width:140px;
    height:140px;
    transform:rotate(0deg);
  }
  to{
   width:240px;
    height:240px;
    transform:rotate(360deg);
  }
}
@keyframes disRound{
  from {
    width:240px;
    height:240px;
    transform:rotate(360deg);
  }
  to{
   width:140px;
    height:140px;
    transform:rotate(0deg);
  }
}
</style>
