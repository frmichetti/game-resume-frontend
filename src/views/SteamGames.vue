<template>
  <div class="all-content">
    <Loading v-if="isLoading"></Loading>
    <div class="container py-4" v-if="!isLoading" style="margin-top: 50px">
      <div class="row align-items-end">
        <div class="col"></div>
        <div class="col"></div>
        <div class="col">
          <a type="button" class="btn btn-outline-primary" :href="`${env}/csv?table=Steam`">to CSV</a> &nbsp;
          <a type="button" class="btn btn-outline-secondary" :href="`${env}/pdf?from=steam`" target="_blank">to PDF</a> &nbsp;
          <a type="button" class="btn btn-outline-success" :href="`${env}/xls?from=steam`">to XLS</a>
        </div>
      </div>
      <div class="about">
        <h1>Steam Games Table</h1>
        <div class="table-responsive">
          <SteamGamesTable />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SteamGamesTable from "@/components/SteamGamesTable.vue";
import Loading from "@/components/Loading.vue";

export default {
  name: "SteamGames",
  components: {
    SteamGamesTable,
    Loading,
  },
  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 2000);
  },
  data() {
    return {
      env: process.env.VUE_APP_BACKEND_SERVER,
      isLoading: true,
    };
  },
};
</script>
