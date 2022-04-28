<template>
  <q-page padding>
    <div class="q-pa-md">
      <q-table
        title="Auditorias"
        :rows="auditorias"
        :columns="columns"
        row-key="id"
      >
        <template v-slot:body-cell-action="props">
          <q-td :props="props">
            <q-btn
              color="negative"
              icon-right="delete"
              no-caps
              flat
              @click="deleteId(props.auditoria)"
            />
            <q-btn
              icon-right="mode_edit"
              no-caps
              flat
              @click="
                editId(props);
                promptEdicao = !promptEdicao;
              "
            />
          </q-td>
        </template>
      </q-table>
      <ModalInsercao />
      <ModalEdicao v-model:promptEdicao="promptEdicao" />
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import { api } from 'boot/axios'
import ModalInsercao from 'src/components/ModalInsercao.vue'
import ModalEdicao from 'src/components/ModalEdicao.vue'

export default defineComponent({
  name: 'IndexPage',
  methods: {
  },
  setup() {
    const auditorias = ref([])
    const promptEdicao = ref(false)
    const columns = [
      { name: 'id', field: 'id', label: 'Id', sortable: true },
      { name: 'recomendacao', field: 'recomendacao', label: 'Recomendação', sortable: true },
      { name: 'descricaoacao', field: 'descricaoacao', label: 'Descrição Ação', sortable: true },
      { name: 'statussiaud', field: 'statussiaud', label: 'Status SIAUD', sortable: true },
      { name: 'gerenciaresponsavel', field: 'gerenciaresponsavel', label: 'Gerência Responsável', sortable: true },
      { name: 'vencimentoacao', field: 'vencimentoacao', label: 'Vencimento', sortable: true },
      { name: 'action', label: 'action', field: 'action' }
    ]
    const deleteId = (auditoria) => {
      console.log(auditoria.recomendacao)
    }

    const editId = (props) => {
      console.log(props.key)
      // this.promptEdicao(true)
    }
    onMounted(() => {
      getPosts()
    })
    const getPosts = async () => {
      try {
        const { data } = await api.get('http://localhost:3000/auditorias')
        console.log('data: ', data)
        auditorias.value = data
        console.log(auditorias.value)
      } catch (error) {
        console.log(error)
      }
    }
    return {
      auditorias,
      columns,
      deleteId,
      editId,
      promptEdicao
    }
  },
  components: { ModalInsercao, ModalEdicao }
})
</script>
