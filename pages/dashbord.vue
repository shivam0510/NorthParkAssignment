<template>
  <form name="d" autocomplete="off">
    <!-- ticket summary part -->
    <div id="summary">
      <table width="100%">
          <tbody width="100%">
            <tr>
              <td width="20%">
                  <label for="summary" id="summary-label"><h2>Tickets Summary</h2></label>
              </td>
              <br>
              <td width="40%">
                  <ChartBar />
              </td>
              <br>
              <td width="40%">
                  <ChartPie />
              </td>
            </tr>
          </tbody>
      </table>
    </div>
    <br><br><br>
    
    <!-- tickets details in modal -->
    <div v-if="showModal == true">
      <div class="modal-backdrop">
        <div class="modal">
          <header class="modal-header">
            <slot name="header">
              Ticket Details
              <button type="button" class="btn-close" v-on:click="closeModal()">
                x
              </button>
            </slot>
          </header>
          <section class="modal-body">
            <slot name="body">
              <table>
                <tr>
                  <td><b>Ticket No: </b>{{ detailData.ticket}}</td>
                </tr>
                <tr>
                  <td><b>Requestor: </b>{{ detailData.Requestor}}</td>
                </tr>
                <tr>
                  <td><b>IT Owner: </b>{{ detailData.ITOwner}}</td>
                </tr>
                <tr>
                  <td><b>Ticket Type: </b>{{ detailData.TicketType}}</td>
                </tr>
                <tr>
                  <td><b>Severity: </b>{{ detailData.Severity}}</td>
                </tr>
                <tr>
                  <td><b>Priority: </b>{{ detailData.Priority}}</td>
                </tr>
                <tr>
                  <td><b>Days Open: </b>{{ detailData.daysOpen}}</td>
                </tr>
                <tr>
                  <td><b>Raised Date: </b>{{ detailData["Ticket Creation Date"]}}</td>
                </tr>
                <tr>
                  <td><b>Satisfaction: </b>{{ detailData.Satisfaction}}</td>
                </tr>
                <tr>
                  <td><b>Field Agent: </b>{{ detailData.FiledAgainst}}</td>
                </tr>
                <tr>
                  <td><b>Requestor Seniority: </b>{{ detailData.RequestorSeniority}}</td>
                </tr>
              </table>
            </slot>
          </section>
          <footer class="modal-footer">
            <slot name="footer">
              <button type="button" class="btn-green" v-on:click="closeModal()">
                Close me!
              </button>
            </slot>
          </footer>
        </div>
      </div>
    </div>

    <!-- table for ticket details -->
    <div id="ticketDetails">
      <br><br>
      <table width="100%">
        <tr>
          <td width="20%">
            <h2>Search Ticket</h2>
          </td>
          <td width="10%"></td>
          <td width="40%">
            <input type="text" id="searchID" v-model="search" placeholder="Search Ticket Number"/>
          </td>
          <td width="10%"></td>
          <td width="10%"><input type="button" value="search" v-on:click="searchElement()"></td>
          <td width="10%"></td>
        </tr>
      </table>      
      <br>
      <br>
      <h2 style="text-align:center">Ticket Detials</h2>
      <br>
      <br>
      <table width="100%">
        <thead width="100%">
          <tr>
            <td><b>Ticket number</b></td>
            <td><b>Requestor</b></td>
            <td><b>IT owner</b></td>
            <td><b>Ticket type</b></td>
            <td><b>Severity</b></td>
            <td><b>Priority</b></td>
            <td><b>Days open</b></td>
            <td><b>Creation Date</b></td>
            <td></td>
          </tr>
        </thead>
        <tbody width="100%">
            <tr v-for="(item,index) in sampleData" :key="index">
              <td>{{ item.ticket}}</td>
              <td>{{ item.Requestor}}</td>
              <td>{{ item.ITOwner}}</td>
              <td>{{ item.TicketType}}</td>
              <td>{{ item.Severity}}</td>
              <td>{{ item.Priority}}</td>
              <td>{{ item.daysOpen}}</td>
              <td>{{ item["Ticket Creation Date"]}}</td>
              <!--<td><img src="assets/infromation.png"></td>-->
              <td><input type="button" value="+" v-on:click="getDetails(item)"></td>
            </tr>
        </tbody>
      </table>
    </div>
  </form>
</template>

<script>
import axios from 'axios'
import ChartBar from "@/components/chart-bar";
import ChartPie from "@/components/chart-pie";

export default {

methods:{
  //method to search element
  searchElement(){
    for(var i=0; i< this.sampleData.length; i++){
      if(this.sampleData[i].ticket == this.search){
        this.detailData = this.sampleData[i];
        this.showModal = true;
        return;
      }
    }
  },
  
  //method for retirving item details on expansion
  getDetails(item){
    this.detailData = item;
    this.showModal = true;
    return;
  },

  //closing the modal
  closeModal() {
    this.showModal = false;      
  },
},

data() {
    return {
      sampleData: [],
      errors: [],
      search: '',
      showModal: false,
      detailData: [],
    }
  },

  // Fetches posts when the component is created.
  created() {
    axios.get('../Sample.json')
    .then(response => {
      // JSON responses are automatically parsed.
      this.sampleData = response.data
      //console.log(this.sampleData)
    })
    .catch(e => {
      this.errors.push(e)
    });
  },
  components: {
    ChartBar,
    ChartPie,
   // Modal,
  }
}
</script>

<style>

.loginHeading {
  font: 28px/1.1 Georgia,serif;
    color: #000;
    padding: 18px 0 0;
    margin: 20px 0;
    border-bottom: 1px solid black;
    padding-bottom: 20px;
}

div {
  display : block;
}

#loginBlock {
  width: 380px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -200px 0 0 -140px;
  font-size: larger;
}

input {
  width: 100%;
}

.modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    border-bottom: 1px solid #eeeeee;
    color: #4AAE9B;
    justify-content: space-between;
  }

  .modal-footer {
    border-top: 1px solid #eeeeee;
    justify-content: flex-end;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #4AAE9B;
    border: 1px solid #4AAE9B;
    border-radius: 2px;
  }

</style>

