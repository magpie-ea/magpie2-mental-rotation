<template>
  <Experiment :title="'Mental rotation experiment'">
    <template #screens>
      <InstructionScreen>
        <p>Thank you for participating in our experiment!</p>
        <p>
          You will need around 10 min to complete the experiment. Please make
          sure that you will not be distracted. Switch off all messaging
          systems, your phone, any background music etc., and try to concentrate
          as much as possible on the task at hand.
        </p>
        <p>Click on the button below to receive instructions.</p>
      </InstructionScreen>

      <InstructionScreen :title="'Instructions'">
        <p>
          You will see pictures showing pairs of geometrical objects. Your task
          is to compare both objects in the pair and decide whether they are the
          same or different. You will need press button "F" if you think the
          objects are the same, and "J" if you think they are different. Please
          try to answer as quick and accurately as possible!
        </p>
        <p>We will practice this first.</p>
      </InstructionScreen>

      <template v-for="(task, i) in trials">
        <KeypressScreen
          :key="i"
          :progress="i / trials.length"
          :fixation-time="2000"
          :keys="{ f: 'different', j: 'same' }"
        >
          <template #stimulus>
            <img :src="task.picture" />
            <Record :data="task" />
          </template>
        </KeypressScreen>
      </template>

      <DebugResultsScreen />
    </template>
  </Experiment>
</template>

<script>
import { practice_trials } from './trials.js';
export default {
  name: 'App',
  data() {
    return {
      trials: practice_trials
    };
  }
};
</script>

<style>
.stimulus {
  width: 20%;
  border: 2px solid blue;
}
</style>
