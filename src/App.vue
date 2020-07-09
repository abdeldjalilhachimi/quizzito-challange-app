<template>
  <div id="app" class="container">
    <h1 class="mb-4"> 
      Quizzito App for kids 
    </h1>
    <b-alert v-if="isFinished" show> {{ score }} / {{ questions.length }} :  النتيجة       </b-alert>
    <b-card :header="questions[index].question"
            header-tag="header">
      <b-list-group>
        <b-list-group-item 
          button 
          v-for="(item, index) in questions[index].answers" 
          :key="item.id"
          @click="action(index)"
          :variant="variants[index]">
          {{ item }}
        </b-list-group-item>
      </b-list-group>
      <b-button v-if="isFinished" @click="reStart" class="mt-4"> اعد محاولة من جديد</b-button>


      <b-button v-if="isRespond && !isFinished" @click="contunie" class="mt-4"  > موافق </b-button>

      
    </b-card>
  </div>
</template>

<script>
export default {
  name: "app",
  data: function() {
    return {
      isFinished: false,
      index: 0,
      score: 0,
      variants: [...Array(3)],
      isRespond: false,
      questions: [
        {
          question: "ماذا مَدَ الأسد كعلامة على صداقته مع الثعلب ؟",
          answers: ["ذيله", "لسانه", "يده"],
          ok: 0,
        },
        {
          question: "لماذا كان الثعلب يتجول في الغابة ؟",
          answers: ["يبحث عن إبنه", "يبحث عن فريسة", "يبحث عن صديقه"],
          ok: 1,
        },
        {
          question: "كيف كان الحيوان الغريب الذي رآه الثعلب؟",
          answers: ["كبيرا و طيبا", "كبيرا و مخيفا", "صغيرا و مخيفا"],
          ok: 1,
        },
      ],
    };
  },
  methods: {
    action: function(index) {
      if (index == this.questions[this.index].ok) {
        this.score++;
      } else {
        this.variants[index] = "danger";
      }
      this.isRespond = true;
      this.variants[this.questions[this.index].ok] = "success";
      if (this.index == this.questions.length - 1) {
        this.isFinished = true;
      }
    },
    reStart: function() {
      this.isRespond = this.isFinished = this.index = this.score = 0;
      this.variants = [...Array(3)];
    },
    contunie: function() {
      this.isRespond = false;
      this.variants = [...Array(3)];
      this.index++;
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 20px;
}
</style>
