<script setup>
import { watch, ref } from 'vue';

    const props = defineProps({
        modelValue: String,
    })
    const emit = defineEmits();

    const selectedOption = ref(props.modelValue);

    watch(selectedOption, (newValue) => {
        emit('update:modelValue', newValue);
        console.log(newValue)
    })

</script>

<template>
    <div class="filter">
        <select  class="select" v-model="selectedOption">
            <option class="select__option" value="Все">Все</option>
            <option class="select__option" value="Завершенные">Завершенные</option>
            <option class="select__option" value="Незавершенные">Незавершенные</option>
        </select>
    </div>
</template>

<style lang="scss">
    .filter {
        margin-left: auto;
        .select {
            background-color: #44446a;
            border: none;
            color: #fff;
            width: 180px;
            padding: 5px 10px;
        }
    }
    
</style>