<template>
  <Layout class-prefix="layout">
  <!--  给组件一个初始化的值，更新时又能获取到最新的值 .sync -->
    <NumberPad @update:value="onUpdateAmount"/>
    <Types :value.sync="record.type"/>
    <Notes @update:value="onUpdateNotes"/>
    <Tags :data-source.sync="tags" @update:value="onUpdateTags"/>
  </Layout>
</template>

<script lang="ts">
  import Vue from 'vue';
  import NumberPad from '@/components/Money/NumberPad.vue';
  import Types from '@/components/Money/Types.vue';
  import Notes from '@/components/Money/Notes.vue';
  import Tags from '@/components/Money/Tags.vue';
  import {Component} from 'vue-property-decorator';
  
  type Record = {
    tags: string[];
    notes: string;
    type: string;
    amount: number;
  }
  @Component({
    components: {Tags, Notes, Types, NumberPad},
  })
  export default class Money extends Vue {
    tags = ['衣', '食', '住', '行', '娱乐'];
    record: Record = {
      tags: [],
      notes: '',
      type: '-',
      amount: 0
    };
    
    onUpdateTags(value: string[]) {
      this.record.tags = value;
      console.log(value);
    }
    
    onUpdateNotes(value: string) {
      this.record.notes = value;
      console.log(value);
    }
    
    onUpdateAmount(value: string) {
      this.record.amount = parseFloat(value);
      console.log(value);
    }
  }
</script>

<style lang="scss">
  .layout-content {
    display: flex;
    flex-direction: column-reverse;
  }
</style>
