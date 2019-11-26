<template>
  <div class="animated fadeIn">
    <b-card>
      <h1>Affiliate Management</h1>
      <br />
      <b-table
        id="aff-table"
        :items="affiliates"
        :fields="fields"
        :per-page="perPage"
        :current-page="currentPage"
        :busy="isAffLoading"
        bordered
        hover
      >
        <template v-slot:table-colgroup="scope">
          <col
            v-for="field in scope.fields"
            :key="field.key"
            :style="{
              width:
                field.key === 'index' || field.key === 'affManage'
                  ? '20px'
                  : '250px'
            }"
          />
        </template>
        <template v-slot:table-busy>
          <div class="text-center text-danger my-2">
            <b-spinner class="align-middle"></b-spinner>
            <strong>Loading...</strong>
          </div>
        </template>

        <template slot="index" slot-scope="data">
          {{ data.index + 1 }}
        </template>

        <template slot="affcode" slot-scope="data">
          {{ data.item.code }}
        </template>

        <template slot="affRegistrationDate" slot-scope="data">
          {{ formatDate(data.item.registrationDate) }}
        </template>

        <template slot="affManage" slot-scope="data">
          <button class="btn btn-primary" @click="openManage(data.value.code)">
            Manage
          </button>
        </template>
      </b-table>
      <!-- 
        <p class="mt-3">Current Page: {{ currentPage }}</p> -->
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        aria-controls="aff-table"
      ></b-pagination>
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
      affiliates: [],
      fields: [
        { key: "index", label: "No." },
        { key: "affcode", label: "Affiliate Code" },
        { key: "affRegistrationDate", label: "Registration Date" },
        { key: "affManage", label: "Actions" }
      ],
      isAffLoading: true,
      perPage: 10,
      currentPage: 1
    };
  },
  mounted() {
    axios
      .all([
        axios.get(
          process.env.VUE_APP_AFFILIATE_MANAGEMENT_API_URL + "affiliates"
        )
      ])
      .then(
        axios.spread(affiliateRes => {
          this.affiliates = affiliateRes.data;
          this.isAffLoading = false;
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
    formatDate(strDate) {
      return _xnconvert.formatDate(new Date(strDate), "dd mmm yyyy");
    }
  },
  computed: {
    rows() {
      return this.affiliates.length;
    }
  }
};
</script>
