<template>
  <div>
    <mavon-editor ref="editor" v-model="doc" style="height: 650px" />
  </div>
</template>

<script>
import { mavonEditor } from 'mavon-editor'
import 'mavon-editor/dist/css/index.css'

export default {
  name: 'Create',
  components: { mavonEditor },
  data() {
    return {
      doc: ''
    }
  }
}
</script>
<style>
.mavonEditor {
  height: 100%;
  width: 100%;
}
</style>
