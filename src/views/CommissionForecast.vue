<template>
  <div class="animated fadeIn">
    <b-card>
      <b-row>
        <b-col sm="6" lg="3">
          <b-form-select
            v-model="affiliates.selected"
            :options="affiliates.options"
            value-field="code"
            text-field="code"
          ></b-form-select>
        </b-col>
        <b-col sm="6" lg="3">
          <b-form-select
            v-model="currencyTypes.selected"
            :options="currencyTypes.options"
          ></b-form-select>
        </b-col>
        <b-col sm="6" lg="3">
          <b-form-select
            v-model="activeChart.selected"
            :options="activeChart.options"
          ></b-form-select>
        </b-col>
      </b-row>
      <hr />
      <b-row>
        <b-col sm="6" lg="3">
          <br />
        </b-col>
      </b-row>

      <b-row>
        <b-col sm="12" lg="12">
          <h4 id="traffic" class="card-title mb-0">
            {{ affiliates.selected }}
          </h4>
          <div class="small text-muted">{{ forecast.lastUpdated }}</div>
        </b-col>
      </b-row>
      <b-card class="text-center">
        <b-row>
          <b-col sm="3" lg="3">
            <b-row>
              <b-col sm="12" lg="12"> <br /><br /><br /><br /><br /> </b-col>
            </b-row>
            <b-row>
              <b-col sm="12" lg="12">
                <h3>WAGER COUNT</h3>
                <br />
                <h4>{{ forecast.totalWager }}</h4>
                <hr />
              </b-col>
            </b-row>
            <b-row>
              <b-col sm="12" lg="12">
                <h3>WIN/LOSS</h3>
                <br />
                <h4>{{ forecast.currency }} {{ forecast.totalRevenue }}</h4>
                <hr />
              </b-col>
            </b-row>
            <b-row>
              <b-col sm="12" lg="12">
                <h3>STAKE</h3>
                <br />
                <h4>{{ forecast.currency }} {{ forecast.totalTurnover }}</h4>
              </b-col>
            </b-row>
          </b-col>
          <b-col sm="9" lg="9">
            <b-row>
              <b-col sm="12" lg="12">
                <h3>Commission Forecast</h3>
                <h4>
                  Total: {{ forecast.currency }} {{ forecast.totalAmount }}
                </h4>
              </b-col>
            </b-row>
            <b-row>
              <b-col sm="12" lg="12">
                <line-chart
                  v-if="activeChart.selected == '0'"
                  chartId="line-chart"
                  class="chart-wrapper"
                  style="height:300px;margin-top:40px;"
                  height="300"
                  :chartData="lineChartData.data"
                  :chartSeries="lineChartData.series"
                  :currency="forecast.currency"
                  @openDetail="openDetails($event)"
                ></line-chart>
                <column-chart
                  v-if="activeChart.selected == '1'"
                  chartId="column-chart"
                  class="chart-wrapper"
                  style="height:300px;margin-top:40px;"
                  height="300"
                  :chartRevenue="columnChartData.revenue"
                  :chartSeries="columnChartData.series"
                  :chartTurnover="columnChartData.turnover"
                  :currency="forecast.currency"
                ></column-chart>
              </b-col>
            </b-row>
          </b-col>
        </b-row>
      </b-card>
    </b-card>
  </div>
</template>

<script>
import LineChart from "./components/commission-forecast/LineChart";
import ColumnChart from "./components/commission-forecast/ColumnChart";
import { Callout } from "@coreui/vue";
import axios from "axios";
import _xnconvert from "@/mylib/xn-data-convert-engine";

export default {
  name: "CommissionForecast",
  components: {
    Callout,
    LineChart,
    ColumnChart
  },
  data: function() {
    return {
      activeChart: {
        selected: "0",
        options: [
          { value: "0", text: "By Dates" },
          { value: "1", text: "By Products" }
        ]
      },
      currencyTypes: {
        selected: "C",
        options: [
          { value: "C", text: "Company Currency" },
          { value: "A", text: "Affiliate Currency" }
        ]
      },
      affiliates: {
        selected: null,
        options: []
      },
      forecast: {
        lastUpdated: new Date(),
        totalAmount: 0,
        totalWager: 0,
        totalRevenue: 0,
        totalTurnover: 0,
        currency: ""
      },
      lineChartData: {
        data: [],
        series: []
      },
      columnChartData: {
        revenue: [],
        turnover: [],
        series: []
      }
    };
  },
  watch: {
    "affiliates.selected": {
      handler: function(val, oldVal) {
        if (val != oldVal && oldVal != null) {
          this.loadForecast();
        }
      },
      deep: true
    },
    "currencyTypes.selected": {
      handler: function(val, oldVal) {
        if (val != oldVal && oldVal != null) {
          this.loadForecast();
        }
      },
      deep: true
    }
  },
  mounted() {
    this.loadForecast();
  },
  methods: {
    loadForecast() {
      console.log(process.env.VUE_APP_AFFILIATE_MANAGEMENT_API_URL + "affiliates")
      axios
        .all([
          axios.get(
            process.env.VUE_APP_AFFILIATE_MANAGEMENT_API_URL + "affiliates"
          )
          //,axios.get(process.env.VUE_APP_REPORT_API_URL + 'product-templates')
        ])
        .then(
          axios.spread(affiliateRes => {
            this.affiliates.options = affiliateRes.data;

            if (this.affiliates.selected == null) {
              this.affiliates.selected = affiliateRes.data[0].code;
            }

            const params = {
              affcode: this.affiliates.selected,
              startDate: "01-11-2019",
              endDate: "30-11-2019",
              currencyType: this.currencyTypes.selected
            };

            axios
              .get(process.env.VUE_APP_REPORT_API_URL + "forecast", { params })
              .then(response => {
                console.log(response.data.columnChartData);
                this.forecast.totalAmount = response.data.totalAmount;
                this.forecast.totalWager = response.data.totalWagerCount;
                this.forecast.totalRevenue = response.data.totalGrossRevenue;
                this.forecast.totalTurnover = response.data.totalTurnover;
                this.forecast.currency = response.data.currency;

                if (response.data.lineChartData != undefined) {
                  this.lineChartData.data = response.data.lineChartData.map(
                    item => item.amount
                  );
                  this.lineChartData.series = response.data.lineChartData.map(
                    item =>
                      _xnconvert
                        .formatDate(new Date(item.date), "dd-mm-yyyy")
                        .toString()
                  );
                } else {
                  this.lineChartData.data = [];
                  this.lineChartData.series = [];
                }

                if (response.data.columnChartData != undefined) {
                  this.columnChartData.turnover = response.data.columnChartData.map(
                    item => item.turnover
                  );
                  this.columnChartData.revenue = response.data.columnChartData.map(
                    item => item.grossRevenue
                  );
                  this.columnChartData.series = response.data.columnChartData.map(
                    item => item.productCode
                  );
                } else {
                  this.columnChartData.turnover = [];
                  this.columnChartData.revenue = [];
                  this.columnChartData.series = [];
                }
              });
          })
        )
        .catch(error => {
          console.log(error);
        });
    },
    openDetails(forecastDate) {
      this.$router.push({
        name: "Affiliate Information",
        params: {
          affCode: this.affiliates.selected,
          forecastDate: forecastDate,
          currencyType: this.currencyTypes.selected
        }
      });
    }
  }
};
</script>

<style>
/* IE fix */
#card-chart-01,
#card-chart-02 {
  width: 100% !important;
}
</style>
