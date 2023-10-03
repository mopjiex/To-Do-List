<script setup>
    import { reactive, ref } from 'vue';
    import MyTask from '@/components/My-Task.vue';
    import MyTaskManager from '@/components/My-TaskManager.vue';

    const inputValue = ref('');
    const tasks = ref([]); 


    const createTask = () => {
        console.log(inputValue.value);
        tasks.value.push({
            id: Date.now(),
            title: inputValue.value,
            color: '#E63946',
            completed: false,
            isEditing: false,
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

    const updateCheckbox = (index) => {
        console.log(tasks.value[index].completed)
        if(!tasks.value[index].completed) tasks.value[index].color = '#4F9153';
        else tasks.value[index].color = '#E63946';
        
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
                    :color="tasks.color"
                    @remove="removeTask"
                    @edit="editTask"
                    @cancel="cancelTask"
                    @updateCheckbox="updateCheckbox"
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
            justify-content: space-between;
        }
    }
</style>
