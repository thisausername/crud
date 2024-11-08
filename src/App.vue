<template>
  <div class="table-box">
    <div class="title">
      <!-- 标题 -->
      <h2>CURD</h2>
    </div>

    <div class="query">
      <el-input v-model="input" style="width: 240px" placeholder="Please input" />
      <el-button type="primary">增加</el-button>
    </div>

    <div class="table">
      <el-table
        ref="multipleTableRef"
       :data="tableData"
        style="width: 100%"
        @selection-change="handleSelectionChange" border>
      <el-table-column type="selection"  width="55" />
      <el-table-column fixed prop="date" label="Date" width="150" />
      <el-table-column prop="name" label="Name" width="120" />
      <el-table-column prop="state" label="State" width="120" />
      <el-table-column prop="city" label="City" width="120" />
      <el-table-column prop="address" label="Address" width="600" />
      <el-table-column prop="zip" label="Zip" width="120" />
      <el-table-column fixed="right" label="Operations" min-width="120">
        <template #default>
          <el-button link type="primary" size="small" @click="handleClick">
            Detail
          </el-button>
          <el-button link type="primary" size="small">Edit</el-button>
        </template>
      </el-table-column>
    </el-table>
    </div>
  </div>
</template>


<script setup lang="ts">
  import { ref } from 'vue';
  //数据
  let tableData = ref([{
    date: '2016-05-03',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Home',
  },
  {
    date: '2016-05-02',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Office',
  },
  {
    date: '2016-05-04',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Home',
  },
  {
    date: '2016-05-01',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Office',
  },])

  let input = ref("");
  let multipleSelection = ref([]);

  //函数
  const handleClick = () => {
    console.log('click')
}

const handleSelectionChange = (val:[]) => {
  multipleSelection.value = val
  console.log(val)
}

</script>




<style scoped>

.table-box{
  width: 800px;
  left: 50%;
  top:30%;
  position: absolute;
  transform: translate(-50%,-50%);
}
.title{
  display: flex;
  justify-content: center;
}
.query{
  padding:0px 40px 0px 0px;
  margin: auto;
  display: flex;
  justify-content:space-between;
}

</style>
