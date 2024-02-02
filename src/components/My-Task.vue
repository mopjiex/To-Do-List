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

    const prioritySelection = (index) => {
        emit('priority', index);
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
                    @keyup.enter="submitTask"
                > 

                <div class="task__priority">
                    <h3 class="task__priority-title">Выберите приоритет</h3>
                    <div class="task__priority-buttons">
                        <button 
                            class="task__priority-btn priority-red"
                            @click="prioritySelection(1)"
                        >
                            
                        </button>
                        <button 
                            class="task__priority-btn priority-yellow"
                            @click="prioritySelection(2)"
                        >
                            
                        </button>
                        <button 
                            class="task__priority-btn priority-green"
                            @click="prioritySelection(3)"
                        >
                            
                        </button>
                    </div>
                </div>

                <button 
                    class="task__btn"
                    @click="submitTask"
                >
                    <img src="../../public/plus.png" alt="" class="task__btn-img">
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
            width: 50%;
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

        &__priority {
            display: flex;
            align-items: center;
            gap: 0 20px;
            &-buttons {
                display: flex;
                align-items: center;
                gap: 0 15px;
            }
            &-btn {
                width: 30px;
                height: 30px;
                background-color: #fff;
                border-radius: 10px;
                transition: all .3s;
                &:hover {
                    transform: scale(1.1);
                }
            }

            .priority-red {
                background-color: #F25F5C;
            }

            .priority-yellow{
                background-color: #FFCF7F;
            }

            .priority-green {
                background-color: #A8DADC;
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