<template>
    <section>
        <router-link to="/projetos/novo" class="button">
            <span class="icon is-small">
                <i class="fas fa-plus"></i>
            </span>
            <span>Novo Projeto</span>
        </router-link>
        <table class="table is-fullwidth">
            <thead>
                <tr>
                    <th>Id</th>
                    <th>Nome do Projeto</th>
                    <th>Acoes</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="projeto in projetos" :key="projeto.id">
                    <td> {{ projeto.id }} </td>
                    <td> {{ projeto.nome }} </td>
                    <td>
                        <router-link :to="`/projetos/${projeto.id}`" class="button">
                            <span class="icon is-small">
                                <i class="fas fa-pencil-alt"></i>
                            </span>
                        </router-link>

                        <button class="button ml-2 is-danger" @click="excluir(projeto.id)">
                            <span class="icon is-small">
                                <i class="fas fa-trash"></i>
                            </span>
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </section>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue';
import { nossaUseStore } from '@/store';
import { EXCLUIR_PROJETO } from '@/store/tipo-mutacoes';
import useNotificador from '@/hooks/notificador';
import { TipoNotificacao } from '@/interfaces/INotificacao';

export default defineComponent({
    name: 'Lista',
    methods: {
        excluir (id: string) {
            this.store.commit(EXCLUIR_PROJETO, id)
            this.notificar(TipoNotificacao.ATENCAO, 'Projeto Apagado', 'O projeto foi apagado com sucesso.')
        }
    },
    setup() {
        const store = nossaUseStore()
        const { notificar } = useNotificador()
        return {
            projetos: computed(() => store.state.projetos),
            store,
            notificar
        }
    }
});
</script>
