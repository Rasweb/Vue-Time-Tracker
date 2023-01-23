<script lang="ts">
export default {
  name: "TrackerComp",
  data() {
    return {
      elapsedTime: 0,
      timer: 0,
    };
  },
  computed: {
    // Format the elapsed time \\
    formattedElapsedTime() {
      // Create a new time, value is 0 \\
      const date = new Date(0);
      // Sets the seconds \\
      date.setSeconds(this.elapsedTime / 1000);
      // Sets the date to a string in the UTC time zone \\
      const utc = date.toUTCString();
      // Returns the time and formats it to = 00:00:00 \\
      return utc.substring(utc.indexOf(":") - 2).replace("GMT", "");
    },
  },
  methods: {
    // Starts the tracker \\
    start() {
      // Uses the setInterval to start the tracker at the last zero. \\
      // eg = 00:00:01 \\
      this.timer = setInterval(() => {
        this.elapsedTime += 1000;
      }, 1000);
    },
    // Stops the tracker \\
    stop() {
      // Clears the interval so it stops \\
      // elapsedTime value also stops \\
      clearInterval(this.timer);
    },
    // Resets the tracker \\
    reset() {
      // Converts the elapsedTime value to 0 \\
      this.elapsedTime = 0;
    },
  },
};
</script>
<template>
  <div>
    <h1>The Tracker</h1>
    <button @click="start">Start</button>
    <button @click="reset">Reset</button>
    <button @click="stop">Stop</button>
    <p>{{ formattedElapsedTime }}</p>
  </div>
</template>
<style></style>
