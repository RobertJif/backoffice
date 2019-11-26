<template>
  <div class="animated fadeIn">
    <b-card class="animated fadeIn">
      <b-row>
        <b-col sm="12" md="12">
          <transition name="fade">
            <b-card no-body v-if="cards.template.active">
              <div slot="header">
                Template Details
                <div class="card-header-actions">
                  <b-link
                    class="card-header-action btn-minimize"
                    v-b-toggle.collapsetemplate
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
              <b-collapse id="collapsetemplate" visible>
                <b-card-body>
                  <b-row>
                    <b-col>
                      <label>Template Name</label>
                      <b-form-input
                        type="text"
                        v-model="model.name"
                        placeholder="Template Name"
                        v-on:keyup="checkName"
                        :state="validation.name.state"
                      ></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback">
                        {{ validation.name.msg }}
                      </b-form-invalid-feedback>
                    </b-col>
                    <b-col>
                      <label>Category</label>
                      <b-form-select
                        v-model="category"
                        :options="categories"
                        value-field="id"
                        text-field="name"
                        v-on:change="checkCategory"
                        :state="validation.category.state"
                      ></b-form-select>
                      <b-form-invalid-feedback id="input-live-feedback">
                        {{ validation.category.msg }}
                      </b-form-invalid-feedback></b-col
                    >
                  </b-row>
                  <br />
                  <b-row>
                    <b-col
                      ><label>Effective Date From</label
                      ><b-form-input
                        type="date"
                        v-model="model.startDate"
                        v-on:change="checkDate"
                        :state="validation.startDate.state"
                      ></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback">
                        {{ validation.startDate.msg }}
                      </b-form-invalid-feedback></b-col
                    >
                    <b-col>
                      <label>Effective Date To</label
                      ><b-form-input
                        type="date"
                        v-model="model.endDate"
                        v-on:change="checkDate"
                        :state="validation.endDate.state"
                      ></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback">
                        {{ validation.endDate.msg }}
                      </b-form-invalid-feedback></b-col
                    >
                  </b-row>
                </b-card-body>
              </b-collapse>
            </b-card>
          </transition>
        </b-col>
      </b-row>

      <b-row>
        <b-col sm="12" md="12">
          <product-base-template
            v-if="category == 0"
            :template="model"
          ></product-base-template>
          <click-base-template v-if="category == 1"></click-base-template>
        </b-col>
      </b-row>
      <b-card>
        <b-row>
          <b-col sm="1" md="11">
            <b-button variant="danger" @click="backToList">Cancel</b-button>
          </b-col>
          <b-col sm="1">
            <b-button variant="primary">Create</b-button>
          </b-col>
        </b-row></b-card
      >
    </b-card>
  </div>
</template>

<script>
import { Callout } from "@coreui/vue";
import axios from "axios";
import _xnconvert from "@/mylib/xn-data-convert-engine";
import ProductBaseTemplate from "./product-base/ProductBaseTemplate";

export default {
  name: "CommissionTemplate",
  components: {
    Callout,
    ProductBaseTemplate
  },
  data: function() {
    return {
      categories: [
        {
          id: -1,
          name: "Select Category"
        },
        {
          id: 0,
          name: "Product Base"
        },
        {
          id: 1,
          name: "Click Base"
        }
      ],
      cards: {
        template: {
          active: true,
          variant: "danger",
          statusMsg: "Incompleted",
          valid: false
        }
      },
      category: -1,
      validation: {
        name: {
          state: null,
          msg: ""
        },
        category: {
          state: null,
          msg: ""
        },
        startDate: {
          state: null,
          msg: ""
        },
        endDate: {
          state: null,
          msg: ""
        }
      },
      model: {
        id: 0,
        name: "",
        startDate: "",
        endDate: ""
      }
    };
  },
  watch: {
    validation: {
      handler: function(val, oldVal) {
        if (
          val.name.state &&
          val.category.state &&
          val.startDate.state &&
          val.endDate.state
        ) {
          this.cards.template.variant = "success";
          this.cards.template.statusMsg = "Completed";
          this.cards.template.valid = true;
        } else {
          this.cards.template.variant = "danger";
          this.cards.template.statusMsg = "Incompleted";
          this.cards.template.valid = false;
        }
      },
      deep: true
    }
  },
  methods: {
    formatDate(strDate) {
      return _xnconvert.formatDate(new Date(strDate), "dd mmm yyyy");
    },
    backToList() {
      this.$parent.activePage = "index";
    },
    checkName() {
      if (this.model.name.length < 5) {
        this.validation.name.msg =
          "Template Name must be at least 5 characters";
        this.validation.name.state = false;
      } else {
        this.validation.name.state = true;
      }
    },
    checkCategory() {
      if (this.category < 0) {
        this.validation.category.msg = "Category must be selected";
        this.validation.category.state = false;
      } else {
        this.validation.category.state = true;
      }
    },
    checkDate() {
      if (this.model.startDate.length < 1) {
        this.validation.startDate.msg = "Effective date from cannot be empty";
        this.validation.startDate.state = false;
        return;
      } else {
        this.validation.startDate.state = true;
      }

      if (this.model.endDate.length < 1) {
        this.validation.endDate.msg = "Effective date to cannot be empty";
        this.validation.endDate.state = false;
        return;
      } else {
        this.validation.endDate.state = true;
      }

      if (new Date(this.model.startDate) > new Date(this.model.endDate)) {
        this.validation.endDate.msg =
          "Effective date to cannot be less than Effective date from";
        this.validation.endDate.state = false;
      } else {
        this.validation.endDate.state = true;
      }
    }
  },
  computed: {
    rows() {
      return this.templates.length;
    }
  }
};
</script>
