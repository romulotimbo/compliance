<template>
  <div class="q-pa-md q-gutter-sm">
    <q-dialog v-model="value" persistent>
      <q-card>
        <q-card-section>
          <div class="text-h6">Ação</div>
        </q-card-section>
        <q-card-section>
          <q-input dense v-model="acao" autofocus />
        </q-card-section>
        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancelar" v-close-popup />
          <q-btn flat label="Salvar" v-close-popup @click="editar()" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>

  <div class="q-pa-md q-gutter-sm">
    <q-dialog v-if="value" persistent>
      <q-card>
        <q-card-section>
          <div class="text-h6">Ação</div>
        </q-card-section>
        <q-card-section>
          <q-input dense v-model="acao" autofocus />
        </q-card-section>
        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancelar" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'ModalEdicao',
  props: {
    promptEdicao: {
      type: Boolean,
      required: true
    },
    editId: {
      type: Number
    }
  },
  emits: ['update:promptEdicao'],
  computed: {
    value: {
      get() {
        return this.promptEdicao
      },
      set(value) {
        this.$emit('update:promptEdicao', value)
      }
    }
  },
  setup() {
    return {
      acao: ref('')
    }
  },
  methods: {
    editar() {
      console.log(this.acao)
    }
  }
})
</script>

<style scoped>
</style>
