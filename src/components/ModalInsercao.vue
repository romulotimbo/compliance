<template>
  <div class="q-pa-md q-gutter-sm">
    <q-btn label="Inserir" color="primary" @click="prompt = true" />
    <q-dialog v-model="prompt" persistent>
      <q-card>
        <q-card-section>
          <div class="text-h6">Ação</div>
        </q-card-section>
        <q-card-section>
          <q-input
            dense
            v-model="acao"
            autofocus
            @keyup.enter="prompt = false"
          />
        </q-card-section>
        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancelar" v-close-popup />
          <q-btn flat label="Adicionar" v-close-popup @click="adicionar()" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'ModalInsercao',
  components: {
  },
  methods: {
    adicionar() {
      console.log(this.acao)
    }
  },
  setup() {
    return {
      prompt: ref(false),
      acao: ref('')
    }
  }
})
</script>

<style scoped>
</style>
