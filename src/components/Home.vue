<template>
  <div class="container">
  
    <header class="navigation">
      <button 
        class="home"
        @click="goHome"
        > 
        <img alt="Home" :src="require('@/assets/outline_home_white_24dp.png')">
      </button>  
      <h3 class="title">{{title}}</h3>
      <button 
        class="module-home"
        :class="{ goldBtn: (currentLocation.module == undefined) }"
        @click="goHome" 
        v-show="calculateCurrentModuleIndex && calculateCurrentLessonIndex && !currentLocation.module"
        >
        Modules
      </button>  

      <button 
        @click="goToModule"
        :class="{ goldBtn: (currentLocation.lesson == undefined) }"        
        v-if="dynamicModule && hierarchicalData[currentModuleIndex]"
        >{{hierarchicalData[currentModuleIndex].moduleLetter}}
      </button>

      <button 
        :class="{ goldBtn: (currentLocation.exercise == undefined) }"
        @click="goToLesson" 
        v-if="dynamicLesson && hierarchicalData[currentModuleIndex].lessons[currentLessonIndex]"
        >{{hierarchicalData[currentModuleIndex].lessons[currentLessonIndex].lessonNumber}}
      </button>

      <button  
        :class="{ goldBtn: (currentLocation.exercise !== undefined) }"
        v-if="dynamicExercise && hierarchicalData[currentModuleIndex].lessons[currentLessonIndex].lessonContent"
        >{{currentLocation.exercise}}
      </button>
   </header> 
           
    <body class="content">
      <div class="button-container">
      <div v-show="currentLocation.module == undefined">
        <button
          :class="'btn'"
          v-for="mod in hierarchicalData" 
          :key="mod" 
          v-on:click="addCurrentLocationData('module', mod.moduleName)"
          > 
          <div class="module-letter">
          {{mod.moduleLetter}}
          </div>
          <br>
          {{mod.moduleName}}
        </button>
      </div>

      <div v-if="currentModuleIndex !== undefined && currentLocation.lesson == undefined">
        <button
          :class="'btn'"
          v-for="lesName in hierarchicalData[currentModuleIndex].lessons" 
          :key="lesName" 
          v-on:click="addCurrentLocationData('lesson', lesName.lessonName)"
          >
          {{lesName.lessonNumber}}
          <br>
          {{lesName.lessonName}}
        </button>
      </div>

      <div v-if="currentModuleIndex !== undefined && currentLessonIndex !== undefined && currentLocation.exercise == undefined">
        <button
          :class="'btn'"
          v-for="content in hierarchicalData[currentModuleIndex].lessons[currentLessonIndex].lessonContent"
          :key="content"
          v-on:click="addCurrentLocationData('exercise', content)"
          > 
          {{content}}
        </button>
      </div>
      </div>
    </body>
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
    

     currentLocation: {},
     currentModuleIndex: undefined,
     currentLessonIndex: undefined,


     hierarchicalData: 
     [
       {
        moduleLetter: 'MODULE A',
        moduleName: 'FM HISTORY AND DOCTRINE',
        lessons: 
        [
          {
            lessonNumber: 'LESSON ONE',
            lessonName: 'BRIEF THE HISTORY OF FINCANCE AND COMPTROLLER CORPS',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonNumber: 'LESSON TWO',
            lessonName: 'CONDUCT FINANCIAL AND COMPTROLLER MUSEUM VISIT AND SCHOOL VISIT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON THREE',
            lessonName: 'COMMUNICATE THE IMPORTANCE OF SRC-14 ORGANIZATIONAL UNITS AND POSITIONS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON FOUR',
            lessonName: 'COMMUNICATE THE IMPORTANCE OF DOD FINANCIAL PUBLICATIONS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON FIVE',
            lessonName: 'ORIENT SOLDIER TO THE FINANCE MANAGEMENT TECHNICIAN COURSE',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleLetter: 'MODULE B',
        moduleName: 'PAY SUPPORT',
        lessons: 
        [
          {
            lessonNumber: 'LESSON ONE',
            lessonName: 'INTERPRET DODFMR VOL 7A, JTR, MPPM, AND PAY INQUIRY',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonNumber: 'LESSON TWO',
            lessonName: 'RECOGNIZE ELEMENTS OF MILITARY PAY SUPPORT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON THREE',
            lessonName: 'IDENTIFY PAY AND ALLOWANCES',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3',
              'PE 4',
              'COMPREHENSIVE PE'
            ]
          },
          {
            lessonNumber: 'LESSON FOUR',
            lessonName: 'PROGRESS TRANSACTIONS FOR RC SOLDIERS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleLetter: 'MODULE C',
        moduleName: 'BANKING AND DISPERSING',
        lessons: 
        [
          {
            lessonNumber: 'LESSON ONE',
            lessonName: 'RECOGNIZE ELEMENTS OF DISBURSING AND INTERPRET DODFMR VOL 5',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonNumber: 'LESSON TWO',
            lessonName: 'RECEIVE FUNDS AS A CASHIER',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON THREE',
            lessonName: 'IDENTIFY DISBURSEMENT VOUCHERS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON FOUR',
            lessonName: 'IDENTIFY COLLECTION VOUCHERS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON FIVE',
            lessonName: 'RECORD EXCANGE TRANSACTIONS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON SIX',
            lessonName: 'CONDUCT DISBURSING CLOSING PROCEDURES',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON SEVEN',
            lessonName: 'INPUT DISBURSING TRANSACTIONS INTO DDS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON EIGHT',
            lessonName: 'PRECESS ECOMMERCE TRANSACTIONS - LAB DDS/ECC/ PREPARE STORED VALUE CARD',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON NINE',
            lessonName: 'CONDUCT DISBURSING CLOSING PROCEDURES IN DDS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleLetter: 'MODULE D',
        moduleName: 'FUND THE FORCE',
        lessons: 
        [
          {
            lessonNumber: 'LESSON ONE',
            lessonName: 'RECOGNIZE ELEMNTS OF CVS',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonNumber: 'LESSON TWO',
            lessonName: 'COMMUNICATE TEH IMPORTANCE OF FISCAL STWARDSHIP',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON THREE',
            lessonName: 'COMPLETE ALMS GFEBS ESSENTIALS TRAINING',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON FOUR',
            lessonName: 'IDENTIFY MASTER DATA ELEMENTS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON FIVE',
            lessonName: 'MAINTAIN CVS DOCUMENTS',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON SIX',
            lessonName: 'PREPARE ACCOUNTS PAYABLE VOUCERS FOR PAYMENT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON SEVEN',
            lessonName: 'PREPARE MISCELLANEOUS VOUCHERFS FOR PAYMENT',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON EIGHT',
            lessonName: 'PERFORM BASIC GFEBS NAVIGATION',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          }
        ]
       },
       {
        moduleLetter: 'MODULE E',
        moduleName: 'PROFESSIONAL DEVELOPMENT',
        lessons: 
        [
          {
            lessonNumber: 'LESSON ONE',
            lessonName: 'COMPLETE FM CERTIFICATION DOD 101 COURSES',
            lessonContent: [
              'PE 1',
              'PE 2',
              'PE 3'
            ]
          },
          {
            lessonNumber: 'LESSON TWO',
            lessonName: 'WRITE EFFECTIVELY USING THE BASIC ARMY WRITING CORRESPONDANCE',
            lessonContent: [
              'Slides 1',
              'Slides 2',
              'PE 1'
            ]
          },
          {
            lessonNumber: 'LESSON THREE',
            lessonName: 'DEFINE THE PRINCIPLES OF MENTORSHIP',
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

   title(){
     var titleText = ''
     if (this.currentLocation.module == undefined) {
       titleText = '36B AIT'
     } else if (this.currentLocation.module && this.currentLocation.lesson == undefined) {
       titleText = this.currentLocation.module
     } else if (this.currentLocation.module && this.currentLocation.lesson && this.currentLocation.exercise == undefined) {
       titleText = this.currentLocation.lesson
     } else if (this.currentLocation.module && this.currentLocation.lesson && this.currentLocation.exercise) {
       titleText = this.currentLocation.exercise
     } else {
       titleText = 'Could Not Determine Title'
     } return titleText
   },

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
     this.currentLocation.module = undefined
     this.currentModuleIndex = undefined
     this.currentLocation.lesson = undefined
     this.currentLessonIndex = undefined
     this.currentLocation.exercise = undefined
   },
   goToModule() {
     this.currentLocation.lesson  = undefined
     this.currentLessonIndex = undefined
    this.currentLocation.exercise = undefined
   },
   goToLesson() {
    this.currentLocation.exercise  = undefined
   },
   
}
}



</script>

<style scoped>

.container {
  display: flex;
  flex-direction: column;
  background-color: #222222;
  width: 100vw;
  height: 100vh;
}

.title {
  color: #FFFFFF;
  background: none;
  border: none;
}

/* .title,
.home,
.module-home {

} */

header.navigation {
  border-bottom: .75vh solid #EBAD1B;
  width: 100vw;
  height: 15vh;
}

.content {
  display: flex;
  align-content: center;
  justify-content: center;
  margin: auto;
  height: 85vh;
  background-color: #333232;
  width: 100vw;
}

.button-container {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  margin-top: 5%;
  height: 55vh;
  background-color: #3F3F3F;
  min-width: 60vw;
  border-radius: .25em;
}

button {
  background: none;
  border: none;
  color: #FFFFFF;
}

.btn {
  display: flex;
  flex-direction: column;
  border: none;
  border-radius: 1.25em;
  background-color: #222222;
  color: #FFFFFF;
  margin: auto; 
  margin-top: 1.25%;
  padding: 1.75%;
  width: 68%;
}

.goldBtn {
  color: #EBAD1B;
  background: none;
  border: none;
}

.module-home {
  color: #FFFFFF;
}

.btn:hover {
  color: #FFFFFF;
  background-color: #EBAD1B;
}

/* inlineblock, displayinline, inlineflex */
</style>
