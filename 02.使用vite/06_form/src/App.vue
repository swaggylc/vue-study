<template>
  <h1>hello vue</h1>
  <!-- 可以将组件中的方法以自定义事件的形式发送给其他的组件 -->
  <studentList />
  <hr>
  <studentForm />
</template>

<script setup>
import studentList from './components/studentList.vue';
import { ref, provide } from 'vue';
import studentForm from './components/studentForm.vue';

/**
 * 依赖注入
 *    -通过依赖注入，可以跨越多层组件向其他组件传递数据
 *    -步骤：
 *      -1、设置依赖（provide） provide('name','value')
 *      -2、输入数据 (inject) const value = inject('name',defaultValue)
 */


// 发送请求向服务器加载数据
const STU_ARR = ref([
  {
    id: 1,
    name: '孙悟空',
    age: 18,
    gender: '男',
    address: '花果山水帘洞'
  },
  {
    id: 2,
    name: '猪八戒',
    age: 28,
    gender: '男',
    address: '高老庄'
  }, {
    id: 3,
    name: '沙和尚',
    age: 38,
    gender: '男',
    address: '流沙河'
  }, {
    id: 4,
    name: '唐僧',
    age: 20,
    gender: '男',
    address: '东土大唐'
  }
])

// 添加一个删除学生的方法
const delStudentByIndex = (index) => {
  STU_ARR.value.splice(index, 1)
  // console.log('删除学生的方法被调用了')
}

// 添加学生的方法
const addNewStudent = (newStu) => {
  const lastId = STU_ARR.value.at(-1)?.id
  const newId = !isNaN(lastId) ? lastId + 1 : 1
  newStu.id = newId
  // console.log(id);
  // console.log(newStu);
  // 调用方法，将newStu添加到数组中
  STU_ARR.value.push(newStu)
}


provide('student', {
  students: STU_ARR,
  delStudentByIndex,
  addNewStudent
})






</script>

<style lang="css" scoped></style>