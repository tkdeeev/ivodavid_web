<script setup>
import { ref } from "vue";
function formatDuration(duration) {
  let seconds = parseInt((duration / 1000) % 60);
  let minutes = parseInt((duration / (1000 * 60)) % 60);
  let hours = parseInt((duration / (1000 * 60 * 60)) % 24);
  let days = parseInt(duration / (1000 * 60 * 60 * 24));

  hours = hours < 10 ? "0" + hours : hours;
  minutes = minutes < 10 ? "0" + minutes : minutes;
  seconds = seconds < 10 ? "0" + seconds : seconds;

  return {
    days,
    hours,
    minutes,
    seconds,
  };
}

let days = ref("")
let hours = ref("")
let minutes = ref("")
let seconds = ref("")

var week = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'];
const cd = new Date();
const fd = new Date("2023-11-11T12:00:00");
var timerID = setInterval(updateTime, 1000);
updateTime();
function updateTime() {
    var cd = new Date();
    var diff = formatDuration(Math.abs(fd - cd));
    days.value = diff.days;
    hours.value = diff.hours;
    minutes.value = diff.minutes;
    seconds.value = diff.seconds;
};

function zeroPadding(num, digit) {
    var zero = '';
    for(var i = 0; i < digit; i++) {
        zero += '0';
    }
    return (zero + num).slice(-digit);
}
</script>

<template>
  <video id="background-video" autoplay loop muted>
    <source src="/btr.mp4" type="video/mp4">
  </video>

  <div class="overlay"></div>

  <div id="clock">
    <p class="date"> COMMING SOON </p>
    <p class="time"><span class="days">{{ days }}</span><span class="dot">:</span><span class="hours">{{ hours }}</span><span class="dot">:</span><span class="minutes">{{ minutes }}</span><span class="dot">:</span><span class="seconds">{{ seconds }}</span></p>
    <button class='glowing-btn'><span class='glowing-txt'>BE <span class='faulty-letter'>PART </span>OF US</span></button>
  </div>
  
  <footer>
    <ul>
      <li>
        <a href="" class="flink">Instagram</a>
      </li>
      <li>
        <a href="" class="flink">Telegram</a>
      </li>
      <li>
        <a href="" class="flink">Discord</a>
      </li>
      <li>
        <a href="" class="flink">Facebook</a>
      </li>
      <li>
        <a href="" class="flink">Tiktok</a>
      </li>
    </ul>
    
  </footer>
</template>

<style scoped lang="scss">
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.8);
  z-index: 0;
}
#background-video {
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 0;
}

footer {
  position: absolute;
  bottom: 10px;
  left: 0;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  ul {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 66vw;
    list-style: none;
    li {
      a.flink {
        color: #fff;
        text-decoration: none;
        font-size: 1.5rem;
        font-weight: 500;
        transition: all 0.3s ease;
        font-family: 'Share Tech Mono', monospace;
        color: #ffffff;
        text-align: center;
        color: #daf6ff;
        text-shadow: 0 0 20px rgba(10, 175, 230, 1),  0 0 20px rgba(10, 175, 230, 0);
        &:hover {
          color: #0a2e38;
        }
        &:visited {
          color: #fff;
        }
      }
    }
  }
}

@import url("https://fonts.googleapis.com/css?family=Raleway");

:root {
  --glow-color: hsl(186 100% 69%);
}
html,body {
    height: 100%;
}
body {
    background: #0f3854;
    background: radial-gradient(ellipse at center,  #0a2e38  0%, #000000 70%);
    background-size: 100%;
}
p {
    margin: 0;
    padding: 0;
}
#clock {
    font-family: 'Share Tech Mono', monospace;
    color: #ffffff;
    text-align: center;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    color: #daf6ff;
    text-shadow: 0 0 20px rgba(10, 175, 230, 1),  0 0 20px rgba(10, 175, 230, 0);
    .time {
        letter-spacing: 0.05em;
        font-size: 6vw;
        padding: 5px 0;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        
        * {
          display: inline-block;
          position: relative;
          padding: 0 5px;
        }
        /*days, minutes, seconds subtext */
        *::after {
            position: absolute;
            padding: 0 5px;
            font-size: 20px;
            width: 100%;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
        }
        .days {
            &::after {
                content: "Days";
            }
        }
        .hours {
            &::after {
                content: "Hours";
            }
        }
        .minutes {
            &::after {
                content: "Minutes";
            }
        }
        .seconds {
            &::after {
                content: "Seconds";
            }
        }

    }
    .date {
        letter-spacing: 0.1em;
        font-size: 24px;
    }
    .text {
        letter-spacing: 0.1em;
        font-size: 12px;
        padding: 20px 0 0;
    }

}

@media screen and (max-width: 768px) {
    #clock {
        .time {
            font-size: 10vw;
            flex-direction: column;
            align-items: flex-end;
            transform: translateX(-50%);
            .dot {
                display: none;
            }
            *::after {
              
              width: 100%;
              bottom: 0px;
              right: -100%;
              transform: translate(0%, -50%);
              left: auto;
            }

        }
        .date {
            font-size: 24px;
        }
        .text {
            font-size: 8px;
        }
    }
    footer ul {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
      width: 100%;
      li {
        margin: 10px 0;
        &:nth-child(1) {
          grid-column: 1 / 3;
        }
        &:nth-child(2) {
          grid-column: 3 / 5;
        }
        &:nth-child(3) {
          grid-column: 5 / 7;
        }
        &:nth-child(4) {
          grid-column: 1 / 4;
        }
        &:nth-child(5) {
          grid-column: 4 / 7;
        }
        a.flink {
          font-size: 1.2rem;
        }
      }

    }
    
  
}



</style>
