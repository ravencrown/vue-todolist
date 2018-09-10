<template>
    <div>
        <Title :title="title" :subtitle="subtitle"></Title>
        <div>
            <input @keyup.enter="handleClick" type="text" v-model="mytodo">
            <button @click="handleClick">添加</button>
            <button @click="clean">清空</button>
        </div>
        <ul>
            <li :class="{'done':todo.status}"  @click="toggle(index)" v-for='(todo, index) in todos'>{{ index }} : {{ todo.text }}</li>
        </ul>
        <p>{{ remains }}/{{ todos.length }}</p>
    </div>
</template>

<script>
import Title from './components/Title'
export default {
    components: {
        Title
    },
    data() {
        return {
            title: 'hello vuejs',
            subtitle: 'vue react angular is good',
            showSub: false,
            mytodo: '',
            todos: [{
                text: '吃饭',
                status: false
            },
            {
                text: '睡觉',
                status: false
            },
            {
                text: '打豆豆',
                status: false
            }]
        }
    },

    computed:{
        remains() {
            return this.todos.filter(v=>!v.status).length
        }
    },
    methods: {
        handleClick() {
            this.todos.push({
                text: this.mytodo,
                status: false
            });
            this.mytodo = '';
            // this.todos.push('')
            // this.title = 'hello mini cooper'
        },
        toggle(index) {
            this.todos[index].status = !this.todos[index].status
        },
        clean() {
            this.todos = this.todos.filter(v=>!v.status)
        }
    }
}    
</script>

<style>
li.done{
    text-decoration: line-through;
    color:red
}
</style>
