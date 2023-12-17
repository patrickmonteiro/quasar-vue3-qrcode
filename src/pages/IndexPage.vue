<template>
  <q-page>
    <div
      v-if="showCamera"
      style="height: 400px;">
      <qr-stream @decode="onDecode">
        <div style="color: red;" class="frame"></div>
      </qr-stream>
    </div>
    <qr-capture @decode="onDecode" class="mb"></qr-capture>
    <div
      v-if="qrcode"
      class="text-h6 text-center">
      <span class="text-purple-6">Leitura realizada: </span>{{ qrcode }}
    </div>
    <div class="q-mt-lg">
      <q-toggle
        label="Iniciar o leitor"
        v-model="showCamera"
        size="lg"
      />
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { QrStream, QrCapture } from 'vue3-qr-reader'

export default defineComponent({
  name: 'IndexPage',
  components: {
    QrStream,
    QrCapture
  },
  setup () {
    const qrcode = ref('')
    const showCamera = ref(false)
    const onDecode = (data) => {
      qrcode.value = data
    }
    return {
      onDecode,
      qrcode,
      showCamera
    }
  }
})
</script>
