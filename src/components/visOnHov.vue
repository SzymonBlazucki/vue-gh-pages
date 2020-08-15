<template>
  <div>
    <svg
      width="300"
      height="100"
    >
      <circle
        cx="50"
        cy="50"
        r="40"
        class="light-blob"
        :fill="colorBefore"
      />
      <circle
        cx="150"
        cy="50"
        r="40"
        class="light-blob"
        :fill="colorAfter"
      />
    </svg>
    <br>
    <svg
      width="400"
      height="100"
      class="back"
    >
      <path
        d="m0 50 l 200 0"
        :stroke="colorBefore"
        stroke-width="20"
        opacity="0.5"
      />
      <path
        d="m200 50 l 200 0"
        :stroke="colorAfter"
        stroke-width="20"
        opacity="0.5"
      />
      <path
        d="m0 50 l 200 0"
        :stroke="colorBefore"
        stroke-width="10"
      />
      <path
        d="m200 50 l 200 0"
        :stroke="colorAfter"
        stroke-width="10"
      />
      <rect
        :x="200 - 15"
        width="30"
        height="100"
        rx="5"
        ry="5"
        fill="blue"
        stroke-width="0"
      />
      <text
        :x="200 - 15"
        y="54"
        fill="white"
      >Op</text>
    </svg>
  </div>
</template>

<script lang="ts">


function giveColor(arr){
  const a = arr.map((d) => Math.round(2 * d * 255));
  return `rgb(${a.join(',')})`;
}

export default  {
  components: {
  },
  props: {
    hover: Array,
    leftBeam: Array

  } ,
      

  data: function() {
      return {
      colorAfter: giveColor(this.hover),
      colorBefore: giveColor(this.leftBeam)
  }},
  methods: {}
}

</script>

<style>
.light-blob {
    opacity: 0.2
}
.light-blob:hover {
    opacity: 1 
}
.back {
  background-color:#000000
}

</style>