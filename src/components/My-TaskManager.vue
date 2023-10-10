<script setup>
    import myBtn from '@/components/My-Button.vue'
    import { ref } from 'vue';

    const checked = ref(false);

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
            <div class="task-manager__card" 
                v-for="(task, index) in tasks" 
                :key="task.id"
            >
                <div class="task-manager__card-left">

                    <input 
                        type="checkbox" 
                        class="task-manager__card-checkbox" 
                        v-model="task.completed"
                        @input="updateCheckbox(index)"
                    >
                    
                    <div class="task-manager__card-desc">
                        <p class="task-manager__card-desc-id"> {{ index + 1 }} </p>
                        <h3 
                            class="task-manager__card-desc-title"
                            :style="task.decoration"
                        >{{ task.title }}</h3>
                    </div>
                </div>
                <div class="task-manager__card-right" v-if="!task.isEditing">
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

                <div class="task-manager__card-right" v-else>
                    <input 
                        class="task-manager__card-right-input" 
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
        background-color: RGBA(59, 46, 79, .8);
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
        &__card {
            background-color: #3E4C59;
            color: #ddd;
            padding: 15px 10px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 15px;
            &-left {
                display: flex;
                align-items: center;
                gap: 0 20px;
            }
            &-right {
                display: flex;
                align-items: center;
                gap: 0 20px;
                &-input {
                    padding: 10px 15px;
                    border-radius: 5px;
                    font-size: 18px;
                }
            }
            &-desc {
                display: flex;
                align-items: center;
                gap: 0 20px;
                &-id {
                    font-size: 20px;
                }
                &-title {
                    font-size: 20px;
                    text-align: center;   
                }
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