<template>
  <main>
    <SiteNavigation />
    <div v-if="data != null">
      <TableView :data="data" />
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";
import SiteNavigation from "../components/Site-Navigation.vue";
import TableView from "../components/Table-View.vue";

const data = ref(null);

const getData = () => {
  axios
    .get("http://localhost:3030/index")
    .then((res) => {
      if (res.status === 201) {
        data.value = res.data.hits.hits;
      }
    })
    .catch((err) => {
      console.log(err);
    });
};
getData();
</script>
