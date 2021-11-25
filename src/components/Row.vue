<template>
    <div class="row" style="margin-top: 12px">
        <div class="col-3">
            <CardTask CardTitle="Todo" 
                :Data="todoTask"
                StatusCard="Todo"
                @dropCard="onDrop"
                @dragCard="dragStart"
                @showCard="showCard" />
        </div>
        <div class="col-3">
            <CardTask CardTitle="Development" 
                :Data="developmentTask"
                StatusCard="Development"
                @dropCard="onDrop"
                @dragCard="dragStart"
                @showCard="showCard" />
        </div>
        <div class="col-3">
            <CardTask CardTitle="Review" 
                :Data="reviewTask"
                StatusCard="Review"
                @dropCard="onDrop"
                @dragCard="dragStart"
                @showCard="showCard" />
        </div>
        <div class="col-3">
            <CardTask CardTitle="Done" 
                :Data="doneTask"
                StatusCard="Done"
                @dropCard="onDrop"
                @dragCard="dragStart"
                @showCard="showCard" />
        </div>
    </div>
</template>

<script>
import CardTask from './CardTask.vue';

export default {
    name: "Row",
    components: {
        CardTask
    },
    props: {
        dataTask: {
            type: Array,
        },
    },
    data() {
        return {
            taskBool: false,
        }
    },
    computed: {
        todoTask() {
            return this.dataTask.filter(task => task.status === "Todo")
        },
        developmentTask() {
            return this.dataTask.filter(task => task.status === "Development")
        },
        reviewTask() {
            return this.dataTask.filter(task => task.status === "Review")
        },
        doneTask() {
            return this.dataTask.filter(task => task.status === "Done")
        }
    },
    methods: {
        showCard(val) {
            this.taskBool = !this.taskBool
            this.$emit('showDataCard', val)
        },
        dragStart(evt, val) {
            evt.dataTransfer.dropEffect = "move"
            evt.dataTransfer.effectAllowed = "move"
            evt.dataTransfer.setData("item-todo", val.id)
        },
        onDrop(evt, status) {
            // const dataTask = this.dataTask
            const taskId = evt.dataTransfer.getData("item-todo")
            const task = this.dataTask.find(task => task.id == taskId)
            // const taskIndex = this.dataTask.findIndex(taskIndex => taskIndex.id == task.id)
            task.status = status
        }
    },
}
</script>