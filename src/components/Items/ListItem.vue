<template>
    <div class="task_container">
        <h2 class="task_header" @click="(event) => this.$emit('editTask', event)">{{ taskInfo.name }}</h2>
        <button class="task_btn task_btn-done" @click="(event) => this.$emit('taskDone', event)">
            <check-mark class="task_icon" />
        </button>
        <button class="task_btn task_btn-delete" @click="(event) => this.$emit('deleteTask', event)">
            <trash-can class="task_icon" />
        </button>
    </div>
</template>

<script>
import CheckMark from '../Icons/IconCheckMark.vue'
import TrashCan from '../Icons/IconTrashCan.vue'

export default {
    components: {
        CheckMark,
        TrashCan,
    },
    props: {
        taskInfo: {
            type: Object,
            default() {
                return {}
            },
        },
    },
}
</script>

<style scoped>
.task_container {
    background: #ffffff;
    min-height: 65px;
    margin: 1rem 0;
    text-align: start;
    display: flex;
    border-radius: 0.5rem;
}
.task_container:last-child {
    margin-bottom: 0;
}
.task_header {
    max-width: 300px;
    padding: 1rem 0.5rem 1rem 1rem;
    vertical-align: middle;
    cursor: pointer;
    word-break: break-word;
}
.task_btn {
    width: 20%;
    min-width: 70px;
    border: none;
}
.task_btn-done {
    margin-left: auto;
    background-color: #04c1a3;
}
.task_btn-delete {
    background-color: #fb7b3f;
    border-radius: 0 0.5rem 0.5rem 0;
}
.task_icon {
    width: 24px;
    fill: #ffffff;
}
.task_done {
  opacity: 0.6;
  transition: opacity 0.1s linear;
}
</style>