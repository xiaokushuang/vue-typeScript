<template>
  <div class="practiceSon-class">
    子组件内容
    {{ dialogVisible }}---{{ sonObj }}
    <div>
      <el-button @click="handleCloseDialog('取消')">取 消</el-button>
      <el-button type="primary" @click="handleCloseDialog('确定')"
        >确 定</el-button
      >
    </div>
  </div>
</template>
<script lang="ts">
import { ToUser } from "@/types";
import { Component, Prop, Vue, Watch, Emit } from "vue-property-decorator";
@Component
export default class Test extends Vue {
  // 接受父组件的值
  @Prop({ default: false }) dialogVisible!: boolean;
  @Prop({ default: {} }) sonObj?: ToUser;
  //子传父
  @Emit("handleCloseDialog")
  //子传父方法
  private handleCloseDialog(val: string): void {
    // return val;
  }
  // 生命周期
  private created(): void {}
  private mounted(): void {}
  private updated(): void {}
  private destroyed(): void {}
}
</script>
