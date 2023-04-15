<template>
    <div class="q-pa-md">
        <q-table
            style="height: 90vh"
            title="Mercado"
            :columns="columns"
            :rows="playersList"
            flat
            bordered
            dark
            virtual-scroll
            :rows-per-page-options="[0]"
            :loading="loadingTableData"
            :filter="filter"
        >
            <template v-slot:loading>
                <q-inner-loading showing color="primary" />
            </template>
            <template v-slot:top-right>
                <q-input
                    dark
                    borderless
                    dense
                    debounce="300"
                    v-model="filter"
                    placeholder="Search"
                >
                    <template v-slot:append>
                        <q-icon name="search" />
                    </template>
                </q-input>
            </template>
            <template v-slot:body-cell-clube_id="props">
                <q-td style="width: 20px" :props="props">
                    <img id="shield" :src="shieldTeam(props.row.clube_id)" />
                </q-td>
            </template>
            <template v-slot:body-cell-status_id>
                <q-td style="width: 20px" class="text-center">
                    <i class="fa fa-check"></i>
                </q-td>
            </template>
            <template #body-cell-posicao_id="props">
                <q-td style="width: 50px" :props="props">
                    {{ getPosition(props.row) }}
                </q-td>
            </template>
        </q-table>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name: "MarketTable",

    data() {
        return {
            players: [],
            playersList: [],
            teams: [],
            positions: [],
            loadingTableData: true,
            filter: "",
            columns: [
                {
                    name: "clube_id",
                    label: "Time",
                    align: "left",
                    style: "width: 20px",
                    field: (row) => row.clube_id,
                    // format: (val) => `${val}`,
                    sortable: true
                },
                {
                    name: "status_id",
                    align: "left",
                    label: "Status",
                    field: "status_id",
                    sortable: true
                },
                {
                    name: "apelido",
                    align: "left",
                    style: "width: 240px",
                    label: "Jogador",
                    field: "apelido",
                    sortable: true
                },
                {
                    name: "posicao_id",
                    align: "left",
                    label: "Posição",
                    field: "posicao_id",
                    sortable: true
                },
                {
                    name: "jogos_num",
                    align: "right",
                    label: "Jogos",
                    field: "jogos_num",
                    sortable: true
                },
                {
                    name: "preco_num",
                    align: "right",
                    label: "Preço",
                    field: "preco_num",
                    sortable: true
                },
                {
                    name: "pontos_num",
                    align: "right",
                    label: "Última",
                    field: "pontos_num",
                    sortable: true
                },
                {
                    name: "media_num",
                    align: "right",
                    label: "Média",
                    field: "media_num",
                    sortable: true
                },
                {
                    name: "minimo_para_valorizar",
                    label: "Mín. p/ Valorizar",
                    field: "minimo_para_valorizar",
                    sortable: true
                }
            ]
        };
    },

    computed: {
        positionOptions() {
            return [
                { value: 0, text: "Todas" },
                ...Object.entries(this.positions).map((i) => {
                    return { value: i[1].id, text: i[1].nome };
                })
            ];
        }
    },

    mounted() {
        this.load();
    },

    methods: {
        load() {
            this.loadingTableData = true;
            axios
                .get("https://api.cartola.globo.com/atletas/mercado")
                .then((res) => {
                    this.players = res.data.atletas.filter(
                        (i) => i.status_id == 7
                    );
                    this.playersList = this.players;
                    this.teams = res.data.clubes;
                    this.positions = res.data.posicoes;
                })
                .finally(() => {
                    this.loadingTableData = false;
                });
        },

        getPosition(player) {
            let positions = Object.entries(this.positions);
            return positions.filter((i) => i[0] == player.posicao_id)[0][1]
                .nome;
        },

        shieldTeam(code) {
            let teams = Object.entries(this.teams);
            return teams.filter((i) => i[0] == code)[0][1].escudos["30x30"];
        }
    }
};
</script>

<style></style>
