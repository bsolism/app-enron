<template>
  <div class="top-4 bg-center text-center text-white">
    <h3>Email Indexed</h3>
  </div>
  <div class="pt-2 mb-8 relative">
    <input
      type="text"
      v-model="search"
      @input="getResult"
      placeholder="Search"
      class="px-1 w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none text-white"
    />
  </div>
  <div class="h-[70vh] flex">
    <div class="w-[100vh] md:h-full overflow-auto">
      <table
        id="email-Enron"
        class="table-fixed w-full cursor-pointer text-white text-xs ml-2"
        v-if="data != null"
      >
        <thead>
          <tr>
            <th class="px-4 py-2">Subject</th>
            <th>From</th>
            <th>To</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="dat in dtaTable"
            :key="dat._id"
            v-on:click="showMessage(dat)"
          >
            <td>{{ dat._source.Subject }}</td>
            <td>{{ dat._source.From }}</td>
            <td>{{ dat._source.To }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="h-[70vh] flex">
      <ShowMessage v-bind:msg="msg2" />
    </div>
  </div>
</template>

<script setup>
import ShowMessage from "../components/Show-Message.vue";
import { ref } from "vue";

const search = ref("");
const dtaTable = ref(null);

const props = defineProps(["data"]);

dtaTable.value = props.data;

const msg2 = ref(null);

const showMessage = (data) => {
  msg2.value = data._source.Message;
};

const getResult = () => {
  const dtaFilter = props.data.filter(
    (x) =>
      x._source.Subject.toLowerCase().includes(search.value) ||
      x._source.From.toLowerCase().includes(search.value) ||
      x._source.To.toLowerCase().includes(search.value) ||
      x._source.Message.toLowerCase().includes(search.value)
  );

  dtaTable.value = dtaFilter;
};
</script>
