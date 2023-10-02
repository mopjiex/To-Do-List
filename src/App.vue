<script setup>
    import { reactive, ref } from 'vue';
    import MyTask from '@/components/My-Task.vue';

    const taskData = reactive({
      inputValue: '',
      textAreaValue: '',
    })

    const createTask = () => {
      console.log(taskData.inputValue, taskData.textAreaValue)
    }
</script>

<template>
    <div class="app">
        <div class="container">
            <MyTask
                inputPlaceholder="Введите заголовок"
                textAreaPlaceholder="Введите описание"
                v-model="taskData"  
                @submit="createTask"   
            />
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
    }
</style>
