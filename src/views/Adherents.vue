<template>
  <div class="adherents">
    <div class="table-header">
      <h1>Liste de tous les adhérents</h1>
      <a href="new" class="btn-new btn btn-accent btn-icon-plus"
        >Ajouter nouveau</a
      >
    </div>
    <div v-if="adherents[0]" class="table-wrapper">
      <table>
        <thead>
          <tr>
            <th><input type="checkbox" /></th>
            <th
              v-for="userKeys in Object.keys(adherents[0])"
              v-bind:key="userKeys"
            >
              {{ userKeys }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            class="inner-row"
            v-for="adherent in adherents"
            v-bind:key="adherent"
          >
            <Adherent :adherent="adherent"> </Adherent>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import AdherentDataService from "../services/AdherentDataService";
import Adherent from "../components/Adherent";
export default {
  name: "Adherents",
  components: {
    Adherent,
  },
  data() {
    return {
      adherents: [],
      page: 1,
      totalPages: 0,
      pageSize: 10,
    };
  },
  methods: {
    getRequestParams(page, pageSize) {
      let params = {};
      if (page) params["page"] = page;
      if (pageSize) params["size"] = pageSize;
      return params;
    },
    retrieveAdherents() {
      const params = this.getRequestParams(this.page, this.pageSize);

      AdherentDataService.getAll(params)
        .then((response) => {
          const { adherents, totalPages } = response.data;
          adherents.forEach((adherent) => {
            this.adherents.push(adherent);
          });
          this.totalPages = totalPages;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    scroll() {
      window.addEventListener("scroll", () => {
          let bottomOfWindow =
            document.documentElement.scrollTop ||
            document.body.scrollTop + document.documentElement.offsetHeight ===
              document.documentElement.scrollHeight;
          if (bottomOfWindow && (this.page <= this.totalPages)) {
            console.log("scroll");
            this.retrieveAdherents();
            this.page++;
            bottomOfWindow = false;
          }
      });
    },
  },
  mounted() {
    this.retrieveAdherents();
    this.scroll();
  },
};
</script>

<style scoped>
.btn-new {
  margin-left: auto;
}
</style>