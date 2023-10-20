<template>
  <Navigator/>
  <div v-if="visible">
    <el-empty description="待上传排序数组"/>
  </div>
  <div v-else>
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="date" label="时间" width="180" />
      <el-table-column prop="ori_array" label="原序列" width="180" />
      <el-table-column prop="sorted_array" label="有序列" />
      <el-table-column prop="method" label="方式" />
      <el-table-column prop="algorithm" label="排序算法" />
    </el-table>
  </div>
  <br/>
  <!-- Form -->
  <el-button type="primary" round @click="dialogFormVisible = true">上传</el-button>
  <el-dialog v-model="dialogFormVisible" title="排序算法">
    <el-form :model="form">
      <el-form-item label="待排序数列" :label-width="formLabelWidth">
        <el-input v-model="form.array" autocomplete="off" />
      </el-form-item>
      <el-form-item label="排序方式" :label-width="formLabelWidth">
        <el-select v-model="form.order" placeholder="选择排序方式">
          <el-option label="升序" value="升序" />
          <el-option label="降序" value="降序" />
        </el-select>
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogFormVisible = false">Cancel</el-button>
        <el-button type="primary" @click="submit">
          Confirm
        </el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script>
import axios from 'axios';
import { reactive, ref } from 'vue'
import Navigator from "@/components/Navigator.vue";
export default {
  components: {Navigator},
  setup(){
    const visible=ref(true);
    const tableData = ref([])
    axios.post("http://localhost:8080/init").then(response=>{
      tableData.value=response.data.data;
      if(tableData.value){
        visible.value=false;
      }else{
        console.log("noData")
      }
    })
    const dialogFormVisible = ref(false);
    const formLabelWidth = '140px';
    const form = reactive({
      array:"",
      order:"",
    });
    const submit = () => {
      dialogFormVisible.value = false;
      console.log(form);
      axios.post("http://localhost:8080/sort",form).then(response=>{
        location.reload();
      })
    };
    return{
      tableData,
      form,
      dialogFormVisible,
      formLabelWidth,
      submit,
      visible
    }
  }
}
</script>
<style scoped>
.el-button--text {
  margin-right: 15px;
}
.el-select {
  width: 300px;
}
.el-input {
  width: 300px;
}
.dialog-footer button:first-child {
  margin-right: 10px;
}
</style>
