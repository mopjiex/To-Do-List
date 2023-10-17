<script setup>
    import { computed, ref, watch } from 'vue';
    import MyTask from '@/components/My-Task.vue';
    import MyFilter from '@/components/My-Filter.vue';
    import MySorted from '@/components/My-Sorted.vue';
    import MyTaskManager from '@/components/My-TaskManager.vue';
    const inputValue = ref('');
    const editInputValue = ref('');
    const tasks = ref([]); 
    const selectedOption = ref('Все');
    const sortedOption = ref('Без');
    const clickedButtonNumber = ref('Высокий');
    const color = ref({
        BG: '#F25F5C',
        text: '#fff',
    });

    const createDate = () => {
        const date = new Date();
        const year = date.getFullYear();
        const month = String(date.getMonth() + 1).padStart(2, '0'); 
        const day = String(date.getDate()).padStart(2, '0'); 
        const hours = String(date.getHours()).padStart(2, '0');
        const minutes = String(date.getMinutes()).padStart(2, '0');
        const seconds = String(date.getSeconds()).padStart(2, '0');
        const formattedDate = `${year}-${month}-${day}T${hours}:${minutes}:${seconds}`;
        return formattedDate;
    }
    const createTask = () => {
       
        tasks.value.push({
            id: Date.now(),
            title: inputValue.value,
            completed: false,
            isEditing: false,
            decoration: {textDecoration: 'none'},
            date: createDate(),
            priority: clickedButtonNumber.value,
            priorityColor: {
                BG: color.value.BG,
                text: color.value.text,
            },
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

    const sortedTask = computed(() => {
        if(sortedOption.value === 'Без') return [...tasks.value]
        else if(sortedOption.value === 'Время') {
            return [...tasks.value].sort((a, b) => {
                const dataA = new Date(a.date);
                const dataB = new Date(b.date);
                console.log(dataA, dataB)
                return dataB - dataA;
            })
           
        }
        else if(sortedOption.value === 'Приоритет') {
            return [...tasks.value].sort((a, b) => {
                const priorityOrder = {
                    'Высокий': 1,
                    'Средний': 2,
                    'Низкий': 3,
                }

                return priorityOrder[a.priority] - priorityOrder[b.priority];
            });
        }
    })


    const combineTasks = computed(() => {
        const filtered = filterTask.value;
        const sorted = sortedTask.value;

        return sorted.filter(task => filtered.includes(task));
    })


    const priority = (index) => {
        const priorityValue = [
            { value: 'Высокий', BG: '#F25F5C', text: '#fff' },
            { value: 'Средний', BG: '#FFC857', text: '#000' },
            { value: 'Низкий', BG: '#A8DADC', text: '#000' },
        ];

        clickedButtonNumber.value = priorityValue[index - 1].value;
        color.value.BG = priorityValue[index - 1].BG;
        color.value.text = priorityValue[index - 1].text;

    }
    
    watch([selectedOption, sortedOption], () => {
        combineTasks.value;
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
                    @priority="priority"
                />

                <div class="app__wrapper">
                    <MySorted v-model="sortedOption"/>
                    <MyFilter v-model="selectedOption"/>
                </div>
                
                
                <MyTaskManager
                    :tasks="combineTasks"
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
            width: 800px;
            margin: 0 auto;
            gap: 20px 0;
            padding: 10px;
            border-radius: 25px;
        }
        &__wrapper {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
            padding: 0 20px;
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
