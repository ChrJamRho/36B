<template>
  <div class="hello">
  
  <h1 v-show="calculateCurrentModuleIndex">HEADER:</h1>  
    <div class = 'module' v-show="dynamicModule">{{currentModule}}</div>
    <div class = 'lesson' v-show="dynamicLesson">{{currentLocation.lesson}}</div>
    <div class = 'exercise' v-show="dynamicExercise">{{currentLocation.content}}</div>
    
           
  <h2>BODY:</h2>
    <button 
      v-for="mod in hierarchicalData" 
      :key="mod" 
      v-on:click="addCurrentLocationData('module', mod.moduleName)"
      >
      {{mod.moduleName}}
    </button>

    <div v-if="hierarchicalData[currentModuleIndex]">
      <button 
        v-for="lessonContent in hierarchicalData[currentModuleIndex].lessons" 
        :key="lessonContent" 
        v-on:click="addCurrentLocationData('lesson', lessonContent.lessonName)"
        >
        {{lessonContent.lessonName}}
      </button>
    </div>

    <!-- <div v-if="hierarchicalData[currentLessonIndex]">
      <button
      v-for
      ></button>
    </div> -->

  </div>
</template>

<script>




export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
 data() {
   return {
     currentLocation: {},
     currentModuleIndex: undefined,
     currentLessonIndex: undefined,

     hierarchicalData: 
     [
       {
        moduleName: 'Module A',
        lessons: 
        [
          {
            lessonName: 'lesson1',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonName: 'lesson2',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'lesson3',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
        ]
       },
       {
        moduleName: 'Module B',
        lessons: 
        [
          {
            lessonName: 'lesson3',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonName: 'lesson4',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
        ]
       },
      ], 
     userNumber: undefined,
   }
 },

 computed: {

   currentModule(){
     return this.currentLocation.module
   },
   currentLesson(){
     return this.currentLocation.lesson
   },
   dynamicModule() {
     if(this.currentLocation.module){
     return true
     }
     else{
       return false
     }
   },
   dynamicLesson() {
     if(this.currentLocation.lesson){
     return true
     }
     else{
       return false
     }
   },
   dynamicExercise() {
     if(this.currentLocation.content) {
     return true
     }
     else{
       return false
     }
   },
    calculateCurrentModuleIndex() { 
      this.hierarchicalData.forEach((moduleObject, index) => {
        if (moduleObject.moduleName == this.currentModule){
          this.currentModuleIndex = index 
        } 
        }
        )
        return true
    },
    calculateCurrentLessonIndex() {
      this.hierarchicalData.forEach((lessonObject, index) => {
        if (lessonObject.lessonName == this.currentLesson){
          this.currentLessonIndex = index
        }
        }
        )
        return true
    }
 },
 methods: {

   addCurrentLocationData(newLocationHierarchy, newLocationValue) {
      this.currentLocation[newLocationHierarchy] = newLocationValue
      
   }
}
}



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
