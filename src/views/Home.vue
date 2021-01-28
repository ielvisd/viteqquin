<template>
  <main>
    <div class="bg-gray-50">
      <div
        class="max-w-screen-xl px-4 py-12 mx-auto sm:px-6 lg:py-16 lg:px-8 lg:flex lg:items-center lg:justify-between"
      >
        <h2
          class="text-3xl font-extrabold leading-9 tracking-tight text-gray-900 sm:text-4xl sm:leading-10"
        >
          Ready to dive in?
          <br />
          <span class="text-indigo-600">Vite 2.x + Vue 3.x + Tailwind 2.x</span>
        </h2>
        <div class="flex mt-8 lg:flex-shrink-0 lg:mt-0">
          <div class="inline-flex rounded-md shadow">
            <router-link
              to="/about"
              class="inline-flex items-center justify-center px-5 py-3 text-base font-medium leading-6 text-white transition duration-150 ease-in-out bg-indigo-600 border border-transparent rounded-md hover:bg-indigo-500 focus:outline-none focus:shadow-outline"
              >Next Page</router-link
            >
          </div>
          <ButtonRepo />
        </div>
      </div>
    </div>
    <div class="app">
    <div class="controls-container">
      <div class="control-container">
        <label for="toggle_button">
          <span>Position </span>
          <input
            type="checkbox"
            id="toggle_button"
            v-model="positionControlValue"
          />
        </label>

        <div v-if="showPositionControls">
          <p>x-position: {{ xPosition }}</p>
          <vue-slider v-model="xPosition" :min="-50" :max="50" :interval="1" />
          <p>y-position: {{ yPosition }}</p>
          <vue-slider v-model="yPosition" :min="-10" :max="10" :interval="1" />
          <p>z-position: {{ zPosition }}</p>
          <vue-slider v-model="zPosition" :min="-50" :max="50" :interval="1" />
        </div>
      </div>

      <div class="control-container">
        <label for="toggle_button">
          <span>Body Motion </span>
          <input
            type="checkbox"
            id="toggle_button"
            v-model="figureControlValue"
          />
        </label>
        <div v-if="showFigureControls">
          <p>bend: {{ bend }}</p>
          <vue-slider v-model="bend" :min="0" :max="360" :interval="1" />
          <p>turn: {{ turn }}</p>
          <vue-slider v-model="turn" :min="0" :max="360" :interval="1" />
          <p>tilt: {{ tilt }}</p>
          <vue-slider v-model="tilt" :min="0" :max="360" :interval="1" />
        </div>
      </div>

      <div class="control-container">
        <label for="toggle_button">
          <span
            >Head Motion </span
          >
          <input
            type="checkbox"
            id="toggle_button"
            v-model="headMotionControlValue"
          />
        </label>
        <div v-if="showHeadMotionControls">
          <p>Nod: {{ headNod }}</p>
          <vue-slider v-model="headNod" :min="-90" :max="90" :interval="1" />
          <p>turn: {{ headTurn }}</p>
          <vue-slider v-model="headTurn" :min="-90" :max="90" :interval="1" />
          <p>tilt: {{ headTilt }}</p>
          <vue-slider v-model="headTilt" :min="-90" :max="90" :interval="1" />
        </div>
      </div>
    </div>
    <component
      class="model"
      :is="test"
      :xposition="xPosition"
      :yposition="yPosition"
      :zposition="zPosition"
      :bend="bend"
      :turn="turn"
      :tilt="tilt"
      :headNod="headNod"
      :headTurn="headTurn"
      :headTilt="headTilt"
    />
  </div>
  </main>
</template>

<script>
// see the syntax-sugared version in About.vue
import ButtonRepo from '@/components/ButtonRepo.vue'
import Stage from '@/components/Stage.vue'
import VueSlider from "vue-slider-component";
import 'vue-slider-component/theme/antd.css'


export default {
  components: { ButtonRepo, Stage, VueSlider },
data() {
    return {
      checked1: false,
      xPosition: 0,
      yPosition: -5,
      zPosition: 0,
      bend: 20,
      turn: 0,
      tilt: 0,
      headNod: 0,
      headTurn: 0,
      headTilt: 0,
      value1: "Left",
      options: ["Left", "Right"],
      test: "Stage",
      showPositionControls: false,
      showFigureControls: false,
      showHeadMotionControls: false,
    };
  },
  computed: {
    positionControlsActive() {
      return this.showPositionControls;
    },
    positionControlValue: {
      get() {
        return this.showPositionControls;
      },
      set(newValue) {
        this.showPositionControls = newValue;
        this.showFigureControls = false;
        this.showHeadMotionControls = false;
      },
    },
    figureControlsActive() {
      return this.showFigureControls;
    },
    figureControlValue: {
      get() {
        return this.showFigureControls;
      },
      set(newValue) {
        this.showFigureControls = newValue;
        this.showPositionControls = false;
        this.showHeadMotionControls = false;
      },
    },
    headMotionControlsActive() {
      return this.showHeadMotionControls;
    },
    headMotionControlValue: {
      get() {
        return this.showHeadMotionControls;
      },
      set(newValue) {
        this.showHeadMotionControls = newValue;
        this.showFigureControls = false;
        this.showPositionControls = false;
      },
    },
  },
}
</script>


<style lang="scss" scoped>
.app {
  /* background: peru; */
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  border: 3px solid orange;
  max-width: 800px;
  margin: 0 auto
}

.controls-container {
  padding: 12px;
  width: 200px;
  border: 5px solid blue;
  min-height: 500px;
}

.control-container {
  margin-top: 12px;
  // border: 5px solid green;
}

.model {
  border: 5px solid green;
  width: 100%;
  /* height: 100vh; */
}

.p-slider-horizontal,
.p-inputtext {
  width: 14rem;
}

.p-slider-vertical {
  height: 14rem;
}

.toggle__button {
  vertical-align: middle;
  user-select: none;
  cursor: pointer;
}
.toggle__button input[type="checkbox"] {
  opacity: 0;
  position: absolute;
  width: 1px;
  height: 1px;
}
.toggle__button .toggle__switch {
  display: inline-block;
  height: 12px;
  border-radius: 6px;
  width: 40px;
  background: #BFCBD9;
  box-shadow: inset 0 0 1px #BFCBD9;
  position: relative;
  margin-left: 10px;
  transition: all 0.25s;
}

.toggle__button .toggle__switch::after,
.toggle__button .toggle__switch::before {
  content: "";
  position: absolute;
  display: block;
  height: 18px;
  width: 18px;
  border-radius: 50%;
  left: 0;
  top: -3px;
  transform: translateX(0);
  transition: all 0.25s cubic-bezier(0.5, -0.6, 0.5, 1.6);
}

.toggle__button .toggle__switch::after {
  background: #4D4D4D;
  box-shadow: 0 0 1px #666;
}
.toggle__button .toggle__switch::before {
  background: #4D4D4D;
  box-shadow: 0 0 0 3px rgba(0, 0, 0, 0.1);
  opacity: 0;
}
</style>