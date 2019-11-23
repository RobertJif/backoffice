<template>
	<div id="mychart"></div>
</template>

<script>
var Highcharts = require('highcharts');
export default {
    name : "Chart",
    props : {
      chartRevenue: Array,
      chartTurnover: Array,
      chartSeries: Array
    },
  	data : function() {
      return {
        target: undefined
      }
    },
    methods:{
      redraw(){
        this.chart.series[0].setData(this.chartData,false);
        this.chart.xAxis[0].setCategories(this.chartSeries, true, true);
      }
    },
    watch:{
      chartData(){this.redraw()}
    },
  	mounted() {
        var highchartsOptions = {
            chart: {
                type: 'column',
                renderTo: 'mychart'
            },
            credits: {
                enabled: false
            },
            tooltip: {
                enabled: true
            },
            title: {
                text: ''
            },
            xAxis: {
                allowDecimals: true,
                title: {
                    text: 'Products'
        },
        categories : this.chartSeries
            },
            yAxis: {
                title: {
                text: 'Amount'
                },
                labels: {
                    formatter: function () {
                    return this.value;
                }
                },
            },
            plotOptions: {},
            series: [
              {
                  name: 'Win/Loss',
                  data: this.chartRevenue
              },
              {
                  name: 'Stake',
                  data: this.chartTurnover
              }
              ],
            credits: false
        }
            this.chart = new Highcharts.chart(highchartsOptions)
    }
  
}
</script>