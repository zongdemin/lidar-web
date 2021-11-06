<template>
  <global-footer class="footer custom-render">
    <template v-slot:links>
      <a  target="_blank">北京和创亿铭科技有限公司</a>
    </template>
  </global-footer>
</template>

<script>
import { GlobalFooter } from '@ant-design-vue/pro-layout'

export default {
  name: 'ProGlobalFooter',
  components: {
    GlobalFooter
  }
}
</script>
