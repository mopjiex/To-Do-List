<script setup>
    import { computed, ref } from 'vue';
    import MyTask from '@/components/My-Task.vue';
    import MyFilter from '@/components/My-Filter.vue';
    import MyTaskManager from '@/components/My-TaskManager.vue';

    const date = new Date();
    const inputValue = ref('');
    const editInputValue = ref('');
    const tasks = ref([]); 
    const selectedOption = ref('Все');

    const createTask = () => {
        tasks.value.push({
            id: Date.now(),
            title: inputValue.value,
            completed: false,
            isEditing: false,
            decoration: {textDecoration: 'none'},
            date: `${date.getDay()}.${date.getMonth()}.${date.getFullYear()}`
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

    const filterTask = computed(() => {
            if(selectedOption.value === 'Все') {
                return [...tasks.value];
            }
            else if(selectedOption.value === 'Завершенные') {
                return [...tasks.value].filter(item => item.completed)
            }
            else if(selectedOption.value === 'Незавершенные') {
                return [...tasks.value].filter(item => !item.completed)
            }
        })

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

                <MyFilter v-model="selectedOption"/>

                <MyTaskManager
                    :tasks="filterTask"
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
        background: url(/BG2.jpg) center/cover no-repeat;
        &__inner {
            background-color: #32315b;
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 600px;
            margin: 0 auto;
            gap: 20px 0;
            padding: 10px;
            border-radius: 25px;
            
        }
    }

    .filter {
        margin-left: auto;
    }
    .select {
        width: 180px;
        padding: 5px 10px;
    }
</style>
