<!-- ParentComponent.vue -->
<template>
    <div class="mainDivWrapper">
        <div v-for="(task, index) in tasks" :key="index" class="mainDiv">
            <p>Name: {{ task.name }} - Time: {{ task.time }}</p>
            <button @click="editTask(index)">Edit</button>
        </div>
        <PopupForm v-if="showPopup" :task="selectedTask" @update-task="updateTask" @close-popup="closePopup"
            :taskIndex="selectedTaskIndex" />
    </div>
</template>
  
<script setup>
import { ref } from 'vue';
import PopupForm from './PopupForm.vue';
const tasks = ref([
    { name: 'Task 1', time: 30 },
    { name: 'Task 2', time: 40 },
    { name: 'Task 3', time: 60 },
    { name: 'Task 4', time: 45 },
    { name: 'Task 5', time: 50 }
]);

const showPopup = ref(false);
const selectedTask = ref(null);
const selectedTaskIndex = ref(null);


const editTask = (index) => {
    console.log(index);
    selectedTask.value = { ...tasks.value[index] };
    selectedTaskIndex.value = index;
    showPopup.value = true;
};

const updateTask = (updatedTask) => {
    console.log(updatedTask);
    tasks.value = tasks.value.map((task, index) => {
        if (index === updatedTask.index) {
            return { ...updatedTask.task };
        }
        return task;
    });
    closePopup();
};

const closePopup = () => {
    showPopup.value = false;
    selectedTask.value = null;
};

</script>
<style scoped>
.mainDivWrapper {
    padding: 40px;
}

.mainDiv {
    width: 400px;
    background: #eee;
    padding: 20px;
    border-radius: 6px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px !important;

    margin: 0 auto;
}
</style>