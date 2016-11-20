<template>
<div id='todo'>
  <h1 v-text='msg'></h1>
  <input v-model='newItem' @keyup.enter='addNew()'/>
  <ul>
    <li v-for="item in items"  v-bind:class="{finished: item.isDone}" @click="aa(item)">
        {{item.do}}
    </li>
  </ul>
</div>
</template>

<script>
import store from '../store'
export default {
  name: 'hello',
  data () {
    return {
      msg: 'todoList',
      items: store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        store.save(items)
      },
      deep: true
    }
  },
  methods: {
    aa: function (item) {
      item.isDone = !item.isDone
    },
    addNew: function () {
      if (this.newItem !== '') {
        this.items.push({
          do: this.newItem,
          isDone: false
        })
        this.newItem = ''
      } else {
        return
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
