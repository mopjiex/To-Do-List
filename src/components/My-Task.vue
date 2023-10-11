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
            <div class="task__inner">
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
                    <img src="/plus.png" alt="" class="task__btn-img">
                </button>
            </div>
    </div>
</template>

<style lang="scss">
    .task {
        padding: 10px;
        width: 100%;
        color: #fff;
        border-radius: 12px;
        
        &__inner {
            background-color: #292850;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 5px 10px;
            border-radius: 25px;
        }

        &__title {
            margin-bottom: 15px;
        }
        &__input {
            font-size: 20px;
            width: 70%;
            padding: 10px 15px;
            border: none;
            border-radius: 10px;
            color: #ddd;
            background-color: transparent;
            cursor: pointer;
            &::placeholder {
                color: #ddd;
            }
        }

        &__btn {
            width: 30px;
            height: 30px;
            background-color: #3f84bd;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all .3s;
            &-img {
                width: 20px;
                height: 20px;
            }
            &:hover {
                transform: scale(1.1);
            }
        }
    }
</style>