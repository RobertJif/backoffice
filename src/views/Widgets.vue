<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col sm="6" lg="3">
        <b-card>
          <div class="h4 m-0">89.9%</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-xs my-3"
            variant="success"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col>
      <b-col sm="6" lg="3">
        <b-card>
          <div class="h4 m-0">12.124</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-xs my-3"
            variant="info"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col>
      <b-col sm="6" lg="3">
        <b-card>
          <div class="h4 m-0">$98.111,00</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-xs my-3"
            variant="warning"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col>
      <b-col sm="6" lg="3">
        <b-card>
          <div class="h4 m-0">2 TB</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-xs my-3"
            variant="danger"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col> </b-row
    ><!--/.row-->
    <b-row>
      <b-col sm="6" lg="3">
        <b-card class="text-white bg-primary">
          <div class="h4 m-0">89.9%</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-white progress-xs my-3"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col>
      <b-col sm="6" lg="3">
        <b-card class="text-white bg-warning">
          <div class="h4 m-0">12.124</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-white progress-xs my-3"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col>
      <b-col sm="6" lg="3">
        <b-card class="text-white bg-danger">
          <div class="h4 m-0">$98.111,00</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-white progress-xs my-3"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col>
      <b-col sm="6" lg="3">
        <b-card class="text-white bg-info">
          <div class="h4 m-0">2 TB</div>
          <div>Lorem ipsum...</div>
          <b-progress
            height="{}"
            class="progress-white progress-xs my-3"
            :value="25"
          />
          <small class="text-muted">Lorem ipsum dolor sit amet enim.</small>
        </b-card>
      </b-col> </b-row
    ><!--/.row-->
    <b-row>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-cogs bg-primary p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-primary mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-laptop bg-info p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-info mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-moon-o bg-warning p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-warning mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-bell bg-danger p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-danger mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true" footer-class="px-3 py-2">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-cogs bg-primary p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-primary mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
          <div slot="footer">
            <b-link
              class="font-weight-bold font-xs btn-block text-muted"
              href="#"
              >View More <i class="fa fa-angle-right float-right font-lg"></i
            ></b-link>
          </div>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true" footer-class="px-3 py-2">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-laptop bg-info p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-info mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
          <div slot="footer">
            <b-link
              class="font-weight-bold font-xs btn-block text-muted"
              href="#"
              >View More <i class="fa fa-angle-right float-right font-lg"></i
            ></b-link>
          </div>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true" footer-class="px-3 py-2">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-moon-o bg-warning p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-warning mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
          <div slot="footer">
            <b-link
              class="font-weight-bold font-xs btn-block text-muted"
              href="#"
              >View More <i class="fa fa-angle-right float-right font-lg"></i
            ></b-link>
          </div>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true" footer-class="px-3 py-2">
          <b-card-body class="p-3 clearfix">
            <i class="fa fa-bell bg-danger p-3 font-2xl mr-3 float-left"></i>
            <div class="h5 text-danger mb-0 mt-2">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
          <div slot="footer">
            <b-link
              class="font-weight-bold font-xs btn-block text-muted"
              href="#"
              >View More <i class="fa fa-angle-right float-right font-lg"></i
            ></b-link>
          </div>
        </b-card>
      </b-col> </b-row
    ><!--/.row-->
    <b-row>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i class="fa fa-cogs bg-primary p-4 font-2xl mr-3 float-left"></i>
            <div class="h5 text-primary mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i class="fa fa-laptop bg-info p-4 font-2xl mr-3 float-left"></i>
            <div class="h5 text-info mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i class="fa fa-moon-o bg-warning p-4 font-2xl mr-3 float-left"></i>
            <div class="h5 text-warning mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i class="fa fa-bell bg-danger p-4 font-2xl mr-3 float-left"></i>
            <div class="h5 text-danger mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i
              class="fa fa-cogs bg-primary p-4 px-5 font-2xl mr-3 float-left"
            ></i>
            <div class="h5 text-primary mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i
              class="fa fa-laptop bg-info p-4 px-5 font-2xl mr-3 float-left"
            ></i>
            <div class="h5 text-info mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i
              class="fa fa-moon-o bg-warning p-4 px-5 font-2xl mr-3 float-left"
            ></i>
            <div class="h5 text-warning mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col>
      <b-col cols="12" sm="6" lg="3">
        <b-card :no-body="true">
          <b-card-body class="p-0 clearfix">
            <i
              class="fa fa-bell bg-danger p-4 px-5 font-2xl mr-3 float-left"
            ></i>
            <div class="h5 text-danger mb-0 pt-3">$1.999,50</div>
            <div class="text-muted text-uppercase font-weight-bold font-xs">
              Income
            </div>
          </b-card-body>
        </b-card>
      </b-col> </b-row
    ><!--/.row-->
    <b-row>
      <b-col md="3" sm="6">
        <div class="brand-card">
          <div class="brand-card-header bg-facebook">
            <i class="fa fa-facebook"></i>
            <div class="chart-wrapper">
              <social-box-chart-example :data="[65, 59, 84, 84, 51, 55, 40]" />
            </div>
          </div>
          <div class="brand-card-body">
            <div>
              <div class="text-value">89k</div>
              <div class="text-uppercase text-muted small">friends</div>
            </div>
            <div>
              <div class="text-value">459</div>
              <div class="text-uppercase text-muted small">feeds</div>
            </div>
          </div>
        </div>
      </b-col>
      <b-col md="3" sm="6">
        <div class="brand-card">
          <div class="brand-card-header bg-twitter">
            <i class="fa fa-twitter"></i>
            <div class="chart-wrapper">
              <social-box-chart-example :data="[1, 13, 9, 17, 34, 41, 38]" />
            </div>
          </div>
          <div class="brand-card-body">
            <div>
              <div class="text-value">973k</div>
              <div class="text-uppercase text-muted small">followers</div>
            </div>
            <div>
              <div class="text-value">1.792</div>
              <div class="text-uppercase text-muted small">tweets</div>
            </div>
          </div>
        </div>
      </b-col>
      <b-col md="3" sm="6">
        <div class="brand-card">
          <div class="brand-card-header bg-linkedin">
            <i class="fa fa-linkedin"></i>
            <div class="chart-wrapper">
              <social-box-chart-example :data="[78, 81, 80, 45, 34, 12, 40]" />
            </div>
          </div>
          <div class="brand-card-body">
            <div>
              <div class="text-value">500+</div>
              <div class="text-uppercase text-muted small">contacts</div>
            </div>
            <div>
              <div class="text-value">292</div>
              <div class="text-uppercase text-muted small">feeds</div>
            </div>
          </div>
        </div>
      </b-col>
      <b-col md="3" sm="6">
        <div class="brand-card">
          <div class="brand-card-header bg-google-plus">
            <i class="fa fa-google-plus"></i>
            <div class="chart-wrapper">
              <social-box-chart-example :data="[35, 23, 56, 22, 97, 23, 64]" />
            </div>
          </div>
          <div class="brand-card-body">
            <div>
              <div class="text-value">894</div>
              <div class="text-uppercase text-muted small">followers</div>
            </div>
            <div>
              <div class="text-value">92</div>
              <div class="text-uppercase text-muted small">circles</div>
            </div>
          </div>
        </div>
      </b-col> </b-row
    ><!--/.row-->
    <b-card-group class="mb-4">
      <b-card>
        <div class="h1 text-muted text-right mb-4">
          <i class="icon-people"></i>
        </div>
        <div class="h4 mb-0">87.500</div>
        <small class="text-muted text-uppercase font-weight-bold"
          >Visitors</small
        >
        <b-progress
          height="{}"
          class="progress-xs mt-3 mb-0"
          variant="info"
          :value="25"
        />
      </b-card>
      <b-card>
        <div class="h1 text-muted text-right mb-4">
          <i class="icon-user-follow"></i>
        </div>
        <div class="h4 mb-0">385</div>
        <small class="text-muted text-uppercase font-weight-bold"
          >New Clients</small
        >
        <b-progress
          height="{}"
          class="progress-xs mt-3 mb-0"
          variant="success"
          :value="25"
        />
      </b-card>
      <b-card>
        <div class="h1 text-muted text-right mb-4">
          <i class="icon-basket-loaded"></i>
        </div>
        <div class="h4 mb-0">1238</div>
        <small class="text-muted text-uppercase font-weight-bold"
          >Products sold</small
        >
        <b-progress
          height="{}"
          class="progress-xs mt-3 mb-0"
          variant="warning"
          :value="25"
        />
      </b-card>
      <b-card>
        <div class="h1 text-muted text-right mb-4">
          <i class="icon-pie-chart"></i>
        </div>
        <div class="h4 mb-0">28%</div>
        <small class="text-muted text-uppercase font-weight-bold"
          >Returning Visitors</small
        >
        <b-progress height="{}" class="progress-xs mt-3 mb-0" :value="25" />
      </b-card>
      <b-card>
        <div class="h1 text-muted text-right mb-4">
          <i class="icon-speedometer"></i>
        </div>
        <div class="h4 mb-0">5:34:11</div>
        <small class="text-muted text-uppercase font-weight-bold"
          >Avg. Time</small
        >
        <b-progress
          height="{}"
          class="progress-xs mt-3 mb-0"
          variant="danger"
          :value="25"
        />
      </b-card>
    </b-card-group>
    <b-row>
      <b-col sm="6" md="2">
        <b-card>
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-people"></i>
          </div>
          <div class="h4 mb-0">87.500</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Visitors</small
          >
          <b-progress
            height="{}"
            class="progress-xs mt-3 mb-0"
            variant="info"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card>
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-user-follow"></i>
          </div>
          <div class="h4 mb-0">385</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >New Clients</small
          >
          <b-progress
            height="{}"
            class="progress-xs mt-3 mb-0"
            variant="success"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card>
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-basket-loaded"></i>
          </div>
          <div class="h4 mb-0">1238</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Products sold</small
          >
          <b-progress
            height="{}"
            class="progress-xs mt-3 mb-0"
            variant="warning"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card>
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-pie-chart"></i>
          </div>
          <div class="h4 mb-0">28%</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Returning Visitors</small
          >
          <b-progress height="{}" class="progress-xs mt-3 mb-0" :value="25" />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card>
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-speedometer"></i>
          </div>
          <div class="h4 mb-0">5:34:11</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Avg. Time</small
          >
          <b-progress
            height="{}"
            class="progress-xs mt-3 mb-0"
            variant="danger"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card>
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-speech"></i>
          </div>
          <div class="h4 mb-0">972</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Comments</small
          >
          <b-progress
            height="{}"
            class="progress-xs mt-3 mb-0"
            variant="info"
            :value="25"
          />
        </b-card>
      </b-col> </b-row
    ><!--/.row-->
    <b-row>
      <b-col sm="6" md="2">
        <b-card class="text-white bg-info">
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-people"></i>
          </div>
          <div class="h4 mb-0">87.500</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Visitors</small
          >
          <b-progress
            height="{}"
            class="progress-white progress-xs mt-3"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card class="text-white bg-success">
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-user-follow"></i>
          </div>
          <div class="h4 mb-0">385</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >New Clients</small
          >
          <b-progress
            height="{}"
            class="progress-white progress-xs mt-3"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card class="text-white bg-warning">
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-basket-loaded"></i>
          </div>
          <div class="h4 mb-0">1238</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Products sold</small
          >
          <b-progress
            height="{}"
            class="progress-white progress-xs mt-3"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card class="text-white bg-primary">
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-pie-chart"></i>
          </div>
          <div class="h4 mb-0">28%</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Returning Visitors</small
          >
          <b-progress
            height="{}"
            class="progress-white progress-xs mt-3"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card class="text-white bg-danger">
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-speedometer"></i>
          </div>
          <div class="h4 mb-0">5:34:11</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Avg. Time</small
          >
          <b-progress
            height="{}"
            class="progress-white progress-xs mt-3"
            :value="25"
          />
        </b-card>
      </b-col>
      <b-col sm="6" md="2">
        <b-card class="text-white bg-info">
          <div class="h1 text-muted text-right mb-4">
            <i class="icon-speech"></i>
          </div>
          <div class="h4 mb-0">972</div>
          <small class="text-muted text-uppercase font-weight-bold"
            >Comments</small
          >
          <b-progress
            height="{}"
            class="progress-white progress-xs mt-3"
            :value="25"
          />
        </b-card>
      </b-col> </b-row
    ><!--/.row-->
  </div>
</template>

<script>
import SocialBoxChartExample from "./dashboard/SocialBoxChartExample";
export default {
  name: "widgets",
  components: {
    SocialBoxChartExample
  },
  data() {
    return {
      msg: "Widgets"
    };
  }
};
</script>
