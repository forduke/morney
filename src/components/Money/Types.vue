<template>
  <div>
    <ul class="types">
      <li :class="value === '-' && 'selected'" @click="selectType('-')">支出</li>
      <li :class="value === '+' && 'selected'" @click="selectType('+')">收入</li>
    </ul>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';
  
  @Component
  export default class Types extends Vue {
    // 从外部把值传进来，统一修改
    @Prop() readonly value!: string; // !让编译器忽略value的初始值问题
    
    selectType(type: string) {
      if (type !== '-' && type !== '+') { // type 只能是 '-' 或'+'
        throw new Error('type is unknown');
      }
      this.$emit('update:value', type);
    }
  }
</script>

<style lang="scss" scoped>
  .types {
    background: #c4c4c4;
    display: flex;
    text-align: center;
    font-size: 24px;
    
    > li {
      width: 50%;
      height: 64px;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
      
      &.selected::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 4px;
        background-color: #333333;
      }
    }
  }

</style>
