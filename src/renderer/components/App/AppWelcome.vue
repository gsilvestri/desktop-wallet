<template>
  <div
    :style="`backgroundImage: url('${assets_loadImage(defaultBackground)}')`"
    class="px-20 py-16 w-screen h-screen relative"
  >
    <div
      class="bg-white w-full h-full animated fadeIn rounded-lg"
    >
      <div
        v-if="step == 1"
        :style="`backgroundImage: url('${assets_loadImage('pages/background-welcome.png')}')`"
        class="AppWelcome__background "
      />
      <div
        v-else
        class="w-full h-full"
      >
        <div
          :style="`backgroundImage: url('${assets_loadImage('pages/background-intro-mobile.png')}')`"
          class="block xl:hidden AppWelcome__background opacity-25 md:opacity-100"
        />
        <div
          :style="`backgroundImage: url('${assets_loadImage('pages/background-intro.png')}')`"
          class="hidden xl:block AppWelcome__background w-full h-full"
        />
      </div>
    </div>
    <div
      class="px-20 py-16 flex justify-center items-center rounded-lg w-full h-full pin-t pin-l fixed animated fadeIn lg:overflow-y-scroll"
    >
      <div
        v-if="step == 1"
        :key="1"
        class="text-center m-8"
      >
        <div class="flex justify-center items-center mb-8">
          <div class="AppWelcome__Logo">
            <img :src="assets_loadImage('kapu-logo.png')">
          </div>
        </div>
        <i18n
          path="INTRODUCTION.WELCOME.TITLE"
          tag="span"
          class="text-5xl"
        >
          <strong place="app">
            {{ $t('COMMON.APP_NAME') }}
          </strong>
        </i18n>
        <div class="mt-3">
          {{ $t('INTRODUCTION.WELCOME.SAFETY_MESSAGE') }}
        </div>
        <div class="mt-2">
          {{ $t('INTRODUCTION.WELCOME.FUNDS_WARNING') }}
        </div>
        <button
          class="blue-button mt-8"
          @click="start"
        >
          {{ $t('COMMON.START') }}
        </button>
      </div>

      <div
        v-else-if="step > 1"
        :key="2"
        class="flex w-full h-full relative"
      >
        <div class="absolute pin-t pin-l">
          <div class="AppWelcome__Logo__corner">
            <img :src="assets_loadImage('kapu-logo.png')">
          </div>
        </div>

        <div
          class="flex w-full h-full block lg:hidden"
        >
          <AppIntroScreenMobile
            v-if="step == 2"
            :is-first="true"
            :selection="1"
            @back="moveTo(1)"
            @next="moveTo(3)"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.POWER.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreenMobile>

          <AppIntroScreenMobile
            v-if="step == 3"
            :selection="2"
            @back="moveTo(2)"
            @next="moveTo(4)"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.DUTY.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreenMobile>

          <AppIntroScreenMobile
            v-if="step == 4"
            :selection="3"
            @back="moveTo(3)"
            @next="moveTo(5)"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.RESPONSIBILITY.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreenMobile>

          <AppIntroScreenMobile
            v-if="step == 5"
            :is-last="true"
            :selection="4"
            @back="moveTo(4)"
            @done="done"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.TURN.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreenMobile>
        </div>

        <div
          class="hidden lg:block lg:flex lg:w-full lg:h-full"
        >
          <AppIntroScreen
            v-if="step == 2"
            :is-first="true"
            :selection="1"
            @back="moveTo(1)"
            @next="moveTo(3)"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.POWER.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreen>

          <AppIntroScreen
            v-if="step == 3"
            :selection="2"
            @back="moveTo(2)"
            @next="moveTo(4)"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.DUTY.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreen>

          <AppIntroScreen
            v-if="step == 4"
            :selection="3"
            @back="moveTo(3)"
            @next="moveTo(5)"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.RESPONSIBILITY.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreen>

          <AppIntroScreen
            v-if="step == 5"
            :is-last="true"
            :selection="4"
            @back="moveTo(4)"
            @done="done"
          >
            <i18n
              slot="title"
              path="INTRODUCTION.PAGE_TITLE"
              tag="span"
            >
              <strong place="page">
                {{ $t('INTRODUCTION.TURN.TITLE') }}
              </strong>
            </i18n>
          </AppIntroScreen>
        </div>
      </div>
    </div>
    <AppFooter
      class="mt-4"
    />
  </div>
</template>

<script>
import { AppFooter, AppIntroScreen } from '@/components/App'
import { AppIntroScreenMobile } from '@/components/App/mobile'

export default {
  name: 'AppWelcome',

  components: {
    AppFooter,
    AppIntroScreen,
    AppIntroScreenMobile
  },

  props: {
  },

  data: () => ({
    step: 1,
    isMobile: false
  }),

  computed: {
    defaultBackground () {
      return 'wallpapers/1Default.png'
    }
  },

  methods: {
    start () {
      this.step = 2
    },

    moveTo (step) {
      this.step = step
    },

    done () {
      this.$emit('done')
    }
  }
}
</script>

<style lang="postcss" scoped>
.AppWelcome__Logo {
  box-shadow: 0 10px 15px #AB8B64;
  @apply .bg-brown-dark .w-24 .p-4 .rounded-lg
}

.AppWelcome__background {
  background-size: contain;
  background-position: top left;
  @apply .bg-no-repeat .w-full .h-full
}

.AppWelcome__Logo__corner {
  @apply .bg-brown-dark .w-18 .px-3 .py-4 .rounded-tl-lg .rounded-br-lg
}
</style>
