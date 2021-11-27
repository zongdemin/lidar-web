<template>
  <page-header-wrapper >
    <div class="table-page-search-wrapper">
      <a-form layout="inline">
        <a-row :gutter="48">
          <a-col :md="12" :sm="24">
            <a-form-item label="查询时间">
              <a-range-picker show-time format="YYYY/MM/DD HH:mm:ss" />
            </a-form-item>
          </a-col>
          <a-col :md="8" :sm="12">
            <a-form-item label="演算数据">
              <a-select v-model="multiple" placeholder="请选择" default-value="[0, 1]" @change="onChange">
                <a-select-option value="0">A通道原始信信号</a-select-option>
                <a-select-option value="1">B通道原始信信号</a-select-option>
                <a-select-option value="2">退偏比</a-select-option>
              </a-select>
            </a-form-item>
          </a-col>
          <a-col :md="6" :sm="24">
            <a-form-item label="Max Length">
              <a-input-number v-model="lazy" style="width: 100%"/>
            </a-form-item>
          </a-col>
          <a-col :md="6" :sm="24">
            <a-form-item label="Min Length">
              <a-input-number v-model="lazy" style="width: 100%"/>
            </a-form-item>
          </a-col>
           <a-col :md="6" :sm="24">
            <a-form-item label="色谱柱最小值">
              <a-input-number v-model="lazy" style="width: 100%"/>
            </a-form-item>
          </a-col>
          <a-col :md="6" :sm="24">
            <a-form-item label="色谱柱最大值">
              <a-input-number v-model="lazy" style="width: 100%"/>
            </a-form-item>
          </a-col>
          <a-col :md="!advanced && 8 || 24" :sm="24">
            <span class="table-page-search-submitButtons" :style="advanced && { float: 'right', overflow: 'hidden' } || {} ">
              <a-button type="primary" @click="$refs.table.refresh(true)">查询</a-button>
              <a-button style="margin-left: 8px" @click="() => queryParam = {}">重置</a-button>
              <a @click="toggleAdvanced" style="margin-left: 8px">
                {{ advanced ? '收起' : '展开' }}
                <a-icon :type="advanced ? 'up' : 'down'"/>
              </a>
            </span>
          </a-col>
        </a-row>
      </a-form>
    </div>
    <a-layout  class="layout-right">
      <div class="m-3" >
        <a-row>
          <div style="width:1000px;margin:0;height:200px;" id="cvsMain1">
          </div>
        </a-row >
        <a-row >
          <div style="width:1000px;margin:0;height:200px;" id="cvsMain2">
          </div>
        </a-row>
      </div>
    </a-layout >
  </page-header-wrapper>
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
              // fixedrange: true, // 固定坐标轴范围
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
                z: [[1, 4, 7], [2, 5, 8], [3, 6, 9]],
                x: ['一', '二', '三'],
                y: ['10', '100', '1000'],
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
                xaxis: '时间',
                yaxis: '高度'
            }
          ]
      Plotly.newPlot('cvsMain1', this.data, this.layout, this.config)
      Plotly.newPlot('cvsMain2', this.data, this.layout, this.config)
    },
    onChange (value) {
      console.log('您选择了：' + value)
    }
  },
  computed: {
  }
}
</script>

<style scoped>

</style>
