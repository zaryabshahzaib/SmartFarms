<template>
  <div class="dashboard-page">
    <b-row>
      <b-col class = "text-center">
      <h1 class="page-title" style = "font-size: 50px"><b>Overview</b> &nbsp;</h1>
      </b-col>
    </b-row>
    <br>
    <Widget
         title="<h5 style = 'text-align:center;'> <span style = 'font-size:27px;' class='fw-bold'>Recent Recommendations</span></h5>"
         customHeader settings close
    >
     <b-row>
        <!-- <b-col lg = "1">
        </b-col> -->
     <b-col >
      
      <table class="table table-striped" >
           <thead>
             <tr>
               <th>Urgency</th>
               <th>Type</th>
               <th>Message</th>
               <th>Recommendation</th>
             </tr>
           </thead>
           <tbody>
             <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "danger"></b-icon></p></td>
               <td style = 'font-size:18px;'>Diseased Crop</td>
               <td style = 'font-size:18px;'>Mold detected on the leaves of tomato crop</td>
               <td style = 'font-size:18px;'>Spray the field evenly with 5 litres of pesticide</td>
             </tr>
             <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "danger"></b-icon></p></td>
               <td style = 'font-size:18px;'>Moisture </td>
               <td style = 'font-size:18px;'>Moisture levels are higher than specified limit</td>
               <td style = 'font-size:18px;'>Field should not be watered for the next 23 hours</td>
             </tr>
             <!-- <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "warning"></b-icon></p></td>
               <td style = 'font-size:18px;'>Larry</td>
               <td style = 'font-size:18px;'>the Bird</td>
               <td style = 'font-size:18px;'>Online</td>
             </tr> -->
           </tbody>
         </table>
          </b-col>
           </b-row>
        </Widget>
    <Widget
        title="<h4 style = 'text-align:center;'> <span style = 'font-size:30px;' class='fw-bold'>Environment</span></h5>"
        close customHeader
    >
    <br>
    <b-row>
     
      <b-col lg="3" xs="15">
        <Widget
          title="<h5 style = 'text-align:center;'> <span style = 'font-size:25px;' class='fw-bold'>Humidity</span></h5>"
          close customHeader
        >
          <br>
          <div>
            <highcharts :options="chartOptions" :callback="chartCallback"></highcharts>
          </div>
          <div>
        
            <echart :options="cd.echarts.humidity_line" :init-options="initEchartsOptions" style="height: 370px"></echart>
       
          </div>
        </Widget>
      </b-col>
      <b-col lg="5" xs="12">
        
        <Widget
          title="<h5 style = 'text-align:center;'> <span style = 'font-size:25px;' class='fw-bold'>Weather</span></h5>"
          close customHeader
        >
          
          <div>
            <weather 
                api-key= "85702345f96272db7a52c3d597695baa"
                title="Weather"
                latitude="25.2854"
                longitude="51.5310"
                language="en"
                units="uk"
                hide-header = true>
            </weather>
          </div>
          <div>
        
            <echart :options="cd.echarts.weather_line" :init-options="initEchartsOptions" style="height: 370px"></echart>
       
          </div>
        </Widget>
      </b-col>
      <b-col lg="4" xs="15">
        <Widget
          title="<h5 style = 'text-align:center;'> <span style = 'font-size:25px;' class='fw-bold'>Light</span></h5>"
          close customHeader
        >
          <br>
          <div>
            <highcharts :options="chartOptions2" :callback="chartCallback1"></highcharts>
          </div>
          <div>
        
            <echart :options="cd.echarts.light_line" :init-options="initEchartsOptions" style="height: 370px"></echart>
       
          </div>
        </Widget>
      </b-col>
      
    </b-row>
    </Widget>

    <Widget
        title="<h4 style = 'text-align:center;'> <span style = 'font-size:27px;' class='fw-bold'>Soil</span></h5>"
        close customHeader
    >
    <br>
    <b-row>
     
      <b-col lg="3" xs="15">
        <Widget
          title="<h5 style = 'text-align:center;'> <span style = 'font-size:20px;' class='fw-bold'>pH</span></h5>"
          close customHeader
        >
          <div>
            <highcharts :options="phChartOptions" :callback="phChartCallback"></highcharts>
          </div>
          <div>
            <echart :options="cd.echarts.ph_line" :init-options="initEchartsOptions" style="height: 370px"></echart>   
          </div>
        </Widget>
      </b-col>
      <b-col lg="3" xs="15">
        <Widget
          title="<h5 style = 'text-align:center;'> <span style = 'font-size:20px;' class='fw-bold'>Moisture</span></h5>"
          close customHeader
        >
          <div>
            <highcharts :options="chartmoisture" :callback="chartCallback3"></highcharts>
          </div>
          <div>
        
            <echart :options="cd.echarts.moisture_line" :init-options="initEchartsOptions" style="height: 370px"></echart>
       
          </div>
        </Widget>
      </b-col>
      <b-col lg="6" xs="15">
        <Widget
          title="<h5 style = 'text-align:center;'> <span style = 'font-size:20px;' class='fw-bold'>Nutrients</span></h5>"
          close customHeader
        >
          <div>
            <highcharts :options="nutrientChartOptions" :callback="chartCallback4" ></highcharts>
          </div>
          <div>
        
            <echart :options="cd.echarts.nutrients_line" :init-options="initEchartsOptions" style="height: 370px"></echart>
       
          </div>
        </Widget>
      </b-col>
      
    </b-row>
    </Widget>

    <!-- <b-row>
      <b-col lg="4" xs="12">
        <Widget
          title="<h6> USERBASE GROWTH </h6>"
          close settings customHeader
        >
          <div class="stats-row">
            <div class="stat-item">
              <h6 class="name">Overall Growth</h6>
              <p class="value">76.38%</p>
            </div>
            <div class="stat-item">
              <h6 class="name">Montly</h6>
              <p class="value">10.38%</p>
            </div>
            <div class="stat-item">
              <h6 class="name">24h</h6>
              <p class="value">3.38%</p>
            </div>
          </div>
          <b-progress variant="success" :value="60"
            :max="100" class="bg-gray-lighter progress-xs" />
          <p>
            <small>
              <span class="circle bg-warning text-white">
                <i class="fa fa-chevron-up" />
              </span>
            </small>
            <span class="fw-semi-bold">&nbsp;17% higher</span>
            &nbsp;than last month
          </p>
        </Widget>
      </b-col>
      
    </b-row> -->
  </div>
