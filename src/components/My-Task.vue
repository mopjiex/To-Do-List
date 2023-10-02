<script setup> 
    import { ref } from 'vue';

    const taskData = ref(props.modelValue);

    const props = defineProps({
        inputPlaceholder: String,
        textAreaPlaceholder: String,
        modelValue: Object,
    });

    const emit = defineEmits();

    const updateInputValue = () => {
        emit('update:modelValue', taskData.value);
    }

    const updateTextAreaValue = () => {
        emit('update:modelValue', taskData.value);
    }

    const submitTask = () => {
        emit('submit');
    }
</script>

<template>
    <div class="task">
        <h2 class="task__title title">Добавление задачи</h2>  
            <input 
                type="text" 
                class="task__input" 
                :placeholder="inputPlaceholder"
                v-model="taskData.inputValue"
                @input="updateInputValue"
                > 
            <textarea 
                class="task__textarea" 
                :placeholder="textAreaPlaceholder"
                v-model="taskData.textAreaValue"
            />
            <button 
                class="task__btn"
                @click="submitTask"
            >
                    Добавить
            </button>
    </div>
</template>

<style lang="scss">
    .task {
        padding: 20px 10px;
        width: 550px;
        background-color: RGBA(247, 249, 249, .8);
        border-radius: 12px;
        &__title {
            margin-bottom: 15px;
        }
        &__input,
        &__textarea {
            width: 100%;
            padding: 10px 15px;
            border: none;
            border-radius: 10px;
            background-color: RGBA(168, 179, 196, .7);
            margin-bottom: 15px;
        }
        &__input {
            font-size: 20px;
        }
        &__textarea {
            font-size: 18px;
            height: 150px;
        }
        &__btn {
            width: 100%;
            background-color: #3B3B98;
            border-radius: 8px;
            padding: 10px;
            color: #E2E8F0;
            font-size: 20px;
            transition: all .3s;
            &:hover {
                background-color: #1F4E79;
            }
        }
    }
</style>