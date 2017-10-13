<template>
    <li v-for="task, index in tasks" :class="{ 'completed-task': task.completed}" class="list-group-item pointer">
        <span @click="toggleTask(index)">
            {{ task.completed ? '✓' : '▢' }} {{ task.description }} - {{ task.created_at | formatDate }}
        </span>
        <button @click="removeTask()">×</button>
    </li>
</template>

<script>
    import moment from "moment";
    export default {
        name: "TaskItem",
        props: {
            task: {
                type: Array,
                required: true
            },
            index: {
                type: Number,
                required: true
            }
        },
        data() {
            return {

            }
        },
        filters: {
            formatDate(date) {
                return moment(date).format("DD MMM YYYY [at] hh:mm:ss a");
            }
        },
        methods: {
            removeTask() {
                this.$emit("remove-task", this.index);
            }
        }
    }
</script>