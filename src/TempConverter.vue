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
  <div>
    <label for="fahrenheit">Fahrenheit</label>
    <input @input="(event) => send({ type: 'changeF', value: (event!.target as HTMLInputElement)!.value })" type="text"
      :value="snapshot.context.fahrenheit" id="fahrenheit" size="10" />
    <label for="celsius">Celsius</label>
    <input @input="(event) => send({ type: 'changeC', value: (event!.target as HTMLInputElement)!.value })"
      :value="snapshot.context.celsius" type="text" id="celsius" size="10" />
  </div>
</template>

<style scoped>
.step {
  padding: 2rem;
  background: white;
  border-radius: 1rem;
  box-shadow: 0 0.5rem 1rem #0001;
  width: 75vw;
  max-width: 40rem;
}

.feedback>.close-button {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 1;
}

.button {
  appearance: none;
  color: white;
  border: none;
  padding: 1rem 1.5rem;
  border-radius: 0.25rem;
  font-size: inherit;
  font-weight: bold;
  margin-right: 1rem;
  background-color: var(--color-primary);
}

.button:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

.close-button {
  appearance: none;
  background: transparent;
  border: none;
  padding: 1rem;
}
</style>
