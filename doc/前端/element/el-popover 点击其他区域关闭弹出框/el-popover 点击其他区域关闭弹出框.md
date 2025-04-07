# el-popover 点击其他区域关闭弹出框

1. 点击其他区域关闭弹出框
2. 多个弹出框的时候, 关闭其他弹出框

```vue title="const refs = ref<any[]>([]); // 使用回调的方式收集 const setRefs = (el: any) => { refs.value.push(el); }; // 更新时-重置refs onBeforeUpdate(() => { refs.value = []; }); // 关闭 const handleClose = () => refs.value.forEach(v => v.hide());"
const refs = ref<any[]>([]);
// 使用回调的方式收集
const setRefs = (el: any) => {
  refs.value.push(el);
};

// 更新时-重置refs
onBeforeUpdate(() => {
  refs.value = [];
});

// 关闭
const handleClose = () => refs.value.forEach(v => v.hide());


<el-popover :ref="setRefs" trigger="contextmenu" placement="right">
  <template #reference>
    <div  @click.right.prevent.stop="handleClose">
            
    </div>
  </template>
</el-popover>


```
