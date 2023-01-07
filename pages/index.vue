<template>
  <converter/>
</template>

<script lang="ts">
import Vue from 'vue'
import Converter from '~/components/Converter.vue'

export default Vue.extend({
  components: { Converter },
  name: 'IndexPage',
})
</script>

<style >
*{
  padding: 0;
  margin: 0;
}
</style>
