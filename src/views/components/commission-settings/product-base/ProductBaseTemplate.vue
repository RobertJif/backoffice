<template>
  <div class="animated fadeIn">
    <transition name="fade">
      <b-card no-body v-if="cards.template.active">
        <div slot="header">
          Product Groups
          <div class="card-header-actions">
            <b-link
              class="card-header-action btn-minimize"
              v-b-toggle.collapseproductbase
            >
              <i class="icon-arrow-up"></i>
            </b-link>
          </div>
          <div class="card-header-actions">
            <b-badge :variant="cards.template.variant">{{
              cards.template.statusMsg
            }}</b-badge
            >&nbsp;
          </div>
        </div>
        <b-collapse id="collapseproductbase" visible>
          <b-card-body>
            <b-button variant="primary" @click="addProductGroup"
              >Add Group</b-button
            >
            <br /><br />
            <product-group
              v-for="(group, i) in model.group"
              :group="group"
              :groupNo="i"
              :key="i"
              :checkProducts="checkProducts"
              :removeGroup="removeGroup"
            ></product-group>
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
import ProductGroup from "./ProductGroup";

export default {
  name: "ProductBaseTemplate",
  components: {
    Callout,
    ProductGroup
  },
  props: {
    template: Object
  },
  watch: {},
  data: function() {
    return {
      cards: {
        template: {
          active: true,
          variant: "danger",
          statusMsg: "Incompleted"
        }
      },
      products: [],
      validation: {},
      model: {
        id: 0,
        name: "",
        startDate: "",
        endDate: "",
        valid: false,
        group: [
          {
            show: true,
            id: 0,
            formula: 0,
            base: 0,
            products: [],
            productsState: null,
            groupState: null,
            tierState: null,
            commissionTierRates: [
              {
                tierNo: 0,
                commissionBaseAmount: 0,
                activeMember: 0,
                rate: 0,
                state: null
              }
            ]
          }
        ]
      }
    };
  },
  mounted() {},
  methods: {
    addProductGroup() {
      this.model.group.push({
        show: true,
        id: 0,
        formula: 0,
        base: 0,
        products: [],
        productsState: null,
        groupState: null,
        tierState: null,
        commissionTierRates: [
          {
            tierNo: 0,
            commissionBaseAmount: 0,
            activeMember: 0,
            rate: 0,
            state: null
          }
        ]
      });
    },
    removeGroup(index) {
      if (
        confirm(
          "Remove Product Group " +
            (index + 1) +
            "?\nYou cannot undo this action."
        )
      ) {
        this.model.group.splice(index, 1);
      }
    },
    formatDate(strDate) {
      return _xnconvert.formatDate(new Date(strDate), "dd mmm yyyy");
    },
    checkProducts() {
      var groupval = [];
      var groupNotValid = false;
      var productNotValid = false;
      this.model.group.forEach(group => {
        groupval = groupval.concat(group.products);
        if (!group.valid) {
          groupNotValid = true;
        }
      });
      if (new Set(groupval).size !== groupval.length) {
        productNotValid = true;
      }
      return productNotValid;
    }
  },
  computed: {
    parentValue() {
      this.model.name = this.template.name;
      this.model.startDate = this.template.startDate;
      this.model.endDate = this.template.endDate;
    }
  }
};
</script>
