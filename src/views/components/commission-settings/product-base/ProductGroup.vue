<template>
  <div class="animated fadeIn">
    <transition name="fade">
      <b-card no-body>
        <div slot="header">
          <b-row>
            <b-col sm="1">Product Group {{ groupNo + 1 }}</b-col>
            <b-col>
              <b-form-checkbox-group
                switches
                v-model="group.products"
                :options="products"
                value-field="id"
                text-field="code"
                :state="group.groupState"
              >
              </b-form-checkbox-group
            ></b-col>
            <b-col>
              <div class="card-header-actions">
                <b-link
                  href="#"
                  class="card-header-action btn-close"
                  @click="removeGroup(groupNo)"
                >
                  <i class="icon-close"></i>
                </b-link>
                <b-link
                  class="card-header-action btn-minimize"
                  @click="group.show = !group.show"
                >
                  <i
                    :class="
                      group.show == true ? 'icon-arrow-up' : 'icon-arrow-down'
                    "
                  ></i>
                </b-link>
              </div>
              <div class="card-header-actions">
                <b-badge :variant="cards.template.variant">{{
                  cards.template.statusMsg
                }}</b-badge
                >&nbsp;
              </div>
            </b-col>
          </b-row>
        </div>
        <b-collapse v-show="group.show" :id="'tier' + groupNo" visible>
          <b-card-body>
            <b-row>
              <b-col>
                <label>Formula Group</label>
                <b-form-select
                  v-model="group.formula"
                  :options="formulas"
                  value-field="id"
                  text-field="name"
                ></b-form-select
              ></b-col>
              <b-col>
                <label>Commission Base</label>
                <b-form-select
                  v-model="group.base"
                  :options="bases"
                  value-field="id"
                  text-field="name"
                ></b-form-select
              ></b-col>
            </b-row>
            <br />
            <b-row>
              <b-col>
                <label>Fee Group</label>
                <b-form-input type="text" readonly=""></b-form-input>
              </b-col>
              <b-col>
                <label>Discount Group</label>
                <b-form-input type="text" readonly=""></b-form-input>
              </b-col>
            </b-row>
            <br />
            <b-row>
              <b-col>
                <b-button variant="primary" @click="addTierRates"
                  >Add Tier</b-button
                ></b-col
              >
            </b-row>
            <br />

            <b-card>
              <b-table
                id="tmpl-table"
                :items="group.commissionTierRates"
                :fields="fields"
                bordered
                hover
              >
                <template v-slot:table-colgroup="scope">
                  <col v-for="field in scope.fields" :key="field.key" />
                </template>

                <template slot="index" slot-scope="data">
                  {{ data.index + 1 }}
                </template>

                <template slot="base" slot-scope="data">
                  <b-form-input
                    type="number"
                    v-model.number="data.item.commissionBaseAmount"
                    step="0.000001"
                    min="0.000000"
                    max="100000000000000000000.000000"
                    :state="data.item.state"
                    @keyup="checkNumber"
                  ></b-form-input>
                </template>

                <template slot="activeMember" slot-scope="data">
                  <b-form-input
                    type="number"
                    v-model.number="data.item.activeMember"
                    step="0.000001"
                    min="0.000000"
                    max="100000000000000000000.000000"
                    :state="data.item.state"
                    @keyup="checkNumber"
                  ></b-form-input>
                </template>

                <template slot="rates" slot-scope="data">
                  <b-form-input
                    type="number"
                    v-model.number="data.item.rate"
                    step="0.000001"
                    min="0.000000"
                    max="100000000000000000000.000000"
                    :state="data.item.state"
                    @keyup="checkNumber"
                  ></b-form-input>
                </template>
                <template slot="action" slot-scope="data">
                  <button
                    class="btn btn-danger"
                    @click="removeTierRates(data.index)"
                  >
                    Remove
                  </button>
                </template>
              </b-table>
            </b-card>
          </b-card-body>
        </b-collapse>
      </b-card>
    </transition>
  </div>
</template>

<script>
import { Callout } from "@coreui/vue";
import axios from "axios";
import _xnconvert from "@/mylib/xn-data-convert-engine";
import CommissionTier from "./CommissionTier";

export default {
  name: "ProductGroup",
  components: {
    Callout,
    CommissionTier
  },
  props: {
    group: Object,
    groupNo: Number,
    checkProducts: Function,
    removeGroup: Function
  },
  data: function() {
    return {
      fields: [
        { key: "index", label: "Tier No." },
        { key: "base", label: "Commission Base Amount" },
        { key: "activeMember", label: "Active Member" },
        { key: "rates", label: "Percentages" },
        { key: "action", label: "" }
      ],
      cards: {
        template: {
          active: true,
          variant: "danger",
          statusMsg: "Incompleted",
          valid: false
        }
      },
      products: [],
      formulas: [
        {
          id: 0,
          name: "Default"
        }
      ],
      bases: [
        {
          id: 0,
          name: "Gross Revenue"
        },
        {
          id: 1,
          name: "Turnover"
        }
      ],
      validation: {}
    };
  },
  watch: {
    "group.products": {
      handler: function(val, oldVal) {
        if (val != oldVal && oldVal != null) {
          this.checkNumber();
          if (this.group.productsState && this.group.tierState) {
            this.group.groupState = true;
          } else {
            this.group.groupState = false;
          }
        }
      },
      deep: true
    },

    "group.groupState": {
      handler: function(val, oldVal) {
        if (val) {
          console.log("success");
          this.cards.template.variant = "success";
          this.cards.template.statusMsg = "Completed";
        } else {
          console.log("fail");
          this.cards.template.variant = "danger";
          this.cards.template.statusMsg = "Incompleted";
        }
      },
      deep: true
    }
  },
  mounted() {
    axios
      .all([
        axios.get(
          process.env.VUE_APP_AFFILIATE_API_URL + "product-management/products"
        )
      ])
      .then(
        axios.spread(productRes => {
          this.products = productRes.data;
        })
      )
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
    addTierRates() {
      this.group.commissionTierRates.push({
        tierNo: 0,
        commissionBaseAmount: 0,
        activeMember: 0,
        rate: 0,
        state: true
      });
    },
    removeTierRates(index) {
      if (
        confirm(
          "Remove Commission Tier " +
            (index + 1) +
            "?\nYou cannot undo this action."
        )
      ) {
        this.group.commissionTierRates.splice(index, 1);
      }
    },
    formatDate(strDate) {
      return _xnconvert.formatDate(new Date(strDate), "dd mmm yyyy");
    },
    checkNumber() {
      this.group.tierState = true;
      this.group.commissionTierRates.forEach((tier, index) => {
        if (
          isNaN(parseInt(tier.commissionBaseAmount)) ||
          isNaN(parseInt(tier.activeMember)) ||
          isNaN(parseInt(tier.rate))
        ) {
          this.group.commissionTierRates[index].state = false;
          this.group.tierState = false;
        }
        this.group.commissionTierRates[index].state = true;
      });
      this.group.productsState = !this.checkProducts();

      if (this.group.productsState && this.group.tierState) {
        this.group.groupState = true;
      } else {
        this.group.groupState = false;
      }
    }
  },
  computed: {}
};
</script>
