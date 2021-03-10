<template>
  <div class="hello">
    <h3>Internet connection status</h3>
    <br />  
    <div class="online-view">
    <slot v-if="online" name="online">Online</slot>
    <slot v-else name="offline">Ofline</slot>
  </div>
  </div>
</template>

<script>
export default { 
  data() {
    return {
      online: navigator.onLine,
    };
  }, 
  mounted() {
    window.addEventListener("online", this.onchange);
    window.addEventListener("offline", this.onchange);
    this.onchange();
  },
  beforeDestroy() {
    window.removeEventListener("online", this.onchange);
    window.removeEventListener("offline", this.onchange);
  },
  methods: {
    onchange() {
      this.online = navigator.onLine;
      this.$emit(this.online ? "online" : "offline");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> 
</style>
