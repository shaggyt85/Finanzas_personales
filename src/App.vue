<template>
    <Suspense>
        <template #default>
            <Home />
        </template>
        <template #fallback>
            <SplashScreen />
        </template>
    </Suspense>
</template>

<script>
    import SplashScreen from "@/components/SplashScreen"
    import { defineAsyncComponent } from "vue";

    export default {
        components: {
            SplashScreen,
            Home: defineAsyncComponent(()=> 
                new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(import("./components/Home"))
                    }, 2500)
                })
            )
        }
    }
</script>

<style>
    html, body, .app {
        min-width: 100vh;
        margin: 0;
        font-family: Arial, Helvetica, sans-serif;
    }
    *{
        --brand-green: #04b500;
        --brand-blue: #0689b0;
    }
    h1 span {
        color: var(--brand-green);
    }
</style>
