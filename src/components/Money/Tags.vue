<template>
  <div class="tags">
    <div class="new">
      <button>新增标签</button>
    </div>
    <ul class="current">
      <li v-for="tag in dataSource"
          :key="tag"
          :class="{selected: selectTags.indexOf(tag) >= 0}"
          @click="toggle(tag)">
        {{ tag }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';
  
  @Component
  export default class Tags extends Vue {
    @Prop() dataSource: string[] | undefined;
    selectTags: string[] = [];
    
    toggle(tag: string) {
      const index = this.selectTags.indexOf(tag);
      if(index >= 0) {
        this.selectTags.splice(index, 1)
      } else {
        this.selectTags.push(tag)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .tags {
    padding: 16px;
    font-size: 14px;
    flex-grow: 1;
    display: flex;
    flex-direction: column-reverse;
    
    > .current {
      display: flex;
      flex-wrap: wrap;
      overflow: auto;
      
      > li {
        $bg: #d9d9d9;
        background: $bg;
        $h: 24px;
        height: $h;
        line-height: $h;
        padding: 0 16px;
        margin-right: 12px;
        margin-top: 10px;
        border-radius: ($h/2);
        &.selected {
          background: darken($bg, 50%);
        }
      }
    }
    
    > .new {
      padding-top: 16px;
      
      button {
        background: transparent;
        border: none;
        color: #999;
        border-bottom: 1px solid;
        padding: 0 3px;
      }
    }
  }
</style>
