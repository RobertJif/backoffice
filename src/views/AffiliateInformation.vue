<template>
  <div id="app">
    <br>
    <div class="row">
      <div class="col col-md-6">
        <b-form-input id="altaddress" v-model="templateName" v-on:input="templateName = $event.target.value"></b-form-input> 
      </div>
      <div class="col col-md-6">
        <b-form-select v-model="templateCategory.selected" :options="templateCategory.options"></b-form-select>
      </div>
    </div>
    <div class="row">
      <div v-if="templateCategory.selected == '0'">
        <Template v-bind:templateName="templateName"/>

      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'AffiliateInformation',
  components: {
  }
}
</script>

