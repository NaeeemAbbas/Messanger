<script setup lang="ts">
import type { ICall, IContact } from "@src/types";

import { getCallName } from "@src/utils";

import { PhoneIcon, XMarkIcon } from "@heroicons/vue/24/solid";
import CallAvatar from "@src/components/shared/blocks/CallAvatar.vue";
import IconButton from "@src/components/ui/inputs/IconButton.vue";

const props = defineProps<{
  members: IContact[];
  activeCall: ICall;
  closeModal: () => void;
  handleCallStatusChange: (status: string) => void;
}>();
</script>

<template>
  <div class="w-full h-full py-6 flex flex-col items-center">
    <!--call info-->
    <div class="mb-7">
      <div class="relative mb-5">
        <CallAvatar
          v-for="(member, index) in members"
          :member="member"
          :index="index"
          :members-length="members.length"
          :large="true"
        />
      </div>

      <p class="heading-2 text-black/70 dark:text-white/70 mb-4" tabindex="0">
        {{ getCallName(activeCall) }}
      </p>

      <p class="body-3 outline-none text-green-300" tabindex="0">
        {{ activeCall.direction }}
      </p>
    </div>

    <!--answer button-->
    <div class="flex">
      <IconButton
        @click="handleCallStatusChange('ongoing')"
        class="ic-btn-contained-success relative p-4.25 mr-8"
      >
        <PhoneIcon class="w-5 h-5" />
        <span
          class="animate-ping absolute inline-flex w-8.75 h-8.75 rounded-full bg-green-400 opacity-75"
        ></span>
      </IconButton>

      <!--reject button-->
      <IconButton
        @click="
          () => {
            props.closeModal();
          }
        "
        class="ic-btn-contained-danger relative p-4.25"
      >
        <XMarkIcon class="w-5 h-5" />
        <span
          class="animate-ping absolute inline-flex w-8.75 h-8.75 rounded-full bg-red-400 opacity-75"
        ></span>
      </IconButton>
    </div>
  </div>
</template>
