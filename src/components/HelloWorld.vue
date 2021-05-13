<template>
  <div class="hello">
  
    <button @click="goHome" v-show="calculateCurrentModuleIndex && calculateCurrentLessonIndex">HOME:</button>  
    <button @click="goToModule" class = 'module' v-show="dynamicModule">{{currentLocation.module}}</button>
    <button @click="goToLesson" class = 'lesson' v-show="dynamicLesson">{{currentLocation.lesson}}</button>
    <button  class = 'exercise' v-show="dynamicExercise">{{currentLocation.exercise}}</button>
    
           
  <h2>BODY:</h2>
    <button 
      v-for="mod in hierarchicalData" 
      :key="mod" 
      v-on:click="addCurrentLocationData('module', mod.moduleName)"
      >
      {{mod.moduleName}}
    </button>

    <div v-if="currentModuleIndex !== undefined">
      <button 
        v-for="lesName in hierarchicalData[currentModuleIndex].lessons" 
        :key="lesName" 
        v-on:click="addCurrentLocationData('lesson', lesName.lessonName)"
        >
        {{lesName.lessonName}}
      </button>
    </div>

    <div v-if="currentModuleIndex !== undefined && currentLessonIndex !== undefined">
      <button
        v-for="content in hierarchicalData[currentModuleIndex].lessons[currentLessonIndex].lessonContent"
        :key="content"
        v-on:click="addCurrentLocationData('exercise', content)"
        > 
        {{content}}
      </button>
    </div>
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
     if(this.currentLocation.exercise) {
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
    if (this.currentModuleIndex !== undefined) {
        this.hierarchicalData[this.currentModuleIndex].lessons.forEach((lessonObject, index) => {
        if (lessonObject.lessonName == this.currentLesson){
          this.currentLessonIndex = index
        }
        }
        )
        }
        return true
    }
 },
 methods: {
   addCurrentLocationData(newLocationHierarchy, newLocationValue) {
      this.currentLocation[newLocationHierarchy] = newLocationValue  
   },
   goHome() {
    //  delete this.currentLocation.module;
    //  delete this.currentLocation.lesson;
    //  delete this.currentLocation.exercise;
     this.currentLocation.module = undefined
     this.currentModuleIndex = undefined
     this.currentLocation.lesson = undefined
     this.currentLessonIndex = undefined
     this.currentLocation.exercise = undefined
   },
   goToModule() {
    //  delete this.currentLocation.lesson;
    //  delete this.currentLocation.exercise;
     this.currentLocation.lesson  = undefined
     this.currentLessonIndex = undefined
      this.currentLocation.exercise = undefined
   },
   goToLesson() {
    //  delete this.currentLocation.exercise;
      this.currentLocation.exercise  = undefined
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
