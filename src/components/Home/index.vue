<template>
    <Layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume 
            :label="label" :amount="amount" :totalAmount="totalAmount" >
                <template #graphic>
                    <Graphic :amounts="amounts" @select="select" />
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
                movements: [],
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
totalAmount() {
    return this.movements.reduce((suma, m) => {
        return suma + m.amount
    }, 0)
}
        },
        mounted() {
            const movements = JSON.parse(localStorage.getItem("movements"))
            if(Array.isArray(movements)){
                this.movements = movements?.map(m => {
                    return {...m, time: new Date(m.time)}
                })
                }
        },
        methods: {
            create(movement) {
                this.movements.push(movement)
                this.save()
            },
            remove(id) {
                const index = this.movements.findIndex(m => m.id === id)
                this.movements.splice(index, 1)
                this.save()
            },
            save() {
                localStorage.setItem("movements", JSON.stringify(this.movements))
            },
            select(el) {
                console.log(el)
                this.amount = el
            }
        }
    }
</script>