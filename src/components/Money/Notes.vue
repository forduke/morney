<template>
  <div>
    <label class="notes">
      <span class="name">备注</span>
      <input type="text"
             v-model="value"
             placeholder="在这里输入备注">
    </label>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Watch} from 'vue-property-decorator';
  
  @Component
  export default class Notes extends Vue {
    value = '';
    
    @Watch('value')
    onValueChanged(value: string) {
      this.$emit('update:value', value);
    }
  }
</script>

<style lang="scss" scoped>
  .notes {
    background: #f5f5f5;
    font-size: 14px;
    display: flex;
    align-items: center;
    padding-left: 16px;
    
    .name {
      padding-right: 16px;
    }
    
    input {
      line-height: 64px;
      flex-grow: 1;
      border: none;
      background: transparent;
      margin-right: 10px;
    }
  }

</style>
