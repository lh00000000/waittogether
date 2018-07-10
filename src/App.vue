
<template>
  <div id="app">
    <p class="title" v-html="titleText"></p>
    <Person
      v-for="(person, idx) in people"
      v-bind:key="idx"
      v-bind:idx="idx"
      v-bind:renaming="person.renaming"
      v-bind:name="person.name"
      v-bind:status="person.status"
    ></Person>
    <div v-if="shouldShowAddButton">
      <button @click="addNewPerson" >➕</button>
    </div>
    <WaitButton v-if="canStartWaiting" />
    <CountDown class="countDownMargin" v-if="timerOn"/>
  </div>
</template>

<script>

import HelloWorld from './components/HelloWorld.vue'
import Person from './components/Person.vue'
import CountDown from './components/CountDown.vue'
import WaitButton from './components/WaitButton.vue'
import { mapActions, mapState, mapGetters } from 'vuex'
import enums from './enums'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Person,
    WaitButton,
    CountDown
  },
  computed: {
    ...mapState(["people", "timerOn"]),
    ...mapGetters(["shouldShowAddButton", "canStartWaiting", "titleText"])
  },
  methods: {
    ...mapActions({
      addNewPerson: enums.actions.ADD_PERSON,
      startWaiting: enums.actions.START_WAITING
    })
  }
}
</script>

<style >

* {
  font-family: 'Montserrat', sans-serif;
  font-size: 36px;
}

.title {
  font-size: 45px;
  margin-top: 36px;
  margin-bottom: 48px;
}
#app {
  margin-left: 10%;
  width: 32ch;
}

body {
  background-color: #dedede;
}

button {
  background-color: Transparent;
  background-repeat:no-repeat;
  border: none;
  cursor:pointer;
  overflow: hidden;
  outline:none;
  padding: 0;
}

.countDownMargin {
  margin-top: 48px;
}


.statusComing {
  color: rgb(233, 92, 92);
}
.statusNotComing {
  color: gray;
}
.statusHere {
  color: green;
}
.statusWaiting {
  color: rgb(246,252,73);
}

.statusReady {
  color: steelblue;
}

</style>
