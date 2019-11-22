<template>
  <div class="animated fadeIn">
    <b-card>
    <h1>Commission Setting Management</h1>
    <br>
        <b-table
          id="tmpl-table"
          :items="templates"
          :fields="fields"
          :per-page="perPage"
          :current-page="currentPage"
          :busy="isTmplLoading"
          bordered hover
        >
          <template v-slot:table-colgroup="scope">
            <col
              v-for="field in scope.fields"
              :key="field.key"
              :style="{ width: field.key === 'index' || field.key === 'tmplManage' ? '20px' : '250px' }"
            >
          </template>
          <template v-slot:table-busy>  
            <div class="text-center text-danger my-2">
              <b-spinner class="align-middle"></b-spinner>
              <strong>Loading...</strong>
            </div>
          </template>

          <template slot="index" slot-scope="data">
            {{ data.index +1 }}
          </template>

          <template slot="tmplName" slot-scope="data">
            {{ data.item.name }}
          </template>

          <template slot="categoryName" slot-scope="data">
            {{ getCategoryName(data.item.category) }}
          </template>

          <template slot="effDtFrom" slot-scope="data">
            {{ formatDate(data.item.startDate) }}
          </template>

          <template slot="effDtTo" slot-scope="data">
            {{ formatDate(data.item.endDate) }}
          </template>

          <template slot="updatedAt" slot-scope="data">
            {{ data.item.updatedAt }}
          </template>

          <template slot="tmplManage" slot-scope="data">
            <button class="btn btn-primary" @click="openManage(data.value.id)">Manage</button>
          </template>

        </b-table>
<!-- 
        <p class="mt-3">Current Page: {{ currentPage }}</p> -->
        <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        aria-controls="tmpl-table"
        ></b-pagination>
    </b-card>
  </div>
</template>

<script>

import { Callout } from '@coreui/vue'
import axios from 'axios'
import _xnconvert from '@/mylib/xn-data-convert-engine'

export default {
  name: 'AffiliateInformation',
  components: {
    Callout
  },
  data: function(){
    return {
      templates : [],
      fields : [
          { key: 'index', label: 'No.' },
          { key: 'tmplName', label: 'Template Name' },
          { key: 'categoryName', label: 'Template Category' },
          { key: 'effDtFrom', label: 'Effective Date From' },
          { key: 'effDtTo', label: 'Effective Date To' },
          { key: 'updatedAt', label: 'Last Modified At' },
          { key: 'tmplManage', label: 'Actions' },

      ],
      isTmplLoading : true,
      perPage: 10,
      currentPage: 1,
    }
  },
  mounted () {
    
    axios.all([
        axios.get(process.env.VUE_APP_AFFILIATE_API_URL + 'commission-templates')
      ])
      .then(axios.spread((tmplRes) => {
        console.log(tmplRes.data)
        this.templates = tmplRes.data
        this.isTmplLoading = false
      }))
      .catch(error => {
        console.log(error)
      })
  },
  methods:{
    openManage: function(Id){
      this.$router.push('commission-forecast') 
    },
    getCategoryName(categoryId){
      switch(categoryId) {
        case 0:
            return "Product Base"
            break;
        case 1:
            return "Click Base"
            break;
        default:
            return "Undefined"
        } 
    },
    formatDate(strDate){
      return _xnconvert.formatDate(new Date(strDate), "dd mmm yyyy" )
    }
  },
    computed: {
      rows() {
        return this.templates.length
      }
    }
}
</script>

