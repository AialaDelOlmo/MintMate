<template>
    <Layout>
        <template #header>
            <Header></Header>
        </template>
        <template #resume>
            <Resume
                :label="'Ahorro total'"
                :dateLabel="dateLabel"
                :total-amount="100000"
                :amount="amount"
            >
                <template #graphic>
                    <Graphic/>
                </template>
                <template #action>
                    <Action/>
                </template>
            </Resume>  
        </template>
        <template #movements>
            <Movements
                :movements="movements">
        </Movements>
        </template>
    </Layout>
</template>

<script>
    import Layout from './Layout.vue';
    import Header from './Header.vue';
    import Resume from './Resume/Index.vue';
    import Movements from './Movements/Index.vue';
    import Action from './Action.vue';
    import Graphic from './Resume/Graphic.vue';

    export default {
        components: { 
            Layout,
            Header,
            Resume,
            Movements,
            Action,
            Graphic,
        },

        data() {
            return {
                amount: null,
                dateLabel: "2024/07/19",
                movements: [{
                    id: 1,
                    title: "Movimiento 0",
                    description: "Salario",
                    amount: "2500",
                },
                {
                    id: 2,
                    title: "Movimiento 1",
                    description: "Alquiler",
                    amount: "-700",
                },
                {
                    id: 3,
                    title: "Movimiento 3",
                    description: "Comida",
                    amount: "-100",
                },
                {
                    id: 4,
                    title: "Movimiento 4",
                    description: "Estudios",
                    amount: "-100",
                },
                {
                    id: 5,
                    title: "Movimiento 5",
                    description: "Facturas",
                    amount: "-300",
                }]
            }
        },
    };
    

</script>