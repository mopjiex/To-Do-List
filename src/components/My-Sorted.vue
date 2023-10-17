<script setup>
    import { watch, ref } from 'vue';

    const props = defineProps({
        modelValue: String,
    })
    const emit = defineEmits();

    const sortedOption = ref(props.modelValue);

    watch(sortedOption, (newValue) => {
        emit('update:modelValue', newValue);
        console.log(newValue)
})
</script>

<template>
    <div class="sorted">
        <h2 class="sorted__title">Сортировка</h2>
            <select  class="select" v-model="sortedOption">
                <option class="select__option" value="Без">Без сортировки</option>
                <option class="select__option" value="Время">По времени</option>
                <option class="select__option" value="Приоритет">По приоритету</option>
            </select>
    </div>
</template>

<style lang="scss">
    .sorted{  
        &__title {
            margin-bottom: 10px;
            color: #fff;
        }
        .select {
            background-color: #44446a;
            border: none;
            color: #fff;
            width: 180px;
            padding: 5px 10px;
        }
    }
</style>