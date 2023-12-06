<template>
  <form @submit.prevent>
    <div class="input-group">
      <input class="form-control" type="text" v-model="queryText" placeholder="Поиск по документам">
      <button class="btn btn-success" @click="callSearch">Найти</button>
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
