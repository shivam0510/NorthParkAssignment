<template>
  <div>
    <div class="card">
      <canvas id="fooCanvas" count="4" />

      <chartjs-bar
        v-for="(item, index) in types"
        v-bind:key="index"
        v-bind:backgroundcolor="item.bgColor"
        v-bind:beginzero="beginZero"
        v-bind:bind="true"
        v-bind:bordercolor="item.borderColor"
        v-bind:data="item.data"
        v-bind:datalabel="item.dataLabel"
        v-bind:labels="labels"
        target="fooCanvas"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      beginZero: false,
      labels: ["Junior", "Regular", "Senior","Management"],
      types: [
        {
          bgColor: "#ff80ab",
          borderColor: "#e91e63",
          data: [5082, 0, 0, 0],
          dataLabel: "Junior"
        },
        {
          bgColor: "#ea80fc",
          borderColor: "#9c27b0",
          data: [0, 10457, 0, 0],
          dataLabel: "Regular"
        },
        {
          bgColor: "#ff80cc",
          borderColor: "#e91ecc",
          data: [0, 0, 4768, 0],
          dataLabel: "Senior"
        },
        {
          bgColor: "#ea80aa",
          borderColor: "#9c27aa",
          data: [0, 0, 0, 4961],
          dataLabel: "Management"
        }
      ]
    };
  }
};
</script>