<template>
  <div id="app">
    <Navbar @change-tab="currentTab = $event" />
    <div class="container mt-4">
      <GradeCalculator v-if="currentTab === 'calculator'" />
      <RegistrationForm v-if="currentTab === 'registration'" />
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import GradeCalculator from "./components/GradeCalculator.vue";
import RegistrationForm from "./components/RegistrationForm.vue";

export default {
  components: { Navbar, GradeCalculator, RegistrationForm },
  data() {
    return { currentTab: "calculator" };
  },
};
</script>
