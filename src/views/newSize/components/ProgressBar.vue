<script setup lang="ts">
import { IconServer } from "@iconify-prerendered/vue-codicon";
defineProps<{
  usedData: number;
  totalData: number;
  name: string;
}>();

function convertToKB(byte: number) {
  return typeof byte === "number" ? Math.round(byte / 1024) : 0;
}

function progressBarColorClass(ratio: number) {
  if (ratio <= 0.3) {
    return { "is-success": true };
  }
  if (ratio <= 0.7) {
    return { "is-warning": true };
  }
  return { "is-danger": true };
}
</script>

<template>
  <div class="notification is-clipped">
    <div class="columns is-vcentered has-text-centered is-mobile">
      <div class="column is-1-tablet is-2-mobile is-clipped">
        <div>
          <span class="icon is-large is-hidden-mobile">
            <IconServer class="is-size-3" />
          </span>
          <br />
          <strong style="vertical-align: super;">{{ name }}</strong>
        </div>
      </div>
      <div class="column">
        <progress
          class="progress"
          v-bind:class="progressBarColorClass(usedData / totalData)"
          v-bind:title="Math.round((usedData / totalData) * 100) + '%'"
          v-bind:value="usedData"
          v-bind:max="totalData"
        ></progress>
      </div>
      <div
        class="column is-3-mobile is-2-tablet is-2-desktop is-size-7-tablet is-size-7-mobile"
      >
        {{ convertToKB(usedData) }}KB / {{ convertToKB(totalData) }}KB
      </div>
    </div>
  </div>
</template>
