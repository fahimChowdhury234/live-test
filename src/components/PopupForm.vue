<!-- PopupForm.vue -->
<template>
    <div class="popup">
        <form @submit.prevent="submitForm">
            <div class="from-item">
                <label>Name:</label>
                <input type="text" v-model="editedTask.name">
            </div>
            <div class="from-item">
                <label>Time:</label>
                <input type="number" v-model.number="editedTask.time">
            </div>
            <button type="submit" class="submit">Submit</button>
            <button type="button" class="cancle" @click="closePopup">Cancel</button>
        </form>
    </div>
</template>
  
<script setup>


import { ref } from "vue";
const emit = defineEmits(["update-task", "close-popup"])
// }; 
const props = defineProps(['task', 'taskIndex'])
// const editedTask = ref(props.task)
const editedTask = ref({ ...props.task });

const submitForm = () => {
    console.log(props.taskIndex);

    emit('update-task', { task: editedTask.value, index: props.taskIndex });
};

const closePopup = () => {
    emit('close-popup');
};

</script>
  
<style scoped>
.popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: white;
    padding: 20px;
    border: 1px solid #ccc;
    width: 50%;

}

.popup form .from-item {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 10px;
}

.popup form .from-item input {
    padding: 5px 20px;
    width: 100%;
    border: 1px solid #ccc;
    outline: none;
    border-radius: 6px;
}

.popup form .submit {
    padding: 5px 10px;
    background: #1134a7;
    color: #fff;
    border-radius: 5px;
}

.cancle {
    padding: 5px 10px;
    background: #e90707;
    color: #fff;
    margin-left: 20px;
    border-radius: 5px;

}
</style>
  