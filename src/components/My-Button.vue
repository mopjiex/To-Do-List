<script setup>

    const emit = defineEmits();
    const props = defineProps({
        imgName: String,
        myClass: String,
        
    })
    const btnEvent = () => {
        emit('btn');
    }

</script>


<template>
    <button :class="`btn ${myClass}`" @click="btnEvent">
        <img :src="imgName" alt="" class="btn__img">
    </button>
</template>


<style lang="scss">
    .btn {
        padding: 10px;
        border-radius: 8px;
        transition: all .3s;
        &__img {
            width: 20px;
            height: 20px;
        }
        &:hover {
            transform: scale(1.2);
        }
    }
</style>