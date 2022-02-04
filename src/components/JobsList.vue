<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <ul>
      <li v-for="job in orederedJobs" :key="job.id">
        <h2>{{ job.id }}. {{ job.title }} ({{ job.location }})</h2>
        <div class="salary">
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Non ea
            eligendi veniam incidunt quas neque, veritatis id minus laboriosam
            sit laudantium, adipisci sint. Quas, dolor!
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script lang="ts">
import {defineComponent, PropType} from 'vue';
import Job from '@/types/Job';
import OrderTerm from '@/types/OrderTerm';
import {computed} from '@vue/reactivity';

export default defineComponent({
  props: {
    jobs: {
      type: Array as PropType<Job[]>,
      required: true,
    },
    order: {
      type: String as PropType<OrderTerm>,
      required: true,
    },
  },
  setup(props) {
    const orederedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return {orederedJobs};
  },
});
</script>

<style land="scss" scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}

.job-list ul {
  padding: 0;
}

.job-list li {
  list-style-type: none;
  background-color: #fff;
  padding: 40px;
  margin: 16px 0;
  border-radius: 8px;
}

.job-list h2 {
  margin: 0 0 12px;
  font-weight: bold;
  font-size: 150%;
  line-height: 1.5;
  text-transform: capitalize;
}

.salary {
  display: flex;
}

.salary img {
  width: 30px;
}

.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
</style>
