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

<style lang="scss">
::-webkit-scrollbar {
    height: 12px;
    width: 14px;
    background: transparent;
    z-index: 12;
    overflow: visible;
}

::-webkit-scrollbar-thumb {
    width: 10px;
    background-color: #c1c1c1;
    border-radius: 10px;
    z-index: 12;
    border: 4px solid rgba(0, 0, 0, 0);
    background-clip: padding-box;
    transition: background-color .32s ease-in-out;
    margin: 4px;
    min-height: 32px;
    min-width: 32px;
}

::-webkit-scrollbar-thumb:hover {
    background: #c1c1c1;
}
</style>