</template>

<script>
import Vue from 'vue';
import Widget from '@/components/Widget/Widget';
import Map from './components/Map/Map';
import AnimatedNumber from "animated-number-vue";
import AreaChart from './components/AreaChart/AreaChart';
import { BootstrapVueIcons } from 'bootstrap-vue'
import 'bootstrap-vue/src/icons.scss'
import {chartData, liveChart, liveChartInterval} from './mock';

import ECharts from 'vue-echarts/components/ECharts';
import 'echarts/lib/chart/line';
import Highcharts from 'highcharts';
import exporting from 'highcharts/modules/exporting';
import exportData from 'highcharts/modules/export-data';
import { Chart } from 'highcharts-vue';
import VueWeatherWidget from 'vue-weather-widget';
import 'vue-weather-widget/dist/css/vue-weather-widget.css';

exporting(Highcharts);
exportData(Highcharts);
import hcMore from "highcharts/highcharts-more";
import solidgauge from "highcharts/modules/solid-gauge";
hcMore(Highcharts);
solidgauge(Highcharts);

Vue.use(BootstrapVueIcons)

const todos = [
  {
    description: 'Take Sebastian to basketball practice.',
    isComplete: false,
    dates: { weekdays: 6, weeklyInterval: 2 }, // Every other Friday
    color: '#ff8080',       // Red
  },
  {
    description: 'German courses',
    isComplete: false,
    dates: new Date(),
    color: '#64a4ff',       // Red
  },
  {
    description: 'Constitution Day',
    isComplete: false,
    dates: new Date(Date.now() + 6*24*60*60*1000), // in 6 days
    color: '#6ae696',       // Red
  },
];

