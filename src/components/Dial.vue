<template>
  <div class="container">
    <key-panel panel-name="abc" :panel-keys="['a','b','c']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="def" :panel-keys="['d','e','f']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="ghi" :panel-keys="['g','h','i']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="jkl" :panel-keys="['j','k','l']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="mno" :panel-keys="['o','n','m']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="pqrs" :panel-keys="['s','r','q','p']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="tuv" :panel-keys="['v','u','t']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="wxyz" :panel-keys="['z','y','x','w']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="mark" :panel-keys="['?','!','.',',']" v-model="isPanelActive"></key-panel>
    <key-panel panel-name="num" :panel-keys="['4','3','2','1']" v-model="isPanelActive"></key-panel>
    <button class="delete-center-key" data-keyname="⇤" v-show="!isPanelActive" @click="deleteChar"></button>
    <div class="dial-display" @click="inputSpace" id="display" ref="display">
      <span>{{ dialDisplay }}</span>
      <span class="cursor">_</span>
    </div>
    <key-map :activeState="isPanelActive"></key-map>
  </div>
</template>

<script>
  import bus from './../assets/utils/eventBus';
  import KeyPanel from './KeyPanel.vue';
  import KeyMap from './KeyMap.vue';
  import './../assets/style/custom.scss';

  export default {
    components: {
      KeyPanel,
      KeyMap
    },
    data() {
      return {
        isPanelActive: false,
        activePanel: '',
        dialDisplay: ''
      }
    },
    mounted() {
      const vm = this;
      bus.$on('setActivePanel', (panel) => {
        vm.activePanel = panel;
      });
      bus.$on('setInput', (key) => {
        vm.dialDisplay += key;
        vm.scrollToBottom();
      });
    },
    methods: {
      deleteChar: function () {
        this.dialDisplay = this.dialDisplay.substring(0, this.dialDisplay.length - 1);
        this.scrollToBottom();
      },
      inputSpace: function () {
        if (this.dialDisplay.length === 0) {
          return;
        }
        if (this.dialDisplay.trim().length === this.dialDisplay.length) {
          this.dialDisplay += ' ';
          this.scrollToBottom();
        }
      },
      scrollToBottom: function () {
        const tar = this.$refs.display;
        this.$nextTick(() => {
          return tar.scrollTop = tar.scrollHeight;
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  @keyframes twinkling {
    0% {
      opacity: 0;
    }
    50% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

  * {
    user-select: none;
    outline: none;
    -webkit-tap-highlight-color: transparent;
  }

  .container {
    background-color: #000;
    overflow: hidden;
    width: 185px;
    height: 185px;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    border-radius: 200px;
  }

  .dial-display {
    background-color: transparent;
    color: #fff;
    width: 80px;
    height: 80px;
    position: absolute;
    margin: auto;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    z-index: 1;
    word-wrap: break-word;
    overflow-y: auto;
  }

  .delete-center-key {
    display: block;
    position: absolute;
    z-index: 200;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #222;
    overflow: hidden;
    cursor: pointer;
    border: none;
    box-sizing: border-box;
    bottom: 0;
    left: 88px;
    &::after {
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
    &:hover {
      transition: 0.5s cubic-bezier(0.58, 3, 0.5, 0.5);
      transition: 0.5s ease;
      background-color: #666;
    }
  }

  .cursor {
    animation: twinkling 1s infinite ease;
  }
</style>

