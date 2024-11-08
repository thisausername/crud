<template>
  <div class="table-box">
    <div class="title">
      <!-- 标题 -->
      <h2>CURD</h2>
    </div>

    <div class="query">
      <el-input v-model="input" style="width: 240px" placeholder="请输入姓名" />
      <el-button type="primary" @click="handleAdd">增加</el-button>
    </div>

    <div class="table">
      <el-table
        ref="multipleTableRef"
       :data="tableData"
        style="width: 100%"
        @selection-change="handleSelectionChange" border>
      <el-table-column type="selection"  width="40" />
      <el-table-column fixed prop="name" label="姓名" width="150" />
      <el-table-column prop="phone" label="电话" width="120" />
      <el-table-column prop="email" label="邮箱" width="120" />
      <el-table-column prop="state" label="状态" width="120" />
      <el-table-column prop="address" label="地址" width="120" />
      <el-table-column fixed="right" label="操作" min-width="120">
        <template #default>
          <el-button link type="primary" size="small" @click="handleClick">
            删除
          </el-button>
          <el-button link type="primary" size="small">
            修改
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    </div>
  </div>

  <div class="dialog">
    <el-dialog v-model="dialogFormVisible" title="Shipping address" width="500">
    <el-form :model="dialogForm">
      <el-form-item label="姓名" :label-width="100">
        <el-input v-model="dialogForm.name" autocomplete="off" />
      </el-form-item>
      <el-form-item label="电话" :label-width="100">
        <el-input v-model="dialogForm.phone" autocomplete="off" />
      </el-form-item>
      <el-form-item label="邮箱" :label-width="100">
        <el-input v-model="dialogForm.email" autocomplete="off" />
      </el-form-item>
      <el-form-item label="状态" :label-width="100">
        <el-input v-model="dialogForm.state" autocomplete="off" />
      </el-form-item>
      <el-form-item label="地址" :label-width="100">
        <el-input v-model="dialogForm.address" autocomplete="off" />
      </el-form-item>
    </el-form>
    <template #footer>
      <div class="dialog-footer">
        <el-button @click="dialogFormVisible = false">
          取消
        </el-button>
        <el-button type="primary" @click="dialogFormVisible = false">
          确认
        </el-button>
      </div>
    </template>
  </el-dialog>
  </div>
</template>


<script setup lang="ts">
  import { ref } from 'vue';
  //数据
  let tableData = ref([{
    name: '张三',
    phone: '10086',
    email: '123@qq.com',
    state: '离线',
    address: '地球',
  }])
  let dialogForm = ref({
    name: "",
    phone: "",
    email: "",
    state: "",
    address: "",
  })

  let input = ref("");
  let multipleSelection = ref([]);
  let dialogFormVisible = ref(false);
  //函数
  const handleClick = () => {
    console.log('click')
}

const handleSelectionChange = (val:[]) => {
  multipleSelection.value = val
  console.log(val)
}
const handleAdd = ()=>{
  dialogFormVisible.value = true;
}
</script>




<style scoped>

.table-box{
  width: 800px;
  margin: 200px;
}
.title{
  display: flex;
  justify-content: center;
}
.query{
  padding:0px 40px 10px 0px;
  margin: auto;
  display: flex;
  justify-content:space-between;
}

</style>
