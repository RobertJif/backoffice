<template>
  <div class="animated fadeIn">
    <transition name="fade">
      <b-card no-body v-if="cards.template.active">
        <div slot="header">
          Commission Tier
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
          <b-card-body> </b-card-body>
        </b-collapse>
      </b-card>
    </transition>
  </div>
</template>

<script>
import { Callout } from "@coreui/vue";
import axios from "axios";
import _xnconvert from "@/mylib/xn-data-convert-engine";

export default {
  name: "ProductBaseTemplate",
  components: {
    Callout
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
          statusMsg: "Incompleted",
          valid: false
        }
      },
      products: [],
      validation: {},
      model: {
        id: 0,
        name: "",
        startDate: "",
        endDate: "",
        group: [
          {
            id: 0,
            formula: 0,
            base: 0,
            products: [],
            commissionTierRates: {
              tierNo: [],
              commissionBaseAmount: [],
              activeMember: [],
              rate: []
            }
          }
        ]
      }
    };
  },
  mounted() {},
  methods: {
    formatDate(strDate) {
      return _xnconvert.formatDate(new Date(strDate), "dd mmm yyyy");
    },
    checkProducts() {
      var groupval = [];
      this.model.group.forEach(group => {
        groupval = groupval.concat(group.products);
      });
      if (new Set(groupval).size !== groupval.length) {
        return true;
      } else {
        return false;
      }
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
