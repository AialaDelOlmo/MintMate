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
                    <Graphic :amounts="amounts"/>
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
                //amounts: [100, 400, 500, 200, -400, -200, -300, 0, 300, 800],  // Example amounts for the graphic component
                dateLabel: "2024/07/19",
                movements: [{
                    id: 1,
                    title: "Movimiento 1",
                    description: "Salario",
                    amount: 1500,
                    time: new Date("2024-06-10"),
                },
                {
                    id: 2,
                    title: "Movimiento 2",
                    description: "Alquiler",
                    amount: -700,
                    time: new Date("2024-06-22"),
                },
                {
                    id: 3,
                    title: "Movimiento 3",
                    description: "Comida",
                    amount: -100,
                    time: new Date("2024-06-26"),
                },
                {
                    id: 4,
                    title: "Movimiento 4",
                    description: "Estudios",
                    amount: -100,
                    time: new Date("2024-06-29"),
                },
                {
                    id: 5,
                    title: "Movimiento 5",
                    description: "Facturas",
                    amount: -300,
                    time: new Date("2024-07-01"),
                },
                {
                    id: 6,
                    title: "Movimiento 6",
                    description: "Freelance",
                    amount: 1500,
                    time: new Date("2024-07-'03'"),
                },
                {
                    id: 7,
                    title: "Movimiento 7",
                    description: "subscripciones",
                    amount: -50,
                    time: new Date("2024-07-05"),
                },
                {
                    id: 8,
                    title: "Movimiento 8",
                    description: "Taller",
                    amount: -100,
                    time: new Date("2024-07-10"),
                },
                {
                    id: 9,
                    title: "Movimiento 9",
                    description: "Compras online",
                    amount: -200,
                    time: new Date("2024-07-12"),
                },
                {
                    id: 10,
                    title: "Movimiento 10",
                    description: "Viaje",
                    amount: -500,
                    time: new Date("2024-07-15"),
                }]
            }
        },
        computed: {
            amounts() {
                const lastDays = this.movements
                    .filter(m => {
                        const today = new Date();
                        const oldDate = today.setDate(today.getDate() - 30);

                        return m.time > oldDate;
                    })
                    .map(m => m.amount);

                    return lastDays.map((m, i) => {
                        const lastMovements = lastDays.slice(0, i);
                        return lastMovements.reduce((suma,movement) => {
                            return suma + movement
                        }, 0);
                    });
            }
        }
    };
    

</script>