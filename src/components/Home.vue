<template>
  <div class="hello">
  
    <button 
      :style="style"
      @click="goHome" 
      v-show="calculateCurrentModuleIndex && calculateCurrentLessonIndex"
      >HOME:
    </button>  

    <button 
      :style="style"
      @click="goToModule" 
      class = 'module' 
      v-show="dynamicModule"
      >{{currentLocation.module}}
    </button>

    <button 
      :style="style"
      @click="goToLesson" 
      class = 'lesson' 
      v-show="dynamicLesson"
      >{{currentLocation.lesson}}
    </button>

    <button  
      :style="style"
      class = 'exercise' 
      v-show="dynamicExercise"
      >{{currentLocation.exercise}}
    </button>
    
           
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
  name: 'Home',
  props: {
    msg: String
  },
 data() {
   return {
     style: {
       color: 'white',
       backgroundColor: 'black'
     },

     currentLocation: {},
     currentModuleIndex: undefined,
     currentLessonIndex: undefined,


     hierarchicalData: 
     [
       {
        moduleName: 'MODULE A: FM HISTORY AND DOCTRINE',
        lessons: 
        [
          {
            lessonName: 'LESSON ONE: BRIEF THE HISTORY OF FINCANCE AND COMPTROLLER CORPS',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonName: 'LESSON TWO: CONDUCT FINANCIAL AND COMPTROLLER MUSEUM VISIT AND SCHOOL VISIT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON THREE: COMMUNICATE THE IMPORTANCE OF SRC-14 ORGANIZATIONAL UNITS AND POSITIONS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON FOUR: COMMUNICATE THE IMPORTANCE OF DOD FINANCIAL PUBLICATIONS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON FIVE: ORIENT SOLDIER TO THE FINANCE MANAGEMENT TECHNICIAN COURSE',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleName: 'MODULE B: PAY SUPPORT',
        lessons: 
        [
          {
            lessonName: 'LESSON ONE: INTERPRET DODFMR VOL 7A, JTR, MPPM, AND PAY INQUIRY',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonName: 'LESSON TWO: RECOGNIZE ELEMENTS OF MILITARY PAY SUPPORT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON THREE: IDENTIFY PAY AND ALLOWANCES',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3',
              'PE 4',
              'COMPREHENSIVE PE'
            ]
          },
          {
            lessonName: 'LESSON FOUR: PROGRESS TRANSACTIONS FOR RC SOLDIERS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleName: 'MODULE C: BANKING AND DISPERSING',
        lessons: 
        [
          {
            lessonName: 'LESSON ONE: RECOGNIZE ELEMENTS OF DISBURSING AND INTERPRET DODFMR VOL 5',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonName: 'LESSON TWO: RECEIVE FUNDS AS A CASHIER',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON THREE: IDENTIFY DISBURSEMENT VOUCHERS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON FOUR: IDENTIFY COLLECTION VOUCHERS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON FIVE: RECORD EXCANGE TRANSACTIONS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON SIX: CONDUCT DISBURSING CLOSING PROCEDURES',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON SEVEN: INPUT DISBURSING TRANSACTIONS INTO DDS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON EIGHT: PRECESS ECOMMERCE TRANSACTIONS - LAB DDS/ECC/ PREPARE STORED VALUE CARD',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON NINE: CONDUCT DISBURSING CLOSING PROCEDURES IN DDS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleName: 'MODULE D: FUND THE FORCE',
        lessons: 
        [
          {
            lessonName: 'LESSON ONE: RECOGNIZE ELEMNTS OF CVS',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonName: 'LESSON TWO: COMMUNICATE TEH IMPORTANCE OF FISCAL STWARDSHIP',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON THREE: COMPLETE ALMS GFEBS ESSENTIALS TRAINING',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON FOUR: IDENTIFY MASTER DATA ELEMENTS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON FIVE: MAINAIN CVS DOCUMENTS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON SIX: PREPARE ACCOUNTS PAYABLE VOUCERS FOR PAYMENT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON SEVEN: PREPARE MISCELLANEOUS VOUCHERFS FOR PAYMENT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON EIGHT: PERFORM BASIC GFEBS NAVIGATION',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleName: 'Module E: PROFESSIONAL DEVELOPMENT',
        lessons: 
        [
          {
            lessonName: 'LESSON ONE: COMPLETE FM CERTIFICATION DOD 101 COURSES',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonName: 'LESSON TWO: WRITE EFFECTIVELY USING THE BASIC ARMY WRITING CORRESPONDANCE',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonName: 'LESSON THREE: DEFINE THE PRINCIPLES OF MENTORSHIP',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
        ]
       }
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
