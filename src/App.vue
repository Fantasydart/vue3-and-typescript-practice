<template>
  <div class="app">
    <p>Order by:</p>
    <button class="btn btn-primary" @click="handleClick('title')">title</button>
    <button class="btn btn-primary" @click="handleClick('salary')">
      salary
    </button>
    <button class="btn btn-primary" @click="handleClick('location')">
      location
    </button>
    <JobList :jobs="jobs" :order="order"/>
  </div>
</template>

<script lang="ts">
import {defineComponent, ref} from 'vue';
import Job from './types/Job';
import OrderTerm from './types/OrderTerm';
import JobList from './components/JobsList.vue';

export default defineComponent({
  name: 'App',
  components: {
    JobList,
  },
  setup() {
    const jobs = ref<Job[]>([
      {
        title: 'farm worker',
        location: 'lon lon ranch',
        salary: 3000,
        id: '1',
      },
      {title: 'fireworker', location: 'Aloha beach', salary: 8000, id: '2'},
      {title: 'developer', location: 'Bishkek', salary: 500, id: '3'},
      {title: 'streamer', location: 'New York', salary: 180000, id: '4'},
    ]);

    const order = ref<OrderTerm>('location');
    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };

    return {jobs, handleClick, order};
  },
});
</script>

<style lang="scss" scoped></style>
