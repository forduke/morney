<template>
  <Layout class-prefix="layout">
    <!--  给组件一个初始化的值，更新时又能获取到最新的值 .sync -->
    <NumberPad @update:value="onUpdateAmount" @submit="saveRecord"/>
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
  import {Component, Watch} from 'vue-property-decorator';

  const recordList: Record[] = JSON.parse(window.localStorage.getItem('recordList') || '[]');
  
  type Record = {
    tags: string[];
    notes: string;
    type: string;
    amount: number; // 数据类型
    createAt?: Date;  // 类 / 构造函数
  }
  @Component({
    components: {Tags, Notes, Types, NumberPad},
  })
  export default class Money extends Vue {
    tags = ['衣', '食', '住', '行', '娱乐'];
    recordList: Record[] = recordList;
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
    
    saveRecord() {
      const record2: Record = JSON.parse(JSON.stringify(this.record));
      record2.createAt = new Date();
      this.recordList.push(record2);
      console.log(this.recordList);
    }
    
    @Watch('recordList')
    onRecordListChanged() {
      window.localStorage.setItem('recordList', JSON.stringify(this.recordList));
    }
  }
</script>

<style lang="scss">
  .layout-content {
    display: flex;
    flex-direction: column-reverse;
  }
</style>
