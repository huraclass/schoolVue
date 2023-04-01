
<style scoped>
.active{
  color:red;
}
.foo {
  background-color: red;
  color:white;
}
.bar{
  color:white;
}
#hi{
  font-size:3em;
  color:darkorchid;
}
</style>
<template class="q-pa-md q-gutter-md">
  <q-card-section>Message : {{msg}}</q-card-section>
  <q-card-section>using text interpolation : {{rawHtml}}</q-card-section>
  <q-card-section>Using v-html directive : <span v-html="rawHtml"></span></q-card-section>

  <q-card-section>
    <q-btn
      unelevated
      color="primary"
      type="a"
      target="_blank"
      id="linkId"
      href="link.to"
      :title="link.title"
      :label="link.label"
    >
    </q-btn>
  </q-card-section>
  <q-card-section><q-btn :disable="isButtonDisabled" label="버튼 보이기"></q-btn> </q-card-section>
  <div class = "q-pa-md row items-start">
    <q-btn @blick="increment" label="키운트" color = "primary"></q-btn>
    <q-card-section>methodCount is : {{methodCount}}</q-card-section>
  </div>
  <q-card-section>책을 가지고 있다 : {{publishedBooksMessage}}</q-card-section>
  <q-card-section class = "texth6">
    {{fullName}}
  </q-card-section>
  <q-card-section class="static" :class="{active:isActive, 'text-h3': hasError}"> change color</q-card-section>
  <q-card-section :class="classObject"> change color</q-card-section>
  <q-card-section :class="[activeClass, errorClass]"> change color</q-card-section>
  <q-card-section :class="{foo:true, bar:true}">안녕!</q-card-section>
  <q-card-section :class="{foo:true, bar:true}" :id="$attrs.id">안녕!</q-card-section>
  <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
  <q-card-section :style="styleObject"> change color</q-card-section>
  <class-child id="hi"></class-child>
  <q-card-section :style="[baseStyles, overridingStyles]"> change color</q-card-section>
  <div :style="{ display: ['flex', '-webkit-box', '-ms-flexbox'] }"></div>
</template>

<script>
import {date} from "quasar"
import ClassChild from "components/ClassChild.vue";
import{nextTick} from 'vue'
export default {
  activeColor : 'red',
  fontSize : 30,
  name: "VueEx",
  title:"Vue Basic",
  componets:{ClassChild},
  data(){
    return{
      styleObject:{
        color :'red',
        fontSize:'13px'
      },
      activeClass : 'active',
      errorClass : 'text-danger',
      isActive:true,
      error:null,
      firstName : "John",
      lastName : "Doe",
      str : '',
      methodCount : 1,
      msg:"hello Vue",
      rawHtml : '<span style="color : red">빨간색 이여야 합니다.</span>',
      linkId: "vue",
      link:{
        to:"http://vuejs.org",
        title: "뷰 공식 사이트",
        label: "Vue.js.org"
      },
      isButtonDisabled : true,
      obj:{
        nested:{count : 0},
        arr : ['foo','bar'],
      },
      author:{
        name : "John Deo",
        books : [
          'vue 2 - advanced guide',
          'vue 3 - basic guide',
          'vue 4 - the mystery'
        ]
      },
      classObject:{
        active : true,
        'text-h3' : false
      },
      baseStyles:{
        textDecorationLine:'underline',
        textDecorationThickness: '5px',
        textDecorationColor: 'red',
      },
      overridingStyles:{
        color:'blue',
        fontSize:'35px',
      },
    }
  },
  counted :{
    publishedBooksMessage(){
      return this.author.books.length > 0 ? 'yes' : 'no'
    },
    toTitleDate() {
      const timeStamp = Date.now();
      const formattedString = date.formatDate(timeStamp, "YYY-MM-DD HH:mm");
      return formattedString;
    },
  },
  methods : {
    increment() {
      this.count++;

    },
   calculateDate() {
      setInterval(()=>{
        const timeStamp = Date.now();
        const formattedString = date.formatDate(timeStamp, "YYYY-MM-DD HH:mm:ss");
        this.str = formattedString;
      },1000);
      return this.str;
    },
  },
  mounted() {
      console.log(this.methodCount);
      this.methodCount = 2;
    console.log(this.methodCount);
    this.error.type='fatal';

  },
  computed:{
    fullName :{
      get(){
        return this.firstName + ' ' + this.lastName;
      },
      set(newValue){
        [this.firstName,this.lastName] = new newValue.split(' ');
      }
    },
    classObj() {
      return{
        active:this.isActive && !this.error,
        'text-h3' : this.error && this.error.type === 'fatal'
      }
    },
  },
  watch:{

  },
}
</script>

<style scoped>

</style>
