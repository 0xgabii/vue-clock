<template>
  <div class="wrapper">
    <div class="date">
      <span class="year">{{year}}</span>
      <span class="month">{{month}}</span>
      <span class="day">{{day}}</span>
    </div>
    <div class="time">
      <span class="isAfternoon">{{isAfternoon}}</span>
      <span class="hour">{{hour}}</span>
      <transition name="slideDown">
        <span
          class="slideDown"
          :key="minute.first">{{minute.first}}</span>
      </transition>
      <transition name="slideDown">
        <span
          class="slideDown"
          :key="minute.last">{{minute.last}}</span>
      </transition>
      {{minute.text}}
      <transition name="slideDown">
        <span
          class="slideDown" 
          :key="second.first">{{second.first}}</span>
      </transition>
      <transition name="slideDown">
        <span
          class="slideDown" 
          :key="second.last">{{second.last}}</span>
      </transition>
      {{second.text}}
    </div>  
  </div>
</template>

<script>
const splitNums = number => {
  const arr = String(number).split('');
  if(arr.length <= 1) arr.unshift('0');
  return arr;
};

export default {
  name: 'datetime',
  data() {
    return {
      now: new Date()
    }
  },
  created() {
    setInterval(() => {
      this.now = new Date();
    }, 1000)
  },
  computed: {
    year() {
      return (this.now.getYear() + 1900) + '년'
    },
    month() {
      return (this.now.getMonth() + 1) + '월'
    },
    day() {
      return this.now.getDate() + '일';
    },
    hour() {
      const hour = this.now.getHours();
      return hour > 12 ? (hour - 12) + '시' : hour + '시';
    },
    minute() {
      return {
        first: splitNums(this.now.getMinutes())[0],
        last: splitNums(this.now.getMinutes())[1],
        text: '분'
      }
    },
    second() {
      return {
        first: splitNums(this.now.getSeconds())[0],
        last: splitNums(this.now.getSeconds())[1],
        text: '초'
      }
    },  
    isAfternoon() {
      return this.now.getHours() > 12 ? '오후' : '오전'
    },
  }
}
</script>

<style scoped>
/* transition-group CSS */
.slideDown-enter {
  opacity: 0;
  transform: translateY(-2rem);
}
.slideDown-leave-to{
  opacity: 0;
  transform: translateY(2rem);
}
.slideDown-leave-active {
  position: absolute;
}
/* template CSS */
.wrapper{
  position: absolute;
  left: 50%;
  top: 50%;
  width: 41rem;
  text-shadow: 3px 3px #282828;
  transform: translate(-50%,-50%);
}
span{
  display: inline-block;
  transition: all 0.5s cubic-bezier(0.18, 0.89, 0.32, 1.28);
}
.date{
  font-size: 2.5rem;
}
.time{
  font-size: 5rem;
}
.slideDown {
  margin: 0 -0.6rem;
}
</style>