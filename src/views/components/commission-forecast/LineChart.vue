<template>
	<div id="mychart">
  </div>
</template>

<script>
import _xnconvert from '@/mylib/xn-data-convert-engine'

var Highcharts = require('highcharts');

var xnChart = {
    name : "Chart",
    props : {
      chartData: Array,
      chartSeries: Array,
      currency: String
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
      chartData(){this.redraw()},
      chartSeries(){this.redraw()},
      currency(){this.redraw()}
    },
  	mounted() {
		var highchartsOptions = {
			chart: {
				type: 'line',
				renderTo: 'mychart'
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
					text: 'Forecast Date'
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
        plotOptions: {
            line: {
                dataLabels: {
                    enabled: true,
                    formatter: function () {
                        return _xnconvert.formatNumber(this.y, "delimiter");
                    }
                },
                enableMouseTracking: true
            },
            series: {
                marker: {
                    enabled: true,
                    symbol: 'circle',
                    radius: 6,
                    states: {
                        hover: {
                            enabled: true
                        }
                    }
                },
                cursor: 'pointer',
                point: {
                    events: {
                      click: ({point}) => {
                        this.$emit('openDetail', point.category);
                      }
                    }
                }
            }

        },
			series: [{
    		name: 'Amount',
    		data: this.chartData
  		}],
			credits: false
    	}
			this.chart = new Highcharts.chart(highchartsOptions)
  }
  
}

export default xnChart
</script>