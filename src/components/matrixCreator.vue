<template>
  <div>
    test 123 {{ rowValues }}
    <table style="width:30%">
      <tr>
        <th />
        <th>R</th>
        <th>G</th>
        <th>B</th>
      </tr>
      <tr>
        <td>
          <b>R</b>
        </td>
        <td
          v-for="(rowValue, number) in redValues"
          :key="rowValue"
        >
          <div class="box">
            <input
              v-model="redValues[number]"
              @input="clearErrorMsg"
            >
            <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
          </div>
          <vue-slider
            v-model="redValues[number]"
            v-bind="options"
            :tooltip="options.errorMsg ? 'none' : 'always'"
            @error="error"
            @change="clearErrorMsg"
          />
        </td>
      </tr>
      <tr>
        <td>
          <b>G</b>
        </td>
        <td
          v-for="(rowValue, number) in greenValues"
          :key="rowValue"
        >
          <div class="box">
            <input
              v-model="greenValues[number]"
              @input="clearErrorMsg"
            >
            <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
          </div>
          <vue-slider
            v-model="greenValues[number]"
            v-bind="options"
            :tooltip="options.errorMsg ? 'none' : 'always'"
            @error="error"
            @change="clearErrorMsg"
          />
        </td>
      </tr>
      <tr>
        <td>
          <b>B</b>
        </td>
        <td
          v-for="(rowValue, number) in blueValues"
          :key="rowValue"
        >
          <div class="box">
            <input
              v-model="blueValues[number]"
              @input="clearErrorMsg"
            >
            <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
          </div>
          <vue-slider
            v-model="blueValues[number]"
            v-bind="options"
            :tooltip="options.errorMsg ? 'none' : 'always'"
            @error="error"
            @change="clearErrorMsg"
          />
        </td>
      </tr><tr />
    </table>
    <mat
      :key="value"
      :initial="[1/3, 1/3, 1/3]"
      :matr="createMatrix(redValues, greenValues, blueValues)"
    />
  </div>
</template>

<script lang="ts">
// eslint-disable-next-line no-unused-vars
import { Cx } from "quantum-tensors";
import { MatrixViewer } from "bra-ket-vue";
import VueSlider from "vue-slider-component";
import "vue-slider-component/theme/default.css";

const ERROR_TYPE = {
  VALUE: 1,
  INTERVAL: 2,
  MIN: 3,
  MAX: 4,
  ORDER: 5,
};

function check (number){
  if (number == 0) return 'R';
  else if (number == 1) return 'G';
  else if (number == 2) return 'B';
}

function mergeRow(colour, data){
      const row = [];
      for(let i=0; i<data.length; i++){
        row.push([colour, check(i), Cx(data[i])])
      }
      return row;
    }

export default {
  components: {
    VueSlider,
    // eslint-disable-next-line vue/no-unused-components
    mat: () => import("../components/mat.vue"),
  },
  props: {
    MatrixViewer,
  },

  data: function () {
    return {
      redValues: [1,1,1],
      greenValues: [1,1,1],
      blueValues: [1,1,1],
      options: {
        min: 0,
        max: 1,
        errorMsg: "",
        interval: 0.01,
        marks: [0, 1],
      },
      button: 0,
      value: 0
    };
  },
  methods: {
    error(type, msg) {
      switch (type) {
        case ERROR_TYPE.MIN:
          break;
        case ERROR_TYPE.MAX:
          break;
        case ERROR_TYPE.VALUE:
          break;
      }
      this.options.errorMsg = msg;
    },
    clearErrorMsg() {
      this.options.errorMsg = "";
    },
    
    createMatrix(R, G, B){
      const matrix = [];
      this.value = this.redValues.concat(this.greenValues, this.blueValues).reduce((a,b) => a+b, 0)
    return matrix.concat(mergeRow('R', R), mergeRow('G', G), mergeRow('B', B))
    }
  },
};
</script>