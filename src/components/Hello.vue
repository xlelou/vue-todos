<template>
<div id='todo'>
  <h1 v-text='msg'></h1>
  <ul>
    <li v-for="item in items"  v-bind:class="{finished: item.isDone}" v-on:click="aa(item)">
        {{item.id + " " +item.do}}
    </li>
  </ul>
</div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'todoList',
      items: [
        {
          id: 1,
          do: 'eat',
          isDone: true
        },
        {
          id: 2,
          do: 'sleep',
          isDone: false
        }
      ],
      methods: {
        aa: function (item) {
          console.log(item)
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

.finished{
  color:red;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
