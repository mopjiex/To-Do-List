<script setup>
    import { reactive, ref } from 'vue';
    import MyTask from '@/components/My-Task.vue';
    import MyTaskManager from '@/components/My-TaskManager.vue';

    const inputValue = ref('');
    const editInputValue = ref('');
    const tasks = ref([]); 


    const createTask = () => {
        tasks.value.push({
            id: Date.now(),
            title: inputValue.value,
            completed: false,
            isEditing: false,
            decoration: {textDecoration: 'none'},
        });
    }

    const removeTask = (index) => {
        tasks.value.splice(index, 1);
    }

    const editTask = (index) => {
        tasks.value[index].isEditing = true;
    }

    const cancelTask = (index) => {
        tasks.value[index].isEditing = false;
    }

    const saveTask = (index) => {
        tasks.value[index].title = editInputValue.value;
        tasks.value[index].isEditing = false;  
    }

    const updateCheckbox = (index) => {
        if(!tasks.value[index].completed) tasks.value[index].decoration = {textDecoration: 'line-through'};
        else tasks.value[index].decoration = {textDecoration: 'none'}; 
    }

</script>

<template>
    <div class="app">
        <div class="container">
            <div class="app__inner">
                <MyTask
                    inputPlaceholder="Введите задачу"
                    v-model="inputValue"  
                    @submit="createTask"   
                />

                <MyTaskManager
                    :tasks="tasks"
                    @remove="removeTask"
                    @edit="editTask"
                    @cancel="cancelTask"
                    @save="saveTask"
                    @updateCheckbox="updateCheckbox"
                    v-model="editInputValue"
                    
                />
            
            </div>
        </div>
    </div>
</template>

<style lang="scss">
    @import url('https://fonts.googleapis.com/css2?family=Russo+One&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Raleway&display=swap');

    
    .title {
        font-family: 'Russo One', sans-serif;
        font-size: 26px;
        text-align: center;
    }

    .app {
        font-family: 'Raleway', sans-serif;
        padding: 40px 0;
        min-height: 100vh;
        background: url(/BG.jpg) center/cover no-repeat;
        &__inner {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 1000px;
            margin: 0 auto;
            gap: 20px 0;
        }
    }
</style>
