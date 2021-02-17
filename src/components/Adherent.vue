<template>
  <td><input type="checkbox" /></td>
  <td v-for="adherentInfo in adherent" v-bind:key="adherentInfo">
    {{ showInfos(adherentInfo) }}
  </td>
  <svg
    class="edit-pen"
    viewBox="0 0 8 8"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M4.54201 1.45749L6.54232 3.4578L2.19872 7.8014L0.415287 7.99827C0.176537 8.02468 -0.0251819 7.8228 0.00138063 7.58405L0.199818 5.79936L4.54201 1.45749ZM7.77951 1.15968L6.84029 0.220459C6.54732 -0.0725098 6.07216 -0.0725098 5.77919 0.220459L4.8956 1.10405L6.89591 3.10436L7.77951 2.22077C8.07247 1.92765 8.07247 1.45265 7.77951 1.15968Z"
      fill="black"
    />
  </svg>
</template>

<script>
export default {
  name: "Adherent",
  props: {
    adherent: Object,
  },
  methods: {
    showInfos(adherentInfo) {
      if (Array.isArray(adherentInfo)) return adherentInfo.join();
      else return adherentInfo;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.edit-pen {
  position: absolute;
  width: 10px;
  display: none;
}
</style>
