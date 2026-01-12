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
    after: '<p class="mt-4">※整體逾3成民眾，每月至少接收一次意圖詐騙訊息；其中30歲到49歲青壯年族群，逾2成每周至少接觸一次。</p>',
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
          "不知道／拒答",
          "沒有詐騙訊息"
        ]
      },
      "series": [{
        "data": [14.5, 18.5, 23.2, 9.4, 3.8, 30.5],
        "type": "bar",
        "label": {"show": true, "formatter": "{c}%"}
      }]
    }
  },
  {
    title: '當您接到意圖詐騙訊息，您通常會採取哪些行動？',
    subtitle: '(複選)',
    after: '<p class="mt-4">※去年《今周刊》防詐大調查中，有85.4％民眾表示在接觸疑似詐騙訊息時，不會報案或檢舉；今年同樣有逾8成民眾，接獲詐騙訊息後會直接忽略和刪除。</p>',
    options: {
      "yAxis": {
        "type": "category",
        "inverse": true,
        "axisLabel": {"fontFamily": "Noto Sans TC"},
        "data": [
          "知道是詐騙，\n直接忽略或刪除",
          "主動分享給\n家人或朋友",
          "向警察單位、\n金融機構或\n反詐騙165專線通報",
          "向社群平台或\n通訊軟體檢舉",
          "自行上網查證，\n但未主動通報或\n分享給他人",
          "無明確意見"
        ]
      },
      "series": [{
        "data": [{ value: 81.7, itemStyle: {color: '#fc8452'} }, { value: 48.2, itemStyle: {color: '#fc8452'} }, 22.1, 15.3, 11.2, 6.2, 1.4],
        "type": "bar",
        "label": {"show": true, "formatter": "{c}%"}
      }]
    }
  },
  {
    title: '當您接到意圖詐騙訊息，您通常會採取哪些行動？',
    subtitle: '學歷交叉分析',
    after: '<p class="mt-4">※主動分享詐騙訊息、向相關單位通報或檢舉的女性比率較高。</p>',
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
    after: '<p class="mt-4">※其中2%造成難以回復的重大財損。</p>',
    options: {
      "yAxis": {
        "type": "category",
        "inverse": true,
        "axisLabel": {"fontFamily": "Noto Sans TC"},
        "data": [
          "曾被詐騙，\n造成財務損失",
          "差點被騙，\n但及時察覺\n並成功脫離，\n未造成財損",
          "目前為止\n都能辨識出詐騙",
          "不確定／無法判斷"
        ]
      },
      "series": [{
        "data": [{ value: 81.7, itemStyle: {color: '#fc8452'} }, 11.2, 6.2, 1.4],
        "type": "bar",
        "label": {
          "show": true,
          formatter: params => (params.value > 5 ? params.value + '%' : ''),
        }
      }]
    }
  },
  {
    title: '您有沒有曾經被詐騙或瀕臨被騙的經驗？',
    subtitle: '交叉分析年齡',
    after: '<p class="mt-4">※其中3.4%造成重大財損，較其他年齡層財損金額更高。</p>',
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
          name: '18-29歲', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [8, 13.4, 76.6, 2]
        },
        {
          name: '30-39歲', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [9.9, 15, 75.1, 0]
        },
        {
          name: '40-49歲', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [9.1, 14.9, 74.2, 1.8]
        },
        {
          name: '50-59歲', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [7.1, 13.9, 78.7, 0.3]
        },
        {
          name: '60-69歲', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [6.7, 15.5, 76.6, 1.3]
        },
        {
          name: '70歲以上', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [11.7, 15.3, 71.2, 1.9]
        }
      ]
    }
  },
  {
    title: '您有沒有曾經被詐騙或瀕臨被騙的經驗？',
    subtitle: '交叉分析學歷',
    after: '<p class="mt-4">※學歷為研究所的受訪者，曾遭詐騙比率高於其他教育程度者，造成重大財損的比率也較整體高。</p>',
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
          data: [0, 0, 0, 0],
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
          name: '國中以下', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [9.5, 15.7, 74.4, 0.3]
        },
        {
          name: '高中職', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [6.9, 13.3, 77.5, 2.3]
        },
        {
          name: '專科', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [7.7, 17.4, 71.9, 3]
        },
        {
          name: '大學', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [9.5, 13.4, 76.5, 0.6]
        },
        {
          name: '碩、博士', type: 'bar', stack: 'total',
          label: {
            show: true,
            formatter: params => (params.value > 5 ? params.value + '%' : ''),
          },
          emphasis: { focus: 'series' },
          barWidth: 45,
          data: [11.7, 16.6, 71.7, 0]
        }
      ]
    }
  },
  // {
  //   title: '今年與去年相比，您接觸到的詐騙訊息是更多還是更少？',
  //   subtitle: '',
  //   options: {
  //     series: [
  //       {
  //         type: 'pie',
  //         radius: isMobile.value ? ['20%', '45%'] : ['35%', '60%'],
  //         avoidLabelOverlap: false,
  //         itemStyle: {
  //           borderRadius: 5,
  //           borderColor: '#fff',
  //           borderWidth: 2
  //         },
  //         data: [
  //           { value: 31.8, name: '更多' },
  //           { value: 24.5, name: '一樣' },
  //           { value: 31.8, name: '更少' },
  //           { value: 11.9, name: '不知道/拒答' }
  //         ],
  //         label: {
  //           show: true,
  //           formatter: '{b}\n{c}%',
  //           fontWeight: '500',
  //           fontSize: 15,
  //           position: 'outside',
  //         },
  //       }
  //     ]
  //   }
  // },
  // {
  //   title: '',
  //   subtitle: '',
  //   after: '<p class="mt-4">※除了最盛行的投資詐騙，橫跨所有世代;其餘以年齡層來看，50歲以下接觸的樣態多集中在購物詐騙、假帳單詐騙；50歲以上則以假冒公務機關和假冒親友詐騙訊息最多。</p>',
  //   options: {
  //     tooltip: {
  //       trigger: 'axis',
  //       axisPointer: { type: 'shadow' },
  //       confine: true,
  //       formatter: (par) => {
  //         return par.reduce((prev, current) => {
  //           if (current.data === 0) return prev;
  //           return `${prev}<p class="text-sm">${current.marker} <span>${current.seriesName}: ${current.value}%</span></p>`
  //         }, `<p class="font-bold text-base mb-1">${par[0].axisValue}</p>`)
  //       }
  //     },
  //     xAxis: { type: 'value', },
  //     yAxis: {
  //       type: 'category',
  //       inverse: true,
  //       axisLabel: {"fontFamily": "Noto Sans TC"},
  //       data: ['18~29歲', '30~39歲', '40~49歲', '50~59歲', '60~69歲', '70歲以上'],
  //       axisLabel: { show: false },
  //     },
  //     grid: { left: 0, top: (isMobile.value ? 130 : 70), right: 0, bottom: 0 },
  //     legend: {
  //       show: true,
  //       itemGap: 15,
  //       data: ['投資詐騙', '購物詐騙', '假帳單詐騙', '中獎/優惠詐騙', '假冒親友詐騙', '假冒公務機關', '勒索恐嚇詐騙', '假融資詐騙', '交友/愛情詐騙'],
  //     },
  //     series: [
  //       {
  //         name: 'labelName', // 偽yAxis label
  //         type: 'bar',
  //         data: [0, 0, 0, 0, 0, 0],
  //         barWidth: 0,
  //         label: {
  //           show: true,
  //           position: [10, -20],
  //           formatter: (params) => params.name,
  //           color: '#7f7f7f',
  //           fontWeight: 'bold',
  //           fontSize: 16,
  //         },
  //         itemStyle: { color: 'transparent' },
  //         emphasis: { disabled: true },
  //         legendHoverLink: false,
  //       },
  //       {
  //         name: '投資詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [39.4, 36.4, 37.9, 33, 27, 11.9]
  //       },
  //       {
  //         name: '購物詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [18.5, 29.8, 22.6, 8.3, 5.9, 0]
  //       },
  //       {
  //         name: '假帳單詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [0, 10.1, 7.6, 7.2, 12.8, 7.6]
  //       },
  //       {
  //         name: '中獎/優惠詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [8.4, 10.1, 5.5, 0, 0, 0]
  //       },
  //       {
  //         name: '假冒親友詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [0, 9.2, 0, 10.7, 14.7, 16.3]
  //       },
  //       {
  //         name: '假冒公務機關', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [0, 0, 6.5, 15.1, 14.8, 21.5]
  //       },
  //       {
  //         name: '勒索恐嚇詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [0, 0, 0, 0, 0, 10.8]
  //       },
  //       {
  //         name: '假融資詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [6.3, 0, 0, 0, 0, 0]
  //       },
  //       {
  //         name: '交友/愛情詐騙', type: 'bar', stack: 'total',
  //         label: {
  //           show: true,
  //           formatter: params => (params.value > 10 ? params.value + '%' : ''),
  //         },
  //         emphasis: { focus: 'series' },
  //         barWidth: 45,
  //         data: [5.9, 0, 0, 0, 0, 0]
  //       },
  //     ]
  //   }
  // },
  // {
  //   title: '您接觸到疑似詐騙訊息時<br>有沒有曾經向警方報案，或使用政府任一檢舉管道？',
  //   subtitle: '',
  //   options: {
  //     series: [
  //       {
  //         type: 'pie',
  //         radius: isMobile.value ? ['20%', '45%'] : ['35%', '60%'],
  //         avoidLabelOverlap: false,
  //         itemStyle: {
  //           borderRadius: 5,
  //           borderColor: '#fff',
  //           borderWidth: 2
  //         },
  //         data: [
  //           { value: 14.6, name: '有' },
  //           { value: 85.4, name: '沒有' },
  //         ],
  //         label: {
  //           show: true,
  //           formatter: '{b}\n{c}%',
  //           fontWeight: '500',
  //           fontSize: 15,
  //           position: 'outside',
  //         },
  //       }
  //     ]
  //   }
  // },
]
</script>