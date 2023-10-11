<script setup>
    import myBtn from '@/components/My-Button.vue'
    import { ref } from 'vue';
    
    const props = defineProps({
        tasks: Array,
    })

    const editInputValue = ref('');

    const emit = defineEmits();

    const removeTask = (index) => {
        emit('remove', index);
    }

    const editTask = (index) => {
        emit('edit', index);
    }

    const cancelTask = (index) => {
        emit('cancel', index);
    }

    const saveTask = (index) => {
        emit('save', index);
        editInputValue.value = '';
    }

    const updateCheckbox = (index) => {
        emit('updateCheckbox', index);
    }

    const updateEditInput = () => {
        emit('update:modelValue', editInputValue.value);
    }
</script>

<template>
    <div class="task-manager">
        <div class="task-manager__infinished">
            <h2 class="task-manager__title title">Задачи</h2>
            <div class="card" 
                v-for="(task, index) in tasks" 
                :key="task.id"
            >
                <div class="card__left">

                    <input 
                        type="checkbox" 
                        class="card__left-checkbox" 
                        v-model="task.completed"
                        @input="updateCheckbox(index)"
                    >
                    
                    <div class="card__left-desc">

                        <p class="card__left-desc__id"> № {{ index + 1 }} </p>
                        <h3 
                            class="card__left-desc__title"
                            :style="task.decoration"
                        >   {{ task.title }}
                        </h3>

                        <p class="card__left-desc__time">
                            <img src="/calendar.png" alt="" class="card__left-desc__time-img">
                            <span class="card__left-desc__time-text"> {{ task.date }}</span>
                        </p>
                    </div>
                </div>
                <div class="card__right" v-if="!task.isEditing">
                    <myBtn
                        imgName="/edit.png" 
                        myClass="edit"
                        @click="editTask(index)"
                    />
                    <myBtn
                        imgName="/trash.png" 
                        myClass="delete"
                        @click="removeTask(index)"
                    />
                    
                </div>

                <div class="card__right" v-else>
                    <input 
                        class="card__right-input" 
                        type="text"
                        v-model="editInputValue"
                        @input="updateEditInput"
                        >
                        
                    <myBtn
                        imgName="/save.png" 
                        myClass="save"
                        @click="saveTask(index)"
                    />
                    <myBtn
                        imgName="/cancel.png" 
                        myClass="cancel"
                        @click="cancelTask(index)"
                    />
                </div>

            </div>
        </div>
    </div>
</template>

<style lang="scss">
    ::-webkit-scrollbar {
        width: 5px; 
    }
    ::-webkit-scrollbar-track {
        background: #f1f1f1; 
    }

    ::-webkit-scrollbar-thumb {
        background: #3B5998; 
    }
    .task-manager {
        padding: 20px 10px;
        width: 100%;
        color: #fff;
        border-radius: 12px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        max-height: 600px;
        overflow: auto;
        &__title {
            border-bottom: 2px solid #fff;
            padding-bottom: 10px;
            margin-bottom: 15px;
        }
    }
  
    .card {
        color: #ddd;
        background-color: #44446a;
        padding: 15px;
        border-radius: 25px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 15px;
        &__left {
            display: flex;
            align-items: center;
            gap: 0 20px;
            &-checkbox {
                width: 25px;
                height: 25px;
            }
            &-desc {
                display: flex;
                flex-direction: column;
                gap: 0 20px;
                max-width: 150px;  
                width: 100%;
                &__id {
                    font-size: 20px;
                }
                &__title {
                    font-size: 18px;
                    word-wrap: break-word;
                    line-height: 110%;
                    margin-bottom: 10px;
                }

                &__time {
                    display: flex;
                    align-items: center;
                    gap: 0 10px;
                    &-img {
                        width: 20px;
                        height: 20px;
                    }
                }
            }
        }
        &__right {
            display: flex;
            align-items: center;
            gap: 0 20px;
            &-input {
                padding: 5px 10px;
                border-radius: 25px;
                font-size: 16px;
                width: 200px; 
            }
        }
    }

    .delete {
        background-color: #F08080;
    }
    .edit {
        background-color: #A3C1AD;
    }
    .cancel  {
        background-color: #E6B0AA;
    }
    .save {
        background-color: #3B5998;
    }
</style>