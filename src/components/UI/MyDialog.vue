<template>
  <div class="dialog" v-if="show" @click="hideDialog">
    <div @click.stop class="dialogs__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import toggleMixin from "@/mixins/toggleMixin";

export default {
  name: "my-dialog",
  mixins: [toggleMixin]
}
</script>

<style scoped lang="scss">
.dialog{
  top:0;
  bottom: 0;
  right: 0;
  left: 0;
  background: rgba(0,0,0, 0.5);
  position: fixed;
  display: flex;
}

.dialogs__content{
  margin: auto;
  background: white;
  border-radius: 10px;
  min-height: 70px;
  min-width: 400px;
  padding: 20px;
}

</style>