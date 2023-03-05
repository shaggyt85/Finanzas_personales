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
                amounts: [100, 200, 500, 200, -600, 2400, -1000, 500],
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