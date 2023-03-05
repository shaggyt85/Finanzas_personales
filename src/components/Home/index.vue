<template>
    <Layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume 
            :label="label" :amount="amount" :totalAmount="100000" >
                <template #graphic>
                    <Graphic :amounts="amounts"/>
                </template>
                <template #action>
                    <Action @create="create" /> 
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="movements" @remove="remove"/>
        </template>
    </Layout>
</template>

<script>
    import Header from "@/components/Header"
    import Layout from "@/components/Layout"
    import Resume from "@/components/Resume"
    import Movements from "@/components/Movements"
    import Action from "@/components/Action"
    import Graphic from "@/components/Graphic"
    export default {
        components: {
            Header,
            Layout,
            Resume,
            Movements,
            Action,
            Graphic
        },
        data() {
            return {
                amount: null,
                label: null,
                // amounts: [100, 200, 500, 200, -600, 2400, -1000, 500],
                movements: [{
                    id: 1,
                    title: "Movimiento Uno",
                    description: "Lorem Impsum and gerty hytui",
                    amount: 110,
                    time: new Date("04-03-2023")
                },
                {
                    id: 2,
                    title: "Movimiento dos",
                    description: "Lorem Impsum and gerty hytui",
                    amount: - 100,
                    time: new Date("04-03-2023")
                },
                {
                    id: 3,
                    title: "Movimiento tres",
                    description: "Lorem Impsum and gerty hytui",
                    amount: -510,
                    time: new Date("04-03-2023")
                },
                {
                    id: 4,
                    title: "Movimiento cuatro",
                    description: "Lorem Impsum and gerty hytui",
                    amount: 1010,
                    time: new Date("04-03-2023")
                },
                {
                    id: 5,
                    title: "Movimiento cinco",
                    description: "Lorem Impsum and gerty hytui",
                    amount: 1010,
                    time: new Date("04-03-2023")
                },]
            }
        },
        computed: {
            amounts() {
  return this.movements
    .filter(({ time }) => {
      const today = new Date();
      const oldDate = today.setDate(today.getDate() - 30);

      return time > oldDate;
    })
    .reduce((acc, { amount }) => {
      return acc.length ? [...acc, acc[acc.length - 1] + amount] : [amount];
    }, []);
},
        },
        methods: {
            create(movement) {
                this.movements.push(movement)
            },
            remove(id) {
                const index = this.movements.findIndex(m => m.id === id)
                this.movements.splice(index, 1)
            }
        }
    }
</script>