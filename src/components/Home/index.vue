<template>
    <Layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume 
            :label="label" :amount="amount" :totalAmount="100000" >
                <template #graphic>
                    graphhic
                </template>
                <template #action>
                    <Action /> 
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="movements" />
        </template>
    </Layout>
</template>

<script>
    import Header from "@/components/Header"
    import Layout from "@/components/Layout"
    import Resume from "@/components/Resume"
    import Movements from "@/components/Movements"
    import Action from "@/components/Action"
    export default {
        components: {
            Header,
            Layout,
            Resume,
            Movements,
            Action
        },
        data() {
            return {
                amount: null,
                label: null,
                movements: [{
                    id: 1,
                    title: "Movimiento Uno",
                    description: "oremsjjahdjhas",
                    amount: 110,
                },
                {
                    id: 2,
                    title: "Movimiento dos",
                    description: "oremsjjahdjhas",
                    amount: - 100,
                }]
            }
        }
    }
</script>