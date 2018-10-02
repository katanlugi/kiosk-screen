<template>
    <div class="display" style="--aspect-ratio:16/9;">
        <custom-content class="content"></custom-content>
        <add-container class="add"></add-container>
    </div>
</template>

<script>
import AddContainer from '@/components/AddContainer.vue';
import CustomContent from '@/components/CustomContent.vue';

export default {
    name: 'display',
    components: {
        AddContainer, CustomContent
    }
}
</script>

<style lang="scss">
    .display {
        // height: 100vh;
        // width: auto;
        margin: 0px;
        padding: 0px;
        background-color: rgb(20, 23, 28);//#1a1d24;
        display: grid;
        grid-gap: 10px;
    }
    
    .content {
        height: 70vh;
    }
    
    .add {
        height: 30vh;
        margin-bottom: 0px;
        background-color: bisque;
    }
</style>
