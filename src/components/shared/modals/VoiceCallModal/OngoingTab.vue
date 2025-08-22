<script setup lang="ts">
import type { ICall, IContact } from "@src/types";

import { getCallName } from "@src/utils";

import {
  ChatBubbleBottomCenterTextIcon,
  PhoneIcon,
  SpeakerXMarkIcon,
  UserPlusIcon,
} from "@heroicons/vue/24/solid";
import CallAvatar from "@src/components/shared/blocks/CallAvatar.vue";
import IconButton from "@src/components/ui/inputs/IconButton.vue";

const props = defineProps<{
  members: IContact[];
  activeCall: ICall;
  closeModal: () => void;
}>();
</script>

<template>
  <div class="w-full h-full pt-6 flex flex-col items-center">
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

      <p
        class="heading-2 text-black/70 dark:text-white/70 mb-4 outline-none"
        tabindex="0"
      >
        {{ getCallName(activeCall) }}
      </p>

      <p class="body-3 outline-none text-green-300" tabindex="0">
        {{ activeCall.direction }}
      </p>
    </div>

    <!--call actions-->
    <div class="mb-9 flex">
      <!--add member to call-->
      <div class="mr-5 first-letter:flex flex-col justify-center items-center">
        <IconButton class="ic-btn-contained-gray p-3 mb-3">
          <UserPlusIcon class="w-4.25 h-4.25" />
        </IconButton>
        <p class="body-4 text-black/70 dark:text-white/70">add</p>
      </div>

      <!--mute sound-->
      <div class="mr-5 flex flex-col justify-center items-center">
        <IconButton class="ic-btn-contained-gray p-3 mb-3">
          <SpeakerXMarkIcon
            class="w-4.25 h-4.25 text-black/60 dark:text-white/70"
          />
        </IconButton>
        <p class="body-4 text-black/70 dark:text-white/70">mute</p>
      </div>

      <!--open chat-->
      <div class="flex flex-col justify-center items-center">
        <IconButton class="ic-btn-contained-gray p-3 mb-3">
          <ChatBubbleBottomCenterTextIcon
            class="w-4.25 h-4.25 text-black/60 dark:text-white/70"
          />
        </IconButton>
        <p class="body-4 text-black/70 dark:text-white/70">chat</p>
      </div>
    </div>

    <!--call actions-->
    <div
      class="relative w-full h-12.5 rounded-b-xl flex justify-center bg-gray-50 dark:bg-gray-700"
    >
      <div class="absolute bottom-4.75">
        <div class="p-3 rounded-full bg-white dark:bg-gray-800">
          <IconButton
            @click="
              () => {
                props.closeModal();
              }
            "
            class="ic-btn-contained-danger p-4.25"
          >
            <PhoneIcon class="w-5 h-5" />
          </IconButton>
        </div>
      </div>
    </div>
  </div>
</template>
