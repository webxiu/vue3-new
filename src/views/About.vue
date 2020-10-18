<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="add">{{ msg }}</button>
    <p>选择: {{ select }}</p>
    <p v-for="(item, index) in arr" @click="selectHandle(index)" :key="index">
      {{ item }}
    </p>
  </div>
</template>
<script lang="ts">
import {
  onMounted,
  onBeforeMount,
  reactive,
  ref,
  toRefs,
  watch,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  onActivated,
  onDeactivated,
  onErrorCaptured,
  onRenderTracked,
  onRenderTriggered
} from "vue";
interface ResProps {
  select: string;
  arr: string[];
  selectHandle: (index: number) => void;
}
// setup()            : 开始创建组件之前，在beforeCreate和created之前执行。创建的是data和method
// onBeforeMount()    : 组件挂载到节点上之前执行的函数。
// onMounted()        : 组件挂载完成后执行的函数。
// onBeforeUpdate()   : 组件更新之前执行的函数。
// onUpdated()        : 组件更新完成之后执行的函数。
// onBeforeUnmount()  : 组件卸载之前执行的函数。
// onUnmounted()      : 组件卸载完成后执行的函数
// onActivated()      : 被包含在<keep-alive>中的组件，会多出两个生命周期钩子函数。被激活时执行。
// onDeactivated()    : 比如从 A 组件，切换到 B 组件，A 组件消失时执行。
// onErrorCaptured()  : 当捕获一个来自子孙组件的异常时激活钩子函数（以后用到再讲，不好展现）。
// onRenderTracked()  : 状态跟踪

export default {
  setup() {
    console.log("1.setup==生命周期");
    const msg = ref(6666);
    const res: ResProps = reactive({
      select: "",
      arr: ["abc", "def", "5"],
      selectHandle: (index: number) => {
        res.select = res.arr[index];
      }
    });
    watch([msg, () => res.select], (newVal, oldVal) => {
      console.log("watch==监听:", newVal);
    });
    onBeforeMount(() => {
      console.log("2.1 onBeforeMount");
    });
    onMounted(() => {
      console.log("2.2 onMounted");
    });
    onBeforeUpdate(() => {
      console.log("3.1 onBeforeUpdate");
    });
    onUpdated(() => {
      console.log("3.2 onUpdated");
    });
    onBeforeUnmount(() => {
      console.log("4.1 onBeforeUnmount");
    });
    onUnmounted(() => {
      console.log("4.2 onUnmounted");
    });
    onActivated(() => {
      console.log("5.1 onActivated-->keep-alive");
    });
    onDeactivated(() => {
      console.log("5.1 onDeactivated-->keep-alive");
    });
    onErrorCaptured(() => {
      console.log("6.1 onErrorCaptured");
    });
    onRenderTracked(() => {
      console.log("7.1 onRenderTracked===状态跟踪");
    });
    onRenderTriggered(() => {
      console.log("7.2 onRenderTriggered===状态跟踪(单次追踪)");
    });
    const refRes = toRefs(res);
    const add = () => msg.value++;
    return {
      msg,
      add,
      ...refRes
    };
  }
};
</script>
