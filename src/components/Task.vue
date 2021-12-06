<template>
    <div @click="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
        <h3>{{ task.text }}
          <font-awesome-icon id="delete-icon" @click="$emit('delete-task', task.id)" :icon="['fas', 'times']" />
        </h3>
        <p>{{ task.day }} at {{ task.time }}</p>
    </div>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object
    },
    methods: {
    }
}
</script>

<style scoped>
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
#delete-icon {
  color: red;
}
</style>