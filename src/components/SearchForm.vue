<template>
  <form @submit.prevent>
    <div class="input-group">
      <input type="text" v-model="queryText" class="form-control">
      <button @click="callSearch" class="btn btn-success">Найти</button>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    msg: String
  },
  data() {
    return {
      queryText: ''
    }
  },
  methods: {
    callSearch(){
      this.$emit('search', this.queryText);
      this.resetForm();
    },
    resetForm(){
      this.queryText = '';
    }
  }
}
</script>

<style>

</style>
