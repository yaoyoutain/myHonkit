# el-table宽度无法自适应

```vue 
<el-table :data='tableData' style='width: 100%;height: 100%;overflow: auto;'>
  <el-table-column label='编号' prop='id' width="100"></el-table-column>
  <el-table-column label='编号' prop='id' width="100"></el-table-column>
</el-table>


```


1. 当我父级div 使用flex布局的时候, 表格扩大宽大可以自适应, 但是当表格缩小的时候自适应不了&#x20;
2. 使用grid 来使表格自适应宽度,在table 上加个父级div , 打上grid  给flex顶掉这样就可以了

```vue 
<div style="display: inline-grid;width: 100%;">
  <el-table :data='tableData' style='width: 100%;height: 100%;overflow: auto;'>
    <el-table-column label='编号' prop='id' width="100"></el-table-column>
    <el-table-column label='编号' prop='id' width="100"></el-table-column>
  </el-table>
</div>
```
