<template>
  <div>
    <q-toolbar>
      <q-btn stretch flat label="Prev" @click="calendarPrev" />
      <q-separator vertical />
      <q-btn stretch flat label="Next" @click="calendarNext" />
      <q-space />
    </q-toolbar>
    <q-separator />
    <div style="overflow: hidden;">
      <q-calendar
        ref="calendar"
        v-model="selectedDate"
        view="month"
        locale="en-us"
        mini-mode="auto"
        breakpoint="sm"
        animated
        transition-prev="slide-right"
        transition-next="slide-left"
        :selected-dates="selectedDates"
        @click:day="onToggleDate"
        @click:date="onToggleDate"
      />
    </div>
  </div>
</template>

<script>
function leftClick (e) {
  return e.button === 0
}

export default {
  data () {
    return {
      selectedDate: '',
      selectedDates: []
    }
  },

  methods: {
    calendarNext () {
      this.$refs.calendar.next()
    },

    calendarPrev () {
      this.$refs.calendar.prev()
    },

    classDay (timestamp) {
      if (this.anchorDayIdentifier !== false && this.otherDayIdentifier !== false) {
        return this.getBetween(timestamp)
      }
    },

    onToggleDate ({ scope, event }) {
      if (leftClick(event)) {
        if (this.selectedDates.includes(scope.date)) {
          // remove the date
          for (let i = 0; i < this.selectedDates.length; ++i) {
            if (scope.date === this.selectedDates[i]) {
              this.selectedDates.splice(i, 1)
              break
            }
          }
        } else {
          // add the date
          this.selectedDates.push(scope.date)
        }
      }
    }
  }
}
</script>
