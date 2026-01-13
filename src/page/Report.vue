<template>
  <div>
    <article class="pt-px">
      <Title class="mt-16">防詐大調查</Title>
      
      <h1 class="text-2xl lg:text-3xl xl:text-4xl sm:text-center mb-6 sm:my-8 xl:leading-snug mx-auto w-11/12 max-w-screen-lg min-h-[1.375em]">
        反詐大調查〉3成民眾每月收到詐騙訊息 高學歷、<br class="hidden sm:block">高齡者財損更多 多數認同刑責太輕 應強化阻詐
      </h1>
      <div class="container">
        <Introduction>
          <p>本刊最新調查顯示，詐騙訊息仍層出不窮，近八成認為台灣詐騙問題嚴重、且判刑應該再斟酌加重。</p>
          <p>為了落實反詐，目前已有多項註記資產的自保方法，多數人仍不知情、高齡者意願低，也都可能成為破口。</p>
        </Introduction>
      </div>
      
      <div class="container">
        <div class="content-wrapper my-16">
          <p class="mb-4">在保險業擔任中階主管的韋任（化名），平時是社群網站和通訊軟體的重度使用者，每周幾乎都會收到詐騙訊息的他，自認很熟悉五花八門的詐騙套路，總能在第一時間辨別，撕開詐團的假面；但是他家中七十多歲的獨居老父，可就不具備這種能力。</p>
          <p class="mb-4">半年前，韋任接到警局通知，他的父親落入常見的「交友結合投資詐騙」圈套，在素未謀面的「愛人」慫恿下，匯出退休老本三百多萬元。當時銀行行員和警察聯手，使勁勸阻兩個多小時，老人家仍然執意匯款，氣得在銀行大鬧一場。</p>
          <p class="mb-4">「被詐騙的人，就像著了魔，好說歹說都聽不進去，匯完錢之後，他竟然還想拿房子去借款……。」韋任憤慨地說，他無法相信自己的父親會做出傻事，事發後，父子倆的關係幾乎降到冰點。如果時光倒轉回半年前，熟悉各種詐術的韋任，能對親友多一句提醒，替長輩多增設一道銀行預警防線，結局會不一樣嗎？</p>
          <p class="mb-4">為了解民眾被詐騙情形，以及對各項防範機制的接受度，《今周刊》委託山水民調公司，針對全國十八歲以上民眾，進行《二○二五全民詐騙大調查》，期盼藉由去年的現況分析，提出政府與民間單位應加強著力的防詐方向。</p>
        </div>
      </div>
      
      <div class="container pb-20">
        <div class="content-wrapper my-16 space-y-4">
          <h3 class="text-xl sm:text-2xl text-primary font-medium">七十歲族群超過一成被騙過</h3>
          <h3 class="text-xl sm:text-2xl text-primary font-medium">教育程度高  也容易陷入受詐盲區</h3>
          <ChartType1 />
        </div>
        
        <div class="content-wrapper my-16">
          <ChartType2 />
        </div>
        
        <div class="content-wrapper my-16">
          <ChartType3 />
        </div>
        
        <!-- 返回按鈕 -->
        <div class="flex justify-center my-16">
          <button
            @click="goToAntiFraud"
            class="inline-block relative border border-primary text-primary text-lg px-4 py-2 rounded-md
            @media-hover:hover:bg-primary @media-hover:hover:text-white cursor-pointer"
          >
            返回防詐專區
          </button>
        </div>
      </div>
    </article>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
import Title from '../components/Title.vue'
import Introduction from '../components/Introduction.vue'
import ChartType1 from '../components/charts/ChartType1.vue'
import ChartType2 from '../components/charts/ChartType2.vue'
import ChartType3 from '../components/charts/ChartType3.vue'

const router = useRouter()

const goToAntiFraud = () => {
  // 使用 router.push 並滾動到頂部
  router.push('/').then(() => {
    window.scrollTo(0, 0)
  })
}
</script>