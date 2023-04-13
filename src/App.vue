<template>
    <q-layout view="lHh Lpr lFf">
        <q-header style="background: #000;" elevated class="text-center">
            <img
            class="q-mt-sm"
                src="@/assets/cartola-logo.png"
                alt=""
                width="120"
                height="39"
            />
        </q-header>

        <q-page-container>
            <MarketTable/>   
        </q-page-container>
    </q-layout>
</template>

<script>
import MarketTable from "@/components/MarketTable.vue";
export default {
    name: "LayoutDefault",

    components: {
        MarketTable
    },
};
</script>
