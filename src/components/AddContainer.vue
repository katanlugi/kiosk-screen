<template>
    <div class="add-container">
        <slider class="panel extra-wide-panel"></slider>
    </div>
</template>

<script>
import Slider from '@/components/Slider.vue';
export default {
    name: 'add-container',
    components: {
        Slider,
    }
}
</script>

<style>
    .add-container {
        background-image: url('../assets/add.jpg');
        color: azure;
        
    }
    .add-container > * {
        background-color: darkslategrey;
    }
</style>
