<script setup lang="ts">
import { useMachine } from '@xstate/vue';
import { tempMachine } from './tempMachine';
import { createBrowserInspector } from '@statelyai/inspect';

const { inspect } = createBrowserInspector({
  // Comment out the line below to start the inspector
  autoStart: false,
});

const { snapshot, send } = useMachine(tempMachine, {
  inspect,
});
</script>

<template>
  <div class="temp-module">
    <input placeholder="----"
      @input="(event) => send({ type: 'changeF', value: (event!.target as HTMLInputElement)!.value })" type="text"
      :value="snapshot.context.fahrenheit" id="fahrenheit" size="10" />
    <label for="fahrenheit">Fahrenheit</label>
  </div>
  <div class="temp-module">
    <input placeholder="----"
      @input="(event) => send({ type: 'changeC', value: (event!.target as HTMLInputElement)!.value })"
      :value="snapshot.context.celsius" type="text" id="celsius" size="10" />
    <label for="celsius">Celsius</label>
  </div>
</template>
