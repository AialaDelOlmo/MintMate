<template>
    <div class="movement">{{ title  }}</div>
</template>

<script setup>
import { toRefs, defineProps } from 'vue';

const props = defineProps({
    title: {
        type: String,
        required: true
    }
});

const { title } = toRefs(props);
</script>