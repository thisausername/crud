<template>
  <div class="table-box">
    <div class="title">
      <!-- 标题 -->
      <h2>CURD</h2>
    </div>

    <div class="query">
      <el-input v-model="input" style="width: 240px" placeholder="请输入姓名" @input="search"/>
      <span>
        <el-button type="primary" @click="handleAdd">增加</el-button>
        <el-button type="danger" @click="handleDelList" v-show="multipleSelection.length>0">删除</el-button>
      </span>
      
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
      <el-table-column prop="address" label="地址" width="300" />
      <el-table-column fixed="right" label="操作" min-width="120">
        <template #default="scope">
          <el-button link type="primary" size="small" @click="handleRowDel(scope.row)" style="color:#F56C6C">
            删除
          </el-button>
          <el-button link type="primary" size="small" style="color:#409EFF" @click="handleEdit(scope.row)">
            编辑
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    </div>
  </div>

  <div class="dialog">
    <el-dialog v-model="dialogFormVisible" :title="dialogTitle==='add'?'增加':'编辑'" width="500">
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
        <el-button type="primary" @click="dialogconfirm">
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
    id:"1",
    name: '张三',
    phone: '10086',
    email: '123@qq.com',
    state: '离线',
    address: '地球',
  },{
    id:"2",
    name: '李三',
    phone: '10086',
    email: '123@qq.com',
    state: '离线',
    address: '地球',
  },{
    id:"3",
    name: '王三',
    phone: '10086',
    email: '123@qq.com',
    state: '离线',
    address: '地球',
  }])
  let dialogForm = ref({
    id:"",
    name: "aa",
    phone: "",
    email: "",
    state: "",
    address: "",
  })

  let input = ref("");
  let multipleSelection =ref<Object[]>([]);
  let dialogFormVisible = ref(false);
  let dialogTitle = ref("");
  let dialogState = ref(true);
  let editIndex = ref("");

  let tableDataCopy = ref([{
    id:"1",
    name: '张三',
    phone: '10086',
    email: '123@qq.com',
    state: '离线',
    address: '地球',
  },{
    id:"2",
    name: '李三',
    phone: '10086',
    email: '123@qq.com',
    state: '离线',
    address: '地球',
  },{
    id:"3",
    name: '王三',
    phone: '10086',
    email: '123@qq.com',
    state: '离线',
    address: '地球',
  }])


  //函数
 


  //增加数据
const handleAdd = ()=>{
  dialogFormVisible.value = true;
  dialogState.value = true;
  dialogTitle.value = "add";
  dialogForm.value = {
    id:"",
    name: "",
    phone: "",
    email: "",
    state: "",
    address: "",
  }
}

const dialogconfirm = ()=>{
  dialogFormVisible.value = false;
  if(dialogState.value){
     //拿数据
  //添加到数组中
  tableData.value.push({
    id: (tableData.value.length+1).toString(),
    name: dialogForm.value.name,
    phone: dialogForm.value.phone,
    email: dialogForm.value.email,
    state: dialogForm.value.state,
    address: dialogForm.value.address,
  })
  }else{
    let index = tableData.value.findIndex(item=>item.id===dialogForm.value.id)
    tableData.value[index] = dialogForm.value;
  }
  tableDataCopy.value = tableData.value; 
  console.log(tableDataCopy);
}


//删除数据
const handleRowDel=({id}:any) => {
    console.log(id)

    let index = tableData.value.findIndex(item=>item.id===id)
    tableData.value.splice(index,1)
    tableDataCopy.value = tableData.value; 
}

//选中
const handleSelectionChange = (val: any[]) => {
multipleSelection.value = [];
val.forEach((item: { id: any; }) =>{
  multipleSelection.value.push(item.id)
})

}
//多删
const handleDelList =()=>{
  multipleSelection.value.forEach(id=>{
    handleRowDel(id);
  })
  multipleSelection.value = [];
}

//改
const handleEdit = (row:any)=>{
  dialogTitle.value = "edit";
  dialogState.value = false;
  dialogFormVisible.value = true;

  dialogForm.value = {
    id:`${row.id}`,
    name: `${row.name}`,
    phone: `${row.phone}`,
    email: `${row.email}`,
    state: `${row.state}`,
    address: `${row.address}`,
  }
  editIndex.value = row.id;
}

//查
const search = (val:any)=>{
  tableData.value = tableDataCopy.value
  if(val.length>0){
    tableData.value = tableData.value.filter(item=>item.name.match(val));

  }else{
    tableData.value = tableDataCopy.value;
    
  }
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
  padding:0px 0px 10px 0px;
  margin: auto;
  display: flex;
  justify-content:space-between;
}

</style>
