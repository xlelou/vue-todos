<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>vue-todolist</title>
    <meta charset="utf-8" />
    <script src="Scripts/vue.js"></script>
</head>
<body>
<style type="text/css">
        #todolist li.finished { background-color: green; color: white; }
    </style>
<div id="todolist">
    <h2 @click="clickH2" v-bind:title="!isEditting?'点击编辑':''">
        <input v-model="user" v-show="isEditting" @keyup.enter="isEditting=false" @blur="isEditting=false" />
        <span v-show="!isEditting" @click="isEditting=true" title="点击编辑">{{user}}</span>
        <span>的todolist</span>
    </h2>
    <div>
        <button @click="addOne">添加新项目</button>
        <button @click="deleteSelectedItems">删除所选项目</button>
        <button @click="deleteAll">删除所有项目</button>
    </div>
    <ul v-for="(item, index) in list">
        <li v-bind:class="[item.finished?'finished':'']">
            <div v-show="item.isEditting">
                <input type="checkbox" v-model="item.selected" />
                <input v-model="item.content" class="content" />
                <button @click="item.isEditting=false">保存</button>
            </div>
            <div v-show="!item.isEditting">
                <input type="checkbox" v-model="item.selected" />
                <span>{{item.content}}</span>
                <button v-if="!item.finished" @click="item.finished=true">标记为已完成</button>
                <button v-if="item.finished" @click="item.finished=false">标记为未完成</button>
                <button @click="editItem(index)">编辑</button>
            </div>
        </li>
    </ul>
</div>
<script>
        new Vue({
            el: '#todolist',
            data: function () {
                var user = localStorage.getItem('todolist_user') || ''
                var list = []
                var listStr = localStorage.getItem('todolist_list')
                if (listStr) {
                    list = JSON.parse(listStr)
                }
                return {
                    isEditting: false,
                    user: user,
                    list: list
                }
            },
            watch: {
                user: function (val, oldVal) {
                    localStorage.setItem('todolist_user', val)
                },
                list: {
                    handler: function (val, oldVal) {
                        var str = JSON.stringify(val)
                        localStorage.setItem('todolist_list', str)
                    },
                    deep: true
                }
            },
            methods: {
                clickH2: function () {
                    if (!this.user) {
                        this.isEditting = true
                    }
                },
                addOne: function () {
                    var item = {
                        title: '',
                        finished: false,
                        selected: false,
                        isEditting: true
                    }
                    this.list.push(item)
                    var vm = this
                    Vue.nextTick(function () {
                        vm.$el.querySelectorAll('li')[vm.list.length - 1].querySelector('.content').focus()
                    })
                },
                editItem: function (index) {
                    this.list[index].isEditting = true
                    var vm = this
                    Vue.nextTick(function () {
                        vm.$el.querySelectorAll('li')[index].querySelector('.content').focus()
                    })
                },
                deleteSelectedItems: function () {
                    this.list = this.list.filter(function (item) {
                        return !item.selected
                    })
                },
                deleteAll: function () {
                    this.list = []
                }
            }
        })
    </script>
</body>
</html>
