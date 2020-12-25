<template>
  <div class="practice-class">
    <el-button @click="handleClickBtn()">现在这个是一个父组件</el-button>
    <!-- 计算属性练习 -->
    <div>
      <el-input v-model="valueModel" placeholder=""></el-input>
      <el-input v-model="valueModel2" placeholder=""></el-input>
      <div>{{ computedContent }}</div>
      <div>--------------------</div>
      <div>{{ computedContent2 }}</div>
      <div v-for="data in list" :key="data">
        {{ data }}
      </div>
    </div>
    <!-- 弹窗 -->
    <el-dialog title="子组件弹窗" :visible.sync="dialogVisible" width="200">
      <div>
        <practiceSon
          :dialogVisible="dialogVisible"
          :sonObj="sonObj"
          @handleCloseDialog="handleCloseDialog"
        ></practiceSon>
      </div>
    </el-dialog>
  </div>
</template>
<script lang="ts">
import { Params, ProjectList, ProjectsData, ToUser } from "@/types/index";
import { Component, Prop, Vue, Watch, Emit } from "vue-property-decorator";
import practiceSon from "./practiceSon.vue";
// 引入组件(有没有组件都必须写，不然页面内容不生效（比如父传子的值传不过去）)
@Component({
  components: {
    practiceSon
  }
})
export default class PracticeParent extends Vue {
  // 定义数据
  private dialogVisible: boolean = false;
  private valueModel: string = "";
  private valueModel2: string = "绑定值2";
  private list: any[] = [1, 2, 3, "555", "闫明爽"];
  public sonObj: ToUser = {
    user_id: "111",
    name: "小护士",
    avatar: "头像",
    type: 12
  };
  //定义methods 方法
  private handleClickBtn(): void {
    this.dialogVisible = true;
  }
  private handleCloseDialog(val: string): void {
    this.dialogVisible = false;
    console.log("子组件传过来的值", val);
  }
  //计算属性
  public get computedContent() {
    return this.valueModel;
  }
  public get computedContent2() {
    return this.valueModel2;
  }
  public set computedContent(message: string) {
    this.valueModel = message + "set";
  }

  //watch
  @Watch("valueModel", {
    deep: true
  })
  public watchmethods1(newVal: string, oldVal: string) {
    debugger;
  }
  @Watch("valueModel2", {
    deep: true
  })
  public watchmethods2(newVal: string, oldVal: string) {
    debugger;
  }
  // 生命周期
  private created(): void {}
  private mounted(): void {
    console.log("111");
  }
  private updated(): void {}
  private destroyed(): void {}
}
</script>
