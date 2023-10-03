<script setup> 
    import { ref } from 'vue';

    const inputValue = ref('');
    const props = defineProps({
        inputPlaceholder: String,
    });

    const emit = defineEmits();

    const updateInputValue = () => {
        emit('update:modelValue', inputValue.value);
    }

    const submitTask = () => {
        emit('submit');
        inputValue.value = '';
    }
</script>

<template>
    <div class="task">
        <h2 class="task__title title">Добавление задачи</h2>  
            <input 
                type="text" 
                class="task__input" 
                :placeholder="inputPlaceholder"
                v-model="inputValue"
                @input="updateInputValue"
                > 

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
        height: 200px;
        background-color: RGBA(247, 249, 249, .8);
        border-radius: 12px;
        &__title {
            margin-bottom: 15px;
        }
        &__input {
            font-size: 20px;
            width: 100%;
            padding: 10px 15px;
            border: none;
            border-radius: 10px;
            background-color: RGBA(168, 179, 196, .7);
            margin-bottom: 15px;
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