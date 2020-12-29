<template>
     <div class="app">   
          <div > 开始时间:
          <date-picker type="datetime" v-model="startTime" placeholder="请选择开始时间" :options="startTimeOption" @on-change="onStartTimeChange"></date-picker>
          </div>
          <div > 结束时间:
          <date-picker type="datetime" v-model="endTime" placeholder="请选择结束时间" :options="endTimeOption" @on-change="onEndTimeChange"></date-picker>
          </div>
          <div>我是about</div>
     </div>          
</template>

<script>
export default {
  name: 'about',
  data() {
        return {
            startTime: '',
            endTime: '',
            startTimeOption: {},
            endTimeOption: {}
        }

},
 mounted() {
          this.startTime = new Date()
          this.endTime = new Date((this.startTime/1000+(86400*4))*1000) 
          this.onStartTimeChange(this.startTime)
          // this.onEndTimeChange(this.endTime)
      },
      methods: {
          /**
           * 开始时间发生变化时触发,设置结束时间不可选择的日期
           * 结束时间应大于等于开始时间,且小于等于当前时间
           * @param {string} startTime 格式化后的日期
           * @param {string} type 当前的日期类型
           */
          onStartTimeChange(startTime, type) {
              this.endTimeOption = {
                  disabledDate(endTime) {
                      return  !((+new Date(endTime) >= +new Date(startTime)) && ((+new Date(endTime) - (+new Date(startTime))) <= 345600000))  
                  }
              }
              this.startTime = startTime
          },
          /**
           * 结束时间发生变化时触发,设置开始时间不可选择的日期
           * 开始时间小于等于结束时间,且小于等于当前时间
           * @param {string} date 格式化后的日期
           * @param {string} type 当前的日期类型
           */
          onEndTimeChange(endTime, type) {
            //   this.startTimeOption = {
            //       disabledDate(startTime) {
            //         // console.log(startTime)
            //           return  startTime < new Date(endTime) || startTime < Date.now()
            //       }
            //   }
            this.onStartTimeChange(this.startTime)
              this.endTime = endTime
          } 
      }
      }    
</script>

<style>

</style>
