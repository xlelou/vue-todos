<template>
<div id='todo'>
  <h1 v-text='msg'></h1>
    <div class="form-group row m-t-20 input-mission">
        <label for="addnew" class="col-xs-2 col-form-label">输入任务：</label>
        <div class="col-xs-10">
            <input v-model.trim='newItem' id='addnew' @keyup.enter='addNew()' class="form-control" type="text" placeholder="Input Mission">
        </div>
    </div>
  <table class="table table-bordered" >
    <thead>
        <tr>
          <!--<th>Id</th>-->
          <th>Do(click to edit)</th>
          <th>Begin-time</th>
            <th>End-time</th>
          <th>Operate</th>
        </tr>
    </thead>
    <tbody v-for="(item, index) in items">
        <tr>
          <!--<td>{{ item.id }}</td>-->
          <!--<td v-bind:class="{finished: item.isDone}">{{ item.do }}</td>-->
          <td class='item'>
              <div v-show="!item.isEdit" >
                  <p @click="editItem(item)" :class="[{finished : item.isFinished}]">{{ item.todo }}</p>
              </div>
              <div class="form-group row" v-show="item.isEdit">
                  <div>
                      <input class="form-control" type="text":id='item.id' v-model="item.todo" @keyup.enter="doneEdit(item)"  @blur="doneEdit(item)" lazy >
                  </div>
              </div>
          </td>
          <td class="time">
              <p>{{ item.b_time }}</p>
          </td>
            <td class="time">
                <p v-show="!item.isFinished">未完成</p>
                <p v-show="item.isFinished">{{ item.e_time }}</p>
            </td>
          <td class="opera">
            <button v-show='!item.isFinished' class="btn btn-outline-primary" @click="doneItem(item)">完成</button>
            <button class="btn btn-outline-danger" @click="remove(item)">删除</button>
          </td>
        </tr>
    </tbody>
  </table>
    <!--<p v-for="(item, index) in items">已完成0项 未完成10项 一共0项</p>-->
</div>
</template>
<style>

</style>
<script>
import store from '../store'
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Mission List',
      items: store.fetch(),
      newItem: '',
      done: ''
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
    doneItem: function (item) {
      var myDate = new Date()
      myDate.getYear()       // 获取当前年份(2位)
      myDate.getFullYear()    // 获取完整的年份(4位,1970-????)
      myDate.getMonth()       // 获取当前月份(0-11,0代表1月)
      myDate.getDate()        // 获取当前日(1-31)
      myDate.getDay()         // 获取当前星期X(0-6,0代表星期天)
      myDate.getTime()        // 获取当前时间(从1970.1.1开始的毫秒数)
      myDate.getHours()      // 获取当前小时数(0-23)
      myDate.getMinutes()     // 获取当前分钟数(0-59)
      myDate.getSeconds()     // 获取当前秒数(0-59)
      myDate.getMilliseconds()    // 获取当前毫秒数(0-999)
      myDate.toLocaleDateString()     // 获取当前日期
      item.isDone = !item.isDone
      item.done = '已完成'
      item.isFinished = !item.isFinished
      item.e_time = myDate.toLocaleString()
    },
    addNew: function () {
      var myDate = new Date()
      myDate.getYear()       // 获取当前年份(2位)
      myDate.getFullYear()    // 获取完整的年份(4位,1970-????)
      myDate.getMonth()       // 获取当前月份(0-11,0代表1月)
      myDate.getDate()        // 获取当前日(1-31)
      myDate.getDay()         // 获取当前星期X(0-6,0代表星期天)
      myDate.getTime()        // 获取当前时间(从1970.1.1开始的毫秒数)
      myDate.getHours()      // 获取当前小时数(0-23)
      myDate.getMinutes()     // 获取当前分钟数(0-59)
      myDate.getSeconds()     // 获取当前秒数(0-59)
      myDate.getMilliseconds()    // 获取当前毫秒数(0-999)
      myDate.toLocaleDateString()     // 获取当前日期
      // var mytime=myDate.toLocaleTimeString()     // 获取当前时间
      // myDate.toLocaleString()        // 获取日期与时间
      if (this.newItem !== '') {
        this.items.push({
          todo: this.newItem,
          done: '未完成',
          isDone: false,
          id: this.items.length + 1,
          isEdit: false,
          isFinished: false,
          b_time: myDate.toLocaleString(),
          e_time: ''
        })
        this.newItem = ''
      } else {
        return
      }
    },
    editItem: function (item) {
      if (item.isFinished) {
        return
      }
      item.isEdit = true
      setTimeout(function () {
        document.getElementById(item.id).focus()
      }, 400)
    },
    doneEdit: function (item) {
      if (!this.editItem) {
        return
      }
      setTimeout(function () {
        item.isEdit = false
      }, 400)
    },
    remove: function (item) {
      this.items.splice(this.items.indexOf(item), 1)
    },
    completed: function (item) {

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
 .time{min-width:200px}
 .item{
    min-width:200px
 }
 .opera{
    min-width:150px
 }
 th{
    text-align:center;
 }
 td{
    vertical-align: middle;
 }
 p{
    margin-bottom:0px;
 }
 .input-mission{
    margin:20px auto;
    width:800px;
 }
 .m-t-20{
    margin-bottom:20px;
 }
</style>
