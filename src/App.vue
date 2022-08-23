<template>
  <div class="app">
    {{name}}
    <button @click="changeName('Jon')">Change name</button>
     <div class="order">
        <button @click="handleClick('title')">Order by title</button>
        <button @click="handleClick('salary')">Order by salary</button>
        <button @click="handleClick('location')">Order by location</button>
      </div>
    <JobList :jobs="jobs" :order="order"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs, ref } from 'vue';
import Job from './models/Job'
import JobList from './components/JobList.vue';
import OrderTerm from './models/OrderTerm'

export default defineComponent({
  name: 'App',
  components: { JobList },
  
  setup(){
    const person = reactive({
      name: 'Jon',
      age: 22 as number | string
    })

    const title = ref<string>('str')

    const jobs = ref<Job[]>([
      {id: 'uid1', title: 'Job 1', location: 'Location', salary: 100},
      {id: 'uid12', title: 'Job 12', location: 'Location2', salary: 1000, experience: 1},
      {id: 'uid123', title: 'Job 122', location: 'Location2', salary: 200, experience: 1}
    ])

    const order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) => {
      order.value = term
    }

    return {
      ...toRefs(person),
      title,
      jobs,
      handleClick,
      order
    }
  },

  data(){
    return {
      name: 'str',
      age: 25 as number
    }
  },

  methods:{
    changeName(name: string){
      this.name = name
    }
  }
});
</script>

<style>
header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
</style>