export default {
  name: 'Dashboard',
  components: {
    Widget,
    echart: ECharts,
    highcharts: Chart,
    Map,
    AnimatedNumber,
    'weather': VueWeatherWidget,
    AreaChart
  },
  data() {
    return {
      cd: chartData,
      ld: liveChart,
      initEchartsOptions: {
        renderer: 'canvas'
      },
      nutrientChartOptions: {
      chart: {
        type: 'bar',
        backgroundColor: 'transparent',
        height: 230
      },
      title: null,
      xAxis: {
        categories: ['Nitrogen', 'Potassium', 'Phosphorus'],
        title: {
          text: null,
        },
      },
      yAxis: {
        min: 0,
        title: {
          text: 'Kg/hectare',
          align: 'high',
        },
        gridLineWidth: 0,
        labels: {
          overflow: 'justify',
        },
      },
        exporting: {
            enabled: false
        },

        tooltip: {
            enabled: false
        },
      plotOptions: {
        bar: {
          dataLabels: {
            enabled: true,
          },
        },
      },
      legend: {
        layout: 'vertical',
        align: 'right',
        verticalAlign: 'top',
        x: -40,
        y: 80,
        floating: true,
        borderWidth: 1,
        backgroundColor:
          (Highcharts.theme && Highcharts.theme.legendBackgroundColor) || '#FFFFFF',
        shadow: true,
      },
      credits: {
        enabled: false,
      },
        colors: [
            '#ff0000',
            '#f0af03',
            '#0000ff'
        ],
      series: [
        {
                      colorByPoint: true,

    showInLegend: false,
          data: [
            {y:20, color:'#80BF4C'}, {y:10, color:'#D16654'}, {y:17,color:'#D2DA49'}
            ],
        }
      ],
    },
      phChartOptions: {

        chart: {
            type: 'gauge',
            backgroundColor: 'transparent',
            height:230
        },

   title: null,

       exporting: {
        enabled: false
    },

    tooltip: {
        enabled: false
    },
       credits: {
        enabled: false
    },

        pane: {
            startAngle: -90,
            endAngle: 90, 
            background: null,
            center: ['50%', '85%'],
            size: '140%'
        },

        // the value axis
        yAxis: {
            min: 0,
            max: 14,
        lineWidth: 0,
        tickWidth: 0,
        minorTickInterval: null,
            title: {
                text: 'pH'
            },
            plotBands: [{
                from: 0,
                to: 6,
                color: '#DF5353  ' // red
            }, {
                from: 6,
                to: 8,
                color: '#55BF3B' // yellow
            }, {
                from: 8,
                to: 14,
                color: '#DDDF0D' // red
            }]
        },

        series: [{
            name: 'Speed',
            data: [6],
            tooltip: {
                valueSuffix: ' km/h'
            }
        }]

      },

      chartOptions: {
    chart: {
        type: 'solidgauge',
        height: 230,
        backgroundColor: 'transparent'

    },

    title: null,

    pane: {
        center: ['50%', '85%'],
        size: '140%',
        startAngle: -90,
        endAngle: 90,
        background: {
            backgroundColor:
                Highcharts.defaultOptions.legend.backgroundColor || '#EEE',
            innerRadius: '60%',
            outerRadius: '100%',
            shape: 'arc'
        }
    },

    exporting: {
        enabled: false
    },

    tooltip: {
        enabled: false
    },

    // the value axis
    yAxis: {
        stops: [
            [0.1, '#55BF3B'], // green
            [0.5, '#DDDF0D'], // yellow
            [0.9, '#DF5353'] // red
        ],
        lineWidth: 0,
        tickWidth: 0,
        minorTickInterval: null,
        tickAmount: 2,
        title: {
            y: -70
        },
        labels: {
            y: 16
        },
                min: 0,
        max: 100,
        title: {
            text: 'Humidity'
        }
    },

    plotOptions: {
        solidgauge: {
            dataLabels: {
                y: 5,
                borderWidth: 0,
                useHTML: true
            }
        }
    },
    // yAxis: {
    //     min: 0,
    //     max: 100,
    //     title: {
    //         text: 'Humidity'
    //     }
    // },

    credits: {
        enabled: false
    },

    series: [{
        name: 'Speed',
        data: [43],
        dataLabels: {
            format:
                '<div style="text-align:center">' +
                '<span style="font-size:25px">{y}</span><br/>' +
                '<span style="font-size:12px;opacity:0.4">%</span>' +
                '</div>'
        },
        tooltip: {
            valueSuffix: '%'
        }
    }]
    },

    chartOptions2: {
    chart: {
        type: 'solidgauge',
        height: 230,
        backgroundColor: 'transparent'

    },

    title: null,

    pane: {
        center: ['50%', '85%'],
        size: '140%',
        startAngle: -90,
        endAngle: 90,
        background: {
            backgroundColor:
                Highcharts.defaultOptions.legend.backgroundColor || '#EEE',
            innerRadius: '60%',
            outerRadius: '100%',
            shape: 'arc'
        }
    },

    exporting: {
        enabled: false
    },

    tooltip: {
        enabled: false
    },

    // the value axis
    yAxis: {
        stops: [
            [0.1, '#DF5353'], // red
        // green
            [0.5, '#DDDF0D'], // yellow
                             [0.9, '#55BF3B']
        ],
        lineWidth: 0,
        tickWidth: 0,
        minorTickInterval: null,
        tickAmount: 2,
        title: {
            y: -70
        },
        labels: {
            y: 16
        },
        min: 0,
        max: 85000,
        title: {
            text: 'Light'
        }
    },

    plotOptions: {
        solidgauge: {
            dataLabels: {
                y: 10,
                borderWidth: 0,
                useHTML: true
            }
        }
    },
    // yAxis: {
    //     min: 0,
    //     max: 100,
    //     title: {
    //         text: 'Humidity'
    //     }
    // },

    credits: {
        enabled: false
    },

    series: [{
        name: 'Speed',
        data: [13000],
        dataLabels: {
            format:
                '<div style="text-align:center">' +
                '<span style="font-size:25px">{y}</span><br/>' +
                '<span style="font-size:12px;opacity:0.4">lux</span>' +
                '</div>'
        },
        tooltip: {
            valueSuffix: '%'
        }
    }]
    },

    chartmoisture: {
    chart: {
        type: 'solidgauge',
        height: 230,
        backgroundColor: 'transparent'

    },

    title: null,

    pane: {
        center: ['50%', '85%'],
        size: '140%',
        startAngle: -90,
        endAngle: 90,
        background: {
            backgroundColor:
                Highcharts.defaultOptions.legend.backgroundColor || '#EEE',
            innerRadius: '60%',
            outerRadius: '100%',
            shape: 'arc'
        }
    },

    exporting: {
        enabled: false
    },

    tooltip: {
        enabled: false
    },

    // the value axis
    yAxis: {
        stops: [
            
            [0.1, '#55BF3B'],
        // green
            [0.6, '#DDDF0D'], // yellow

            [0.8, '#DF5353'], // red
      
        ],
        lineWidth: 0,
        tickWidth: 0,
        minorTickInterval: null,
        tickAmount: 2,
        title: {
            y: -70
        },
        labels: {
            y: 16
        },
        min: 0,
        max: 100,
        title: {
            text: 'Moisture'
        }
    },

    plotOptions: {
        solidgauge: {
            dataLabels: {
                y: 10,
                borderWidth: 0,
                useHTML: true
            }
        }
    },
    // yAxis: {
    //     min: 0,
    //     max: 100,
    //     title: {
    //         text: 'Humidity'
    //     }
    // },

    credits: {
        enabled: false
    },

    series: [{
        name: 'Speed',
        data: [15],
        dataLabels: {
            format:
                '<div style="text-align:center">' +
                '<span style="font-size:25px">{y}</span><br/>' +
                '<span style="font-size:12px;opacity:0.4">%</span>' +
                '</div>'
        },
        tooltip: {
            valueSuffix: '%'
        }
    }]
    },

      animateNumberOptions: {
        duration: 2000,
        easing: 'easeInQuad',
        formatValue(value) {
          return value.toFixed(0);
        }
      },
      checkedArr: [false, false, false],
      dataCollection: null,
      todos
    };
  },
  mounted () {
    this.fillData();
  },
  methods: {
    phChartCallback(chart) {
      if (!chart.renderer.forExport) {
setInterval(function () {
    // Speed
                var point = chart.series[0].points[0],
                newVal = 0;

                while(newVal <=4 || newVal>=8){
                  newVal = Math.round((Math.random()) * 10);
                }
                point.update(newVal);
    
}, 2000);}
},

chartCallback1(chart) {

if (!chart.renderer.forExport) {

setInterval(function () {

// Speed

var point,
newVal,
inc;
newVal = 0;
point = chart.series[0].points[0];
while (newVal<=13000 || newVal>=14500){
inc = Math.round((Math.random()) * 30000);
newVal = inc;
}
point.update(newVal);
}, 2000);

}

},

chartCallback4(chart) {

if (!chart.renderer.forExport) {

setInterval(function () {

// Speed

var point,
newVal,
inc;
newVal = 0;
point = chart.series[0].points[0];

while (newVal<=16 || newVal>=19){
inc = Math.round((Math.random()) * 100);
newVal = inc;
}
point.update(newVal);
// point1.update(newVal);
}, 2000);

}

},


chartCallback3(chart) {

if (!chart.renderer.forExport) {

setInterval(function () {

// Speed

var point,
newVal,
inc;
newVal = 0;
point = chart.series[0].points[0];
while (newVal<=15 || newVal>=20){
inc = Math.round((Math.random()) * 100);
newVal = inc;
}
point.update(newVal);
}, 2000);

}

},

    chartCallback(chart) {

if (!chart.renderer.forExport) {

setInterval(function () {

// Speed

var point,

newVal,

inc;
newVal = 0;
point = chart.series[0].points[0];
while (newVal<=43 || newVal>=47){
inc = Math.round((Math.random()) * 100);
newVal = inc;
}



point.update(newVal);


}, 2000);

}

},

    checkTable(id) {
      let arr = [];
      if (id === 0) {
        const val = !this.checkedArr[0];
        for (let i = 0; i < this.checkedArr.length; i += 1) {
          arr[i] = val;
        }
      } else {
        arr = this.checkedArr;
        arr[id] = !arr[id];
      }
      if (arr[0]) {
        let count = 1;
        for (let i = 1; i < arr.length; i += 1) {
          if (arr[i]) {
            count += 1;
          }
        }
        if (count !== arr.length) {
          arr[0] = !arr[0];
        }
      }
      Vue.set(this, 'checkedArr', arr);
    },
    fillData () {
      this.dataCollection = {
        labels: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            borderColor: 'transparent',
            data: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
          }, {
            label: 'Data Two',
            backgroundColor: '#7c87f8',
            borderColor: 'transparent',
            data: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
          }
        ]
      }
    },
    getRandomInt () {
      return Math.floor(Math.random() * (50 - 5 + 1)) + 5
    }
  },
  computed: {
    calendarAttributes() {
      return [
        // Today attribute
        {
          contentStyle: {
            fontWeight: '700',
            fontSize: '.9rem',
          },
          dates: new Date(),
        },
        // Attributes for todos
        ...this.todos.map(todo => ({
          dates: todo.dates,
          dot: {
            backgroundColor: todo.color,
            opacity: todo.isComplete ? 0.3 : 1,
          },
          popover: {
            label: todo.description,
          },
        })),
      ];
    },
  }
};
</script>

<style src="./Dashboard.scss" lang="scss" />
