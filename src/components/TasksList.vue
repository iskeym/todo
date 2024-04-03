<template>
    <div class="tasks" v-show="tasks.length > 0">
        <transition-group name="tasks">
            <task-item v-for="task in tasks" :task="task.text" :done="task.done" @remove="$emit('remove', task)" @changeDone="changeDone"/>
        </transition-group>
    </div>
    <h2 v-show="tasks.length == 0">задач нет</h2>
</template>

<script>
import TaskItem from '@/components/TaskItem.vue'

export default {
    components: {
        TaskItem
    },
    props: {
        tasks: {
            type: Array,
            required: true
        }
    },
    methods: {
        changeDone(check) {
        }
    },
}
</script>

<style lang="scss" scoped>
.tasks{
  display: flex;
  flex-direction: column;
}
h2{
    margin: 0 auto;
    margin-top: 50px;
    font-size: 30px;
    border-bottom: 3px solid black;
}
.tasks-enter-active,
.tasks-leave-active {
  transition: all 0.3s ease;
}
.tasks-enter-from,
.tasks-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>