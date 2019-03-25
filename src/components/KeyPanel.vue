<template>
  <div class="key-panel" :class="panelName" v-show="!value || activePanel === panelName">
    <label
      :for="panelName"
      class="center-key"
      :data-keyname="getFirstLetter(panelKeys)"
      @click="SetPanel"
    ></label>
    <div class="cssplay-menu">
      <div>
        <input
          type="checkbox"
          :id="panelName"
          class="key-input"
          :checked="value"
          @change="$emit('setactive', $event.target.checked)"
        >
        <div class="holder">
          <div class="segment">
            <button v-for="k in panelKeys" :key="`button${k}`" :for="k" @click="InputChar(k)"></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import './../assets/style/custom.scss';
  import bus from './../assets/utils/eventBus'

  export default {
    props: {
      panelName: {
        type: String,
        default: '123'
      },
      panelKeys: {
        type: Array,
        required: true
      },
      value: {
        type: Boolean
      }
    },
    data() {
      return {
        activePanel: ''
      }
    },
    model: {
      prop: 'value',
      event: 'setactive'
    },
    created() {
      const vm = this;
      bus.$on('setActivePanel', (panel) => {
        vm.activePanel = panel;
      });
    },
    methods: {
      SetPanel: function () {
        bus.$emit('setActivePanel', this.panelName);
      },
      InputChar: function (key) {
        bus.$emit('setInput', key);
        this.$emit('setactive', false);
      },
      getFirstLetter: function (keys) {
        const copy = keys.concat();
        const tarArr = copy.sort();
        return tarArr[0];
      }
    }
  }
</script>

<style lang="scss" scoped>
  * {
    user-select: none;
    outline: none;
    -webkit-tap-highlight-color: transparent;
  }

  input,
  input:focus,
  button,
  button:focus {
    outline: none;
  }

  button {
    background-color: transparent;
    border: none;
  }

  .key-panel {
    position: absolute;
    width: 200px;
    height: 200px;
  }

  .cssplay-menu {
    box-sizing: border-box;
    position: relative;
    margin: 0 auto;
    width: 100%;
    max-width: 568px;
    height: 0;
    z-index: 2;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
    transform: translate3d(0, 0, 0);
  }

  .cssplay-menu > div {
    position: relative;
    max-width: 100%;
  }

  .cssplay-menu * {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }

  .cssplay-menu .holder {
    position: relative;
    padding-bottom: 100%;
    max-width: 100%;
    height: 0;
    overflow: hidden;
    display: none;
  }

  .cssplay-menu input {
    position: absolute;
    display: none;
  }

  .cssplay-menu .segment {
    position: absolute;
    z-index: 15;
    left: 50%;
    top: 50%;
    margin-left: -48%;
    margin-top: -48%;
    width: 96%;
    height: 96%;
    border-radius: 50%;
    overflow: hidden;
    transform: scale(0);
    /* transition: 0.5s cubic-bezier(.58, 2.4, 0.5, 0.5);
                                                                                  transition: 0.5s ease; */
  }

  .cssplay-menu .segment button {
    display: block;
    position: absolute;
    left: 50%;
    top: 50%;
    width: 50%;
    height: 50%;
    background: #444;
    color: #fff;
    border: 1px solid #888;
    cursor: pointer;
    transform-origin: left top;
    /* transition: 0.25s cubic-bezier(0, 0, 1, 1);
                                                                                  transition: 0.25s ease; */
  }

  //   .cssplay-menu .segment label .ph {
  //     display: block;
  //     position: absolute;
  //     left: 0;
  //     top: 0;
  //     right: 15px;
  //     bottom: 25px;
  //     margin: auto;
  //     width: 35px;
  //     height: 35px;
  //     background-position: center center;
  //     background-repeat: no-repeat;
  //   }

  .center-key {
    display: block;
    position: absolute;
    z-index: 200;
    left: 50%;
    top: 50%;
    margin-left: -10%;
    margin-top: -10%;
    width: 20%;
    height: 20%;
    border-radius: 50%;
    background-color: #222;
    overflow: hidden;
    cursor: pointer;
  }

  .center-key::after {
    content: attr(data-keyname);
    color: #fff;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    font-size: 20px;
    width: 24px;
    height: 24px;
    margin: auto;
    line-height: 20px;
    text-align: center;
  }

  .cssplay-menu .key-input:checked + .holder {
    display: block;
  }

  .cssplay-menu .key-input:checked + .holder .segment {
    /* transition: 0.5s cubic-bezier(.58, 3, 0.5, 0.5);
                                                                                  transition: 0.5s ease; */
    transform: scale(1);
  }

  .center-key:hover {
    transition: 0.5s cubic-bezier(0.58, 3, 0.5, 0.5);
    transition: 0.5s ease;
    background-color: #666;
  }

  .segment button:hover {
    background-color: #888;
  }
</style>

