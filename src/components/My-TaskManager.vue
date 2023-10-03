<script setup>
    import { ref } from 'vue';

    const checked = ref(false);

    const props = defineProps({
        tasks: Array,
        color: String,
    })

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
    const updateCheckbox = (index) => {
        emit('updateCheckbox', index);
    }
</script>

<template>
    <div class="task-manager">
        <div class="task-manager__infinished">
            <h2 class="task-manager__title title">Задачи</h2>
            <div class="task-manager__card" 
                v-for="(task, index) in tasks" 
                :key="task.id"
                :style="{ backgroundColor: task.color }"
            >
                <div class="task-manager__card-left">
                    <input 
                        type="checkbox" 
                        class="task-manager__card-checkbox" 
                        v-model="task.completed"
                        @input="updateCheckbox(index)">
                    <div class="task-manager__card-desc">
                        <p class="task-manager__card-desc-id"> {{ index + 1 }} </p>
                        <h3 class="task-manager__card-desc-title">{{ task.title }}</h3>
                    </div>
                </div>
                <div class="task-manager__card-right" v-if="!task.isEditing">
                    <button class="task-manager__card-btn" @click="editTask(index)">Редактировать</button>
                    <button class="task-manager__card-btn" @click="removeTask(index)">Удалить</button>
                </div>

                <div class="task-manager__card-right" v-else>
                    <button class="task-manager__card-btn">Сохранить</button>
                    <button class="task-manager__card-btn" @click="cancelTask(index)">Отменить</button>
                </div>

            </div>
        </div>
    </div>
</template>

<style lang="scss">
    .task-manager {
        padding: 20px 10px;
        width: 700px;
        background-color: RGBA(247, 249, 249, .8);
        border-radius: 12px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        max-height: 700px;
        overflow: auto;
        &__title {
            border-bottom: 2px solid #3D405B;
            margin-bottom: 15px;
        }
        &__card {
            // background-color: #E63946;
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
            &-btn {
                background-color: #ddd;
                padding: 10px;
                border-radius: 8px;
            }
        }
    }
</style>