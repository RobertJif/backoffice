<template>
  <div class="animated fadeIn">
    <b-card class="animated fadeIn">
      <transition name="fade">
        <b-card no-body v-if="show">
          <div slot="header">
            Card with header actions

            <div class="card-header-actions">
              <b-badge variant="success">Success</b-badge>
            </div>
            <div class="card-header-actions">
              <b-link
                class="card-header-action btn-minimize"
                v-b-toggle.collapse1
              >
                <i class="icon-arrow-up"></i>
              </b-link>
            </div>
          </div>
          <b-collapse id="collapse1" visible>
            <b-card-body>
              Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
              nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam
              erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci
              tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo
              consequat.
            </b-card-body>
          </b-collapse>
        </b-card>
      </transition>

      <b-button variant="danger" @click="activePage = 'index'">Cancel</b-button>
      <b-button variant="primary" @click="createCommissionSettings"
        >Create</b-button
      >
    </b-card>
  </div>
</template>

<script>
import { Callout } from "@coreui/vue";
import axios from "axios";
import _xnconvert from "@/mylib/xn-data-convert-engine";

export default {
  name: "AffiliateInformation",
  components: {
    Callout
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
      head: {
        show: true
      }
    };
  },
  mounted() {
    axios
      .all([
        axios.get(
          process.env.VUE_APP_AFFILIATE_API_URL + "commission-templates"
        )
      ])
      .then(
        axios.spread(tmplRes => {
          console.log(tmplRes.data);
          this.templates = tmplRes.data;
          this.isTmplLoading = false;
        })
      )
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
    openManage: function(Id) {
      this.$router.push("commission-forecast");
    },
    openCreate: function() {
      this.$router.push("commission-setting/create");
    },
    getCategoryName(categoryId) {
      switch (categoryId) {
        case 0:
          return "Product Base";
          break;
        case 1:
          return "Click Base";
          break;
        default:
          return "Undefined";
      }
    },
    formatDate(strDate) {
      return _xnconvert.formatDate(new Date(strDate), "dd mmm yyyy");
    }
  },
  computed: {
    rows() {
      return this.templates.length;
    }
  }
};
</script>
