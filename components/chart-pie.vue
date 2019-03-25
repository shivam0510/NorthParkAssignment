<template>
  <div>
    <div class="card">
      <chartjs-doughnut
        v-bind:bind="true"
        v-bind:datasets="datasets"
        v-bind:labels="labels"
        v-bind:option="option"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
        /*sampleData:[],
    seniorCount:0,
        juniorCount:0,
      regularCount:0,
      managCount:0,*/
      //hardcoded below values after computing
      datasets: [{ 
          data: [5082, 10457, 4768,4961],
          backgroundColor: ["#b388ff", "#82b1ff", "#80d8ff","#000000"],
          hoverBackgroundColor: ["#673ab7", "#2196f3", "#03a9f4","#000000"]
        }],
      labels: ["Junior", "Regular", "Senior","Management"],
      option: {}
    };
  },

 /* created(){
      axios.get('../Sample.json')
    .then(response => {
      // JSON responses are automatically parsed.
      this.sampleData = response.data;
      for(var i=0; i< this.sampleData.length; i++){
          if(this.sampleData[i].RequestorSeniority == '1 - Junior'){
              this.juniorCount++;
          }else if(this.sampleData[i].RequestorSeniority == '2 - Regular'){
              this.regularCount++;
          }else if(this.sampleData[i].RequestorSeniority == '3 - Senior'){
              this.seniorCount++;
          }else if(this.sampleData[i].RequestorSeniority == '4 - Management'){
              this.managCount++;
          }
      }
    });
    datasets: [{ 
          data: [this.juniorCount,  this.regularCount, this.seniorCount,this.managCount],
          backgroundColor: ["#b388ff", "#82b1ff", "#80d8ff","#000000"],
          hoverBackgroundColor: ["#673ab7", "#2196f3", "#03a9f4","#000000"]
        }];
  }*/
};
</script>