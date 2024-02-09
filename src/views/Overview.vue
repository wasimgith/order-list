<template>
  <div>
    <div class="overview">Orders List</div>

    <div>
      <b-tabs content-class="mt-3">
        <div class="main" id="app">
          <div>
            <b-tab title="Provising Orders" active>
               
              <table id="table" >
                <tr style="background-color: Green">
                  <th>Item ID</th>
                  <th>Created On</th>
                  <th>Price(MRC)</th>
                  <th>Price(OTC)</th>
                  <th>Created By</th>
                  <th>Status</th>
                  <th>Action</th>
                </tr>
                <tbody>
                  <tr v-for="(user, index) in users" :key="user.id">
                    <th>{{ user.id }}</th>
                    <th>{{ user["created-on"] | formatDate}}</th>
                    <th>{{ user.currency }} {{ user.mrc }}</th>
                    <th>{{ user.currency }} {{ user.otc }}</th>
                    <th>{{ user["created-by"] }}</th>
                    <th>{{ user.status }}</th>
                    <th>
                      <button v-on:click="deleteEvent(index)">
                        Delete
                      </button>
                    </th>
                  </tr>
                  
                </tbody>
                
              </table>
              </b-tab>
          </div>
        </div>
        <b-tab title="Active orders"><p>Active orders</p></b-tab>
      </b-tabs>
    </div>
    
  </div>
</template>


<script>
import users from "./users.json";
import swal from "sweetalert2";

window.Swal = swal;

export default {
  data: () => ({
    users,
    pageSize:5,
    currentPage:1
  }),
  computed: {
    rows() {
      return this.users.length;
    },
  },
  methods: {
    deleteEvent: function (index){
      this.$swal({
        title: "Are you sure?",
        type: "warning",
        showCancelButton: true,
        confirmButtonText: "Yes Delete it!",
        cancelButtonText: "No, Keep it!",
        showCloseButton: true,
        showLoaderOnConfirm: true,
      }).then((result) => {
        if (result.value) {
         this.users.splice(index, 1);
          this.$swal(
            "Deleted",
            "You successfully deleted this file",
            "success"
          );
        } else {
          this.$swal("Cancelled");
        }
      });
    },
  },
}
</script>

<style scoped>
.overview {
  display: flex;
  height: 100%;
  width: 100%;
  font-size: 40px;
  color: rgb(167, 167, 167);
  font-weight: 600;
}
table {
  margin: 0 auto;
  font-size: large;
  border: 1px solid black;
  padding: o auto;
}
tr:hover {
  background-color: rgb(161, 161, 154);
}

h1 {
  text-align: center;
  color: #159c15;
  font-size: xx-large;
}
td {
  background-color: #ecf0e8;
  border: 1px solid black;
}

th,
td {
  font-weight: bold;
  border: 1px solid rgb(117, 14, 14);
  padding: 10px;
  text-align: center;
}

td {
  font-weight: lighter;
}
</style>

<style scoped>
td, th {
  padding: 5px;
}

th {
  cursor:pointer;
}

</style>