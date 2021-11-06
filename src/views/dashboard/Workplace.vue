<template>
  <a-layout  class="layout-right">
    <div >
      <a-form layout="horizontal">
        <div >
          <a-row >
            <a-col :md="8" :sm="24" >
              <a-form-item
                label="查询时间"
                :labelCol="{span: 5}"
                :wrapperCol="{span: 18, offset: 1}"
              >
                <a-range-picker show-time format="YYYY/MM/DD HH:mm:ss"/>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <span style="float:right;margin-top:3px;">
                <a-button type="primary">查询</a-button>
              </span>
            </a-col>
          </a-row>
        </div>
      </a-form>
    </div>
    <div class="m-3" >
      <el-row>
        <div style="width:auto;margin:0;height:250px;" id="cvsMain1">
        </div>
      </el-row >
      <el-row >
        <div style="width:auto;margin:0;height: 250px;" id="cvsMain2">
        </div>
      </el-row>
    </div>
  </a-layout >
</template>
<script>
import Plotly from 'plotly.js/dist/plotly'
import moment from 'moment'
export default {
  components: {
  },
  data () {
    return {
        data: [],
        layout: {
          autosize: true,
          title: '',
          showlegend: true,
          height: 235,
          xaxis: {
              title: '',
              showgrid: false,
              showline: true,
              showexponent: 'first',
              hoverformat: '%Y/%m/%d %H:%M',
              tickformat: ' %H:%M:%S \n %Y/%m/%d',
              mirror: true,
              tickangle: 0, // x时间轴横向展示
              // fixedrange:true,// 固定坐标轴范围
              zeroline: false
          },
          yaxis: {
              title: '高度(M)',
              titlefont: {
                  size: 12
              },
              showgrid: false,
              showline: true,
              showexponent: 'first',
              mirror: true,
              tickangle: 0,
              fixedrange: true, // 固定坐标轴范围
              // autorange:true, // 点击坐标轴不会出现自适应范围
              zeroline: false
                },
          margin: {
                    autoexpand: false,
                    l: 56,
                    r: 82,
                    t: 50,
                    b: 43
                }
        },
        config: {
          titlefont: 'afasfsa',
          displayModeBar: true,
          displaylogo: false,
          modeBarButtonsToRemove: [
                        'zoom2d', 'pan2d', 'select2d', 'lasso2d', 'zoomIn2d', 'zoomOut2d', 'autoScale2d', 'resetScale2d',
                        'hoverClosestCartesian', 'hoverCompareCartesian',
                        'zoom3d', 'pan3d', 'resetCameraDefault3d', 'resetCameraLastSave3d', 'hoverClosest3d',
                        'orbitRotation', 'tableRotation',
                        'zoomInGeo', 'zoomOutGeo', 'resetGeo', 'hoverClosestGeo',
                        'sendDataToCloud',
                        'hoverClosestGl2d',
                        'hoverClosestPie',
                        'toggleHover',
                        'resetViews',
                        'toggleSpikelines',
                        'resetViewMapbox',
                        'toImage'
                    ]
        }
    }
  },
  mounted () {
    this.fetchData()
  },
  created () {
  },
  methods: {
    moment,
    fetchData () {
      this.data = [
            {
                z: [[1, 20, 30], [20, 1, 60], [30, 60, 1]],
                colorscale: [
                      [0, 'rgb(0,0,139)'],
                      [0.2, 'rgb(0,0,255)'],
                      [0.4, 'rgb(0,255,255)'],
                      [0.6, 'rgb(0,128,0)'],
                      [0.8, 'rgb(255,255,0)'],
                      [1, 'rgb(255,0,0)']
                  ],
                colorbar: {
                    // thicknessmode:'fraction',
                    x: 1.03,
                    // y:0.5,
                    len: 1.06,
                    tickformat: '.1e',
                    exponentformat: 'E',
                    tickwidth: '1',
                    //  tickformat:'6f',
                    ticks: 'outside',
                    thickness: 12,
                    xanchor: 'left',
                    xpad: 0,
                    tickmode: 'array'
                },
                type: 'heatmap',
                zsmooth: 'best',
                zhoverformat: 'e',
                xaxis: 'x',
                yaxis: 'y'
            }
          ]
      Plotly.plot('cvsMain1', this.data, this.layout, this.config)
      Plotly.plot('cvsMain2', this.data, this.layout, this.config)
    }
  },
  computed: {
  }
}
</script>

<style scoped>

</style>
