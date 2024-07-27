<template>
    <div>
        <svg 
            @touchstart="tap"
            @touchmove="tap"
            @touchend="unTap"
            viewBox="0 0 300 200">
            <!--Línea horizontal-->
            <line
                stroke="#c4c4c4"
                stroke-width="2"
                x1="0"
                x2="300"
                :y1="zero"
                :y2="zero"
            />
            <polyline 
                fill="none"
                stroke="#0689B0"
                stroke-width="2"
                :points="points"
            />
            <!--Línea del puntero o vertical (verde)-->
            <line
                v-show= "showPointer"
                stroke="#04b500"
                stroke-width="2"
                :x1="pointer"
                :x2="pointer"
                y1="0"
                y2="200"
            />
        </svg>
        <p>Últimos 30 días</p>
    </div>
</template>

<script setup>
import { toRefs, defineProps, computed, ref, watch, defineEmits } from 'vue';

const props = defineProps({
    amounts: {
        type: Array,
        default: () => [],
    }
});

const { amounts } = toRefs(props);

const amountToPixels = (amount) => {
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);

    // transformar el monto en pixeles. El minimo representa el 0% y el máximo el 100%
    const amountAbs = amount + Math.abs(min);
    const minMaxRange = Math.abs(max) + Math.abs(min);

    return 200 - ((amountAbs * 100) / minMaxRange) * 2;
}

const zero = computed(() => {
    return amountToPixels(0);
})

const points = computed(() => {
    const totalElementos = amounts.value.length;

    return amounts.value.reduce((points, amount, i) => {
        const x = (300 / totalElementos) * (i + 1);
        const y = amountToPixels(amount);
        return `${points} ${x},${y}`;
    }, `0, ${amountToPixels(amounts.value.length ? amounts.value[0] : 0)}`);
});

const showPointer = ref(false);
const pointer = ref(0);

const emit = defineEmits(["select"]);

watch(pointer, (value) => {
    const index = Math.ceil((value / (300/ amounts.value.length)));
    if (index < 0 || index > amounts.value.length) return;
    emit("select", amounts.value[index - 1]);
});

const tap = ({ target, touches }) => {
    showPointer.value = true;
    const elementWidth = target.getBoundingClientRect().width;
    const elementX = target.getBoundingClientRect().x;
    const touchX = touches[0].clientX;
    pointer.value = ((touchX - elementX) * 300) / elementWidth; // viewBox="0 0 300 200">
} 

const unTap = () => {
    showPointer.value = false;

} 
</script>

<style scoped>
    svg {
        width: 100%;
    }
    p {
        text-align: center;
    }
</style>