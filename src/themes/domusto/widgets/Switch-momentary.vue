<template>
  <div class="widget widget--switch" v-on:click="trigger">
    <!-- <audio ref="audio" :src="audio"></audio> -->
    <div class="widget__status-indicator switch--moment-off"></div>
    <div class="widget__status-indicator switch--moment-on widget__status-indicator--green"></div>
    <div class="widget__timer-indicator" v-bind:class="{ 'widget__timer-indicator--enabled': output.hasTimers }"></div>
    <div class="widget__title">{{ output.name }}</div>
  
  </div>
</template>

<script>
import axios from 'axios';
import { round } from '@/app/filters.js'

let CONFIG = require('@/config.js');

export default {
  props: ['output'],
  data: function () {
    return {

    };
  },
  computed: {
    audio() {
      var audio = new Audio();
      audio.src = require('../assets/sounds/220176_4100837-hq.mp3');
      audio.preload = 'auto';     
      return audio;
    }
  },
  methods: {
    round,
    trigger: function () {

      if (CONFIG.buttonSound) {
        this.audio.currentTime = 0.01;
        this.audio.play();
      }
      
      console.log('trigger', this.output, this.output.actions);

      if (this.output.actions) {

        axios.get(this.output.actions.trigger).then(() => {
          // this.output.state = response.data.state;
        });

      } else {
        console.error('no action defined for for command: trigger');
      }

    }
  },
};
</script>

<style>

</style>