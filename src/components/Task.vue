<script>
export default {
    data() {
        return {
            isReduct: false,
            newText: '',
            reductButtonText: 'Редактировать',
        }
    },
    props: {
        text: String,
        done: Boolean,
        id: Number,
    },
    emits: [
        'changeDone',
        'removeTask',
        'changeTask'
    ],
    methods: {
        doneTask() {
            this.$emit('changeDone', this.id);
        },
        reductTask() {
            this.isReduct = !this.isReduct;
            this.$emit('changeTask', this.id, this.newText);
            this.reductButtonText = this.reductButtonText == 'Редактировать' ?
             'Закончить редактирование' :
             'Редактировать';
            this.newText = '';
        }
    },
    computed: {
        myStyle() {
            return {
                done: this.done
            };
        }
    }
}
</script>
    
<template>
    <div class="task">
        <input type="checkbox" @click="doneTask">
        <p :class="myStyle" v-if="!isReduct">{{ text }}</p>
        <input type="text" v-if="isReduct" v-model="newText">
        <button @click="reductTask()">{{ reductButtonText }}</button>
        <button @click="this.$emit('removeTask', this.id)">удалить</button>
    </div>
</template>

<style>
p {
    display: inline-block;
    padding: 5px;
}
div.task {
    border: 1px solid blue;
    margin: 5px 0px;
    padding: 5px;
}

p.done {
    text-decoration: line-through;
}
</style>