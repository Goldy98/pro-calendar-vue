<template>
  <div
    class="select-none flex space-x-2 flex-row flex-nowrap items-center min-w-10dt125rem"
  >
    <!--left button icon master-->
    <a
      class="bg-F4F4F5 w-7 h-7 rounded-tl-md rounded-bl-md inline-flex flex-shrink-0 items-center justify-center hover:opacity-80 active:animate-pulse cursor-pointer calendar--arrows-left"
      href="#"
      @click.prevent="$emit('calendar-arrow:left')"
      :title="$t('calendar.previous_day')"
    >
      <template v-if="slots.leftSwitchArrow">
        <component :is="slots.leftSwitchArrow" />
      </template>
      <template v-else>
        <Left />
      </template>
    </a>
    <!-- <span
      v-if="!configs?.nativeDatepicker"
      class="capitalize bg-F4F4F5 text-18181B text-center py-0dt375 px-4 flex-shrink-0 font-medium text-xs mx-px"
    >
      {{ label }}
    </span> -->
    <!--right button icon master-->
    <a
      class="bg-F4F4F5 rounded-tr-md rounded-br-md w-7 h-7 inline-flex flex-shrink-0 items-center justify-center hover:opacity-80 active:animate-pulse cursor-pointer calendar--arrows-right"
      href="#"
      @click.prevent="$emit('calendar-arrow:right')"
      :title="$t('calendar.next_day')"
    >
      <template v-if="slots.rightSwitchArrow">
        <component :is="slots.rightSwitchArrow" />
      </template>
      <template v-else>
        <Right />
      </template>
    </a>
  </div>
</template>

<script setup lang="ts">
export interface Props {
  label?: string;
  slots: Slots;
}

import type { Configs } from "@/stores/events";
import { computed, type Slots } from "vue";
import { useEventsStore } from "../../stores/events";

import Left from "./assets/button-master-left.vue";
import Right from "./assets/button-master-right.vue";

const store = useEventsStore();

const props = withDefaults(defineProps<Props>(), {
  label: "dd/mm/yyyy",
});

const configs = computed<Configs>(() => store.getConfigs);

const emit = defineEmits(["calendar-arrow:left", "calendar-arrow:right"]);
</script>
