<template>
  <div>
    <input type="checkbox" value="maxwel" v-model="names" />
    <label>Maxwel</label>
  </div>
  <div>
    <input type="checkbox" value="ochieng" v-model="names" />
    <label>Ochieng</label>
  </div>
  <div>
    <input type="checkbox" value="okeyo" v-model="names" />
    <label>Okeyo</label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      names: [],
    };
  },
};
</script>

<style>
</style>