<template>
  <div class="space-y-4">
    <p>從接觸詐騙訊息的管道來看，整體而言，手機來電占逾三成，社群媒體和手機簡訊則分別占超過二三％，均高於通訊軟體所占的十五％。</p>
    <p>進一步與年齡交叉分析，則呈現顯著的世代差異。三十九歲以下受試者，有約六成是透過社群媒體和通訊軟體接觸疑似詐騙訊息；逾六十歲以上長者，接觸管道則較為單純，逾七成是透過手機來電或家用電話兩種途徑，凸顯未來如何強化來電辨識機制，是高齡詐騙的防範重點。</p>
    <br>
    <ChartGroup :sliderData="chartData" />
  </div>
</template>

<script setup>
import ChartGroup from './ChartGroup.vue';

import useClientSize from '../../composables/useClientSize'
const { isMobile } = useClientSize();

const chartData = [
  {
    title: '過去一年中，您大約多久接觸到一次意圖詐騙訊息？',
    subtitle: '(包含疑似詐騙電話、訊息、廣告、真人對談等)',
    after: '<p class="mt-4">整體逾3成民眾，每月至少接收一次意圖詐騙訊息；其中30歲到49歲青壯年族群，逾2成每周至少接觸一次。</p>',
    options: {
      "yAxis": {
        "type": "category",
        "inverse": true,
        "axisLabel": {"fontFamily": "Noto Sans TC"},
        "data": [
          "每周至少一次",
          "約每月一次",
          "幾個月一次",
          "一年一次",
          "沒有",
          "不知道／拒答"
        ]
      },
      "series": [{
        "data": [14.5, 18.5, 23.2, 9.4, 30.5, 3.8],
        "type": "bar",
        "label": {"show": true, "formatter": "{c}%"}
      }]
    }
  },
  {
    title: '當您接到意圖詐騙訊息，您通常會採取哪些行動？',
    subtitle: '(複選)',
    after: '<p class="mt-4">去年《今周刊》防詐大調查中，有85.4％民眾表示在接觸疑似詐騙訊息時，不會報案或檢舉；今年同樣有逾8成民眾，接獲詐騙訊息後會直接忽略和刪除。</p>',
    options: {
      "yAxis": {
        "type": "category",
        "inverse": true,
        "axisLabel": {"fontFamily": "Noto Sans TC"},
        "data": [
          "知道是詐騙\n，直接忽略或刪除",
          "主動分享給\n家人或朋友",
          "向警察單位\n、金融機構或\n反詐騙165專線通報",
          "向社群平台或\n通訊軟體檢舉",
          "將相關訊息發布到\n社群媒體或群組",
          "自行上網查證\n，但未主動通報或\n分享給他人",
          "無明確意見"
        ]
      },
      "series": [{
        "data": [{ value: 81.7, itemStyle: {color: '#fc8452'} }, { value: 48.2, itemStyle: {color: '#fc8452'} }, 22.1, 15.3, 11.2, 6.2, 1.4],
        "type": "bar",
        "label": {
          "show": true,
          formatter: params => (params.value > 5 ? params.value + '%' : ''),
        }
      }]
    }
  },
  {
    title: '當您接到意圖詐騙訊息，您通常會採取哪些行動？',
    subtitle: '交叉分析性別',
    after: '<p class="mt-4">主動分享詐騙訊息、向相關單位通報或檢舉的女性比率較高。</p>',
    options: {
      color: ['#5470c6', '#fc8452'],
      tooltip: {
        trigger: 'axis',
        axisPointer: { type: 'shadow' },
        confine: true,
        formatter: (par) => {
          return par.reduce((prev, current) => {
            if (current.seriesName === 'labelName') return prev;
            return `${prev}<p class="text-sm">${current.marker} <span>${current.seriesName}: ${current.value}%</span></p>`
          }, `<p class="font-bold text-base mb-1">${par[0].axisValue}</p>`)
        }
      },
      xAxis: { type: 'value', },
      yAxis: {
        type: 'category',
        inverse: true,
        axisLabel: {"fontFamily": "Noto Sans TC"},
        data: ['知道是詐騙，直接忽略或刪除', '主動分享給家人或朋友', '向警察單位、金融機構或反詐騙165專線通報', '向社群平台或通訊軟體檢舉', '將相關訊息發布到社群媒體或群組', '自行上網查證，但未主動通報或分享給他人', '無明確意見'],
        axisLabel: { show: false },
      },
      grid: { left: 0, top: 60, right: 0, bottom: 0 },
      legend: {
        show: true,
        itemGap: 15,
        data: ['男性', '女性'],
      },
      series: [
        {
          name: 'labelName', // 偽yAxis label
          type: 'bar',
          data: [0, 0, 0, 0, 0, 0, 0],
          barWidth: 0,
          label: {
            show: true,
            position: [10, -20],
            formatter: (params) => params.name,
            color: '#7f7f7f',
            fontWeight: 'bold',
            fontSize: 16,
          },
          itemStyle: { color: 'transparent' },
          emphasis: { disabled: true },
          legendHoverLink: false,
        },
        {
          name: '男性', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [83.4, 40.5, 18, 14.7, 8.6, 6.3, 1.6]
        },
        {
          name: '女性', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [80, 55.5, 26.1, 15.8, 13.7, 6.1, 1.2]
        }
      ]
    }
  },
  {
    title: '您有沒有曾經被詐騙或瀕臨被騙的經驗？',
    subtitle: '',
    after: '<p class="mt-4">其中2%造成難以回復的重大財損。</p>',
    options: {
      tooltip: {
        trigger: 'item',
        formatter: (par) => {
          const { name, value } = par.data
          const title = `<div class="text-sm tracking-normal break-all whitespace-pre-wrap">${name.replace(/\n/g, '')}</div>`
          return `${title}<strong class="text-base" style="color: ${par.color}">${value}%</strong>`
        }
      },
      title: [
        {
          text: '',
          left: '50%',
          top: '2%',
          textAlign: 'center',
          textStyle: {
            color: '#505050',
            fontFamily: 'Noto Sans TC',
            fontWeight: '500',
          },
        },
      ],
      series: [
        {
          type: 'pie',
          radius: ['35%', '60%'],
          center: ['50%', '50%'],
          itemStyle: {
            borderRadius: 5,
            borderColor: '#fff',
            borderWidth: 2
          },
          label: {
            show: true,
            formatter: '{b}\n{c}%',
            fontWeight: '500',
            fontSize: 15,
            position: 'outside',
          },
          emphasis: {label: { show: true }},
          data: [
            { value: 9, name: '曾被詐騙，造成財務損失', itemStyle: { color: '#5470c6' }},
            { value: 14.5, name: '差點被騙，但及時察覺並成功脫離，未造成財損', itemStyle: { color: '#91cc75' }},
            { value: 75.2, name: '目前為止都能辨識出詐騙', itemStyle: { color: '#fc8452' }},
            { value: 1.3, name: '不確定／無法判斷', itemStyle: { color: '#c3c3c3' }},
          ]
        },
      ],
    }
  },
  {
    title: '您有沒有曾經被詐騙或瀕臨被騙的經驗？',
    subtitle: '交叉分析年齡',
    after: '<p class="mt-4">其中3.4%造成重大財損，較其他年齡層財損金額更高。</p>',
    options: {
      color: ['#5470c6', '#fc8452', '#91cc75', '#fac858'],
      tooltip: {
        trigger: 'axis',
        axisPointer: { type: 'shadow' },
        confine: true,
        formatter: (par) => {
          return par.reduce((prev, current) => {
            if (current.seriesName === 'labelName') return prev;
            return `${prev}<p class="text-sm">${current.marker} <span>${current.seriesName}: ${current.value}%</span></p>`
          }, `<p class="font-bold text-base mb-1">${par[0].axisValue}</p>`)
        }
      },
      xAxis: { type: 'value', },
      yAxis: {
        type: 'category',
        inverse: true,
        axisLabel: {"fontFamily": "Noto Sans TC"},
        data: ['18-29歲', '30-39歲', '40-49歲', '50-59歲', '60-69歲', '70歲以上'],
        axisLabel: { show: false },
      },
      grid: { left: 0, top: 60, right: 0, bottom: 0 },
      legend: {
        show: true,
        itemGap: 15,
        data: ['曾被詐騙造成財損', '差點被騙未有財損', '目前都能辨識', '不確定／無法判斷'],
      },
      series: [
        {
          name: 'labelName', // 偽yAxis label
          type: 'bar',
          data: [0, 0, 0, 0, 0, 0],
          barWidth: 0,
          label: {
            show: true,
            position: [10, -20],
            formatter: (params) => params.name,
            color: '#7f7f7f',
            fontWeight: 'bold',
            fontSize: 16,
          },
          itemStyle: { color: 'transparent' },
          emphasis: { disabled: true },
          legendHoverLink: false,
        },
        {
          name: '曾被詐騙造成財損', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [8, 9.9, 9.1, 7.1, 6.7, 11.7]
        },
        {
          name: '差點被騙未有財損', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [13.4, 15, 14.9, 13.9, 15.5, 15.3]
        },
        {
          name: '目前都能辨識', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [76.6, 75.1, 74.2, 78.7, 76.6, 71.2]
        },
        {
          name: '不確定／無法判斷', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [2, 0, 1.8, 0.3, 1.2, 1.8]
        }
      ]
    }
  },
  {
    title: '您有沒有曾經被詐騙或瀕臨被騙的經驗？',
    subtitle: '交叉分析學歷',
    after: '<p class="mt-4">學歷為研究所的受訪者，曾遭詐騙比率高於其他教育程度者，造成重大財損的比率也較整體高。</p>',
    options: {
      color: ['#5470c6', '#fc8452', '#91cc75', '#fac858'],
      tooltip: {
        trigger: 'axis',
        axisPointer: { type: 'shadow' },
        confine: true,
        formatter: (par) => {
          return par.reduce((prev, current) => {
            if (current.seriesName === 'labelName') return prev;
            return `${prev}<p class="text-sm">${current.marker} <span>${current.seriesName}: ${current.value}%</span></p>`
          }, `<p class="font-bold text-base mb-1">${par[0].axisValue}</p>`)
        }
      },
      xAxis: { type: 'value', },
      yAxis: {
        type: 'category',
        inverse: true,
        axisLabel: {"fontFamily": "Noto Sans TC"},
        data: ['國中以下', '高中職', '專科', '大學', '碩、博士'],
        axisLabel: { show: false },
      },
      grid: { left: 0, top: 60, right: 0, bottom: 0 },
      legend: {
        show: true,
        itemGap: 15,
        data: ['曾被詐騙造成財損', '差點被騙未有財損', '目前都能辨識', '不確定／無法判斷'],
      },
      series: [
        {
          name: 'labelName', // 偽yAxis label
          type: 'bar',
          data: [0, 0, 0, 0, 0],
          barWidth: 0,
          label: {
            show: true,
            position: [10, -20],
            formatter: (params) => params.name,
            color: '#7f7f7f',
            fontWeight: 'bold',
            fontSize: 16,
          },
          itemStyle: { color: 'transparent' },
          emphasis: { disabled: true },
          legendHoverLink: false,
        },
        {
          name: '曾被詐騙造成財損', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [9.5, 6.9, 7.7, 9.5, 11.7]
        },
        {
          name: '差點被騙未有財損', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [15.7, 13.3, 17.4, 13.4, 16.6]
        },
        {
          name: '目前都能辨識', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [74.4, 77.5, 71.9, 76.5, 71.7]
        },
        {
          name: '不確定／無法判斷', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [0.3, 2.3, 3.0, 0.6, 0]
        }
      ]
    }
  },
]
</script>