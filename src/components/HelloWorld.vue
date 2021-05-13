<template>
  <div class="hello">
<h1 v-show="calculateCurrentModuleIndex">HEADER:</h1>  
    <div class = 'module' v-show="dynamicModule">{{currentModule}}</div>
    <div class = 'lesson' v-show="dynamicLesson">{{currentLocation.lesson}}</div>
    <div class = 'exercise' v-show="dynamicExercise">{{currentLocation.content}}</div>
    
            <!-- <div v-show="currentModule == 'Module A'">
                    <button class= "moduleAButton" >Lesson 1</button>
                    <button class= "moduleAButton">Lesson 2</button>
                    <button class= "moduleAButton">Lesson 3</button>
            </div> -->
<h2>BODY:</h2>
    <!-- for each module object in hierarchicalData, we make a button, which when clicked, sets the currentLocation to where we're going -->

    <!--
      create a button with a v-for loop that 
      -->
    <button v-for="mod in hierarchicalData" :key="mod" v-on:click="addCurrentLocationData('module', mod.moduleName)">{{mod.moduleName}}</button>


    <!-- for each lesson object in hierarchicalData -> module A, we make a button, which when clicked, sets the currentLocation to where we're going -->
<div v-if="hierarchicalData[currentModuleIndex]" >
    <button v-for="lessonContent in hierarchicalData[currentModuleIndex].lessons" :key="lessonContent" v-on:click="addCurrentLocationData('lesson', lessonContent.lessonName)">{{lessonContent.lessonName}}</button>
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
    //  modulesArray: ['Module A','Module B','Module C','Module D','Module E'],
    //  lessonArray: ['Lesson 1', 'Lesson 2', 'Lesson 3'],
    

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
    //  moduleA: {lesson1: "Lesson 1", lesson2: "Lesson 2", lesson3: "Lesson 3"}
   }
 },

 computed: {

   currentModule(){
     return this.currentLocation.module
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
