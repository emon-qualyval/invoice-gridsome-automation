<template>
  <v-row no-gutters class="v-application">
    <v-col cols="12" md="8">
      <div class="ml-5 mt-5 mb-5 pt-5 pb-5 white leftSide">
        <v-row no-gutters>
          <v-col cols="12" md="6" sm="5" class="left">
            <img
              class="m-3"
              src="../components/image/Amberley-Logo-blue.png"
              alt=""
            />
          </v-col>
          <v-col
            cols="12"
            md="6"
            class="headRight d-flex justify-end align-end pr-5 mb-5"
          >
            <div>
              <h5>AMBERLEY INNOVATIONS LIMITED</h5>
              <p>Amberley, First Avenue,</p>
              <p>Amersham,Buckinghamshire, United,</p>
              <p>Kingdom, HP79BL,</p>
            </div>
          </v-col>
        </v-row>
        <v-row no-gutters class="mx-auto invoiceInformation">
          <v-col cols="12" sm="5" class="ml-5 left">
            <p class="d-flex mt-5">
              <span class="mt-2">Invoice number:</span>
              <v-text-field
                md="5"
                label="Enter purchase order no"
                :rules="rules"
                hide-details="auto"
                color="success  text--lighten-1"
                class="chris pt-0 mt-0 ml-5"
                v-model="purchaseNo"
                type="number"
              />
            </p>
            <p class="d-flex mt-2">
              <span class="mt-2">Purchase order no:</span>
              <v-text-field
                md="5"
                label="Enter purchase order no"
                :rules="rules"
                hide-details="auto"
                color="success  text--lighten-1"
                class="chris pt-0 mt-0 ml-5"
                v-model="purchaseNo"
                type="number"
              />
            </p>
            <p class="mt-5 d-flex">
              <span>Issued date:</span>
              <span class="ml-5">{{
                new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
                  .toISOString()
                  .substr(0, 10)
              }}</span>
            </p>
            <p class="d-flex">
              <span class="mt-5">Due date:</span>
              <v-menu
                ref="menu"
                v-model="menu"
                :close-on-content-click="false"
                :return-value.sync="date"
                transition="scale-transition"
                offset-y
                min-width="auto"
                class="ml-5"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    v-model="date"
                    prepend-icon="mdi-calendar"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker v-model="date" no-title scrollable>
                  <v-spacer></v-spacer>
                  <v-btn text color="primary" @click="menu = false">
                    Cancel
                  </v-btn>
                  <v-btn text color="primary" @click="$refs.menu.save(date)">
                    OK
                  </v-btn>
                </v-date-picker>
              </v-menu>
            </p>
          </v-col>
          <v-col cols="12" sm="6" class="d-flex ml-10 justify-end align-end">
            <v-col cols="12" md="7" class="pt-3 pb-3 right">
              <p>Billed to</p>
              <v-text-field
                label="Enter customer name"
                :rules="clientName"
                hide-details="auto"
                color="success  text--lighten-1"
                class="chris"
                v-model="customerName"
              />
              <p>NEXT FIFTEEN COMMUNICATION GROUP PLC</p>
              <p>Bermondsey Street, London, United Kingdom</p>
            </v-col>
          </v-col>
        </v-row>
        <div class="invoice mx-auto">
          <h6>Item Details</h6>
          <table>
            <tr>
              <td>Item name</td>
              <td>Unit/Days/Hours</td>
              <td>Rate</td>
              <td>Vat</td>
              <td>Total</td>
              <td></td>
            </tr>
            <br />
            <tr class="items">
              <td>item</td>
              <td>10</td>
              <td><i class="moneySign fa fa-sterling-sign"></i>10</td>
              <td><i class="moneySign fa fa-sterling-sign"></i>0.00</td>
              <td><i class="moneySign fa fa-sterling-sign"></i>0.00</td>
              <td></td>
            </tr>
            <br />
            <tr class="addItem">
              <td>
                <v-text-field
                  label="Item name"
                  hide-details="auto"
                  class="mt-0 pt-1 pb-1 pl-2"
                  v-model="item"
                ></v-text-field>
              </td>
              <td>
                <v-text-field
                  label="unit"
                  hide-details="auto"
                  class="mt-0 pt-1 pb-1 pl-2"
                  v-model="unit"
                  type="number"
                ></v-text-field>
              </td>
              <td>
                <v-text-field
                  label="rate"
                  hide-details="auto"
                  class="mt-0 pt-1 pb-1 pl-2"
                  v-model="rate"
                  type="number"
                ></v-text-field>
              </td>
              <td>
                <select style="width: 70%" name="" id="">
                  <option value="5">5%</option>
                  <option value="12.5">12.5%</option>
                  <option selected value="20">20%</option>
                </select>
              </td>
              <td>
                <i class="moneySign fa fa-sterling-sign"></i>
                0.00
              </td>
              <td>
                <i class="plus"><span>+</span></i>
              </td>
            </tr>
            <br />
          </table>
          <v-text-field
            label="Description"
            hide-details="auto"
            class="mt-0 pt-1 pl-2 pb-1"
            style="background-color: #f3f1f1"
            v-model="description"
          ></v-text-field>
          <v-row class="d-flex mx-auto paymentMethod">
            <v-col cols="12" sm="6" class="left">
              <h6>Payment Details</h6>
              <p>Account name: <span>Amberley Innovations</span></p>
              <p>Account no: <span>6795 0463 3712 </span></p>
              <p>Routing no: <span>021000021</span></p>
            </v-col>
            <v-col cols="12" sm="6" class="d-flex mt-5 justify-end right">
              <div>
                <p>
                  Sub Total:
                  <span>
                    <i class="moneySign fa fa-sterling-sign"></i>
                    0.00
                  </span>
                </p>
                <p>
                  Total Vat:
                  <span>
                    <i class="moneySign fa fa-sterling-sign"></i>
                    0.00
                  </span>
                </p>
                <p>
                  Total Amount:
                  <span>
                    <i class="moneySign fa fa-sterling-sign"></i>
                    0.00
                  </span>
                </p>
              </div>
            </v-col>
          </v-row>
        </div>
      </div>
    </v-col>
    <v-col cols="12" md="4">
      <RightSide />
    </v-col>
  </v-row>
</template>
<script>
import "../components/css/style.css";
import RightSide from '../components/RideSide.vue'
export default {
  metaInfo: {
    title: "Invoice",
  },
  components:{
    RightSide
  },
  data: () => ({
    rules: [(value) => value != "" || "Required."],
    clientName: [(value) => value != "" || "Required."],
    date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    menu: false,
    items: ["5%", "12.5%", "20%"],
    item: "",
    unit: "",
    rate: "",
    invoiceNo: "",
    purchaseNo: "",
    customerName: "",
    description: "",
    vat: "20%",
  }),
};
</script>
