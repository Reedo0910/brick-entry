<template>
  <div class="key-map">
    <div
      class="key-group"
      v-for="m in map"
      :key="m.title"
      :class="m.title"
      v-show="activePanel === m.title && activeState"
    >
      <div v-for="c in m.array" :key="c" :id="c" class="char">{{ c }}</div>
    </div>
  </div>
</template>

<script>
  import bus from './../assets/utils/eventBus';
  export default {
    props: ['activeState'],
    data() {
      return {
        activePanel: '',
        map: [
          {
            title: 'abc',
            array: ['a', 'b', 'c']
          },
          {
            title: 'def',
            array: ['d', 'e', 'f']
          },
          {
            title: 'ghi',
            array: ['g', 'h', 'i']
          },
          {
            title: 'jkl',
            array: ['j', 'k', 'l']
          },
          {
            title: 'mno',
            array: ['m', 'n', 'o']
          },
          {
            title: 'pqrs',
            array: ['p', 'q', 'r', 's']
          },
          {
            title: 'tuv',
            array: ['t', 'u', 'v']
          },
          {
            title: 'wxyz',
            array: ['w', 'x', 'y', 'z']
          },
          {
            title: 'mark',
            array: [',', '.', '!', '?']
          },
          {
            title: 'num',
            array: ['1', '2', '3', '4']
          },
        ]
      }
    },
    created() {
      const vm = this;
      bus.$on('setActivePanel', (panel) => {
        vm.activePanel = panel;
      });
    }
  }
</script>

<style lang="scss" scoped>
  @mixin key-position($left, $top) {
    left: $left;
    top: $top;
  }

  .key-map {
    position: relative;
    color: #fff;
    z-index: 200;
    font-size: 20px;
    pointer-events: none;
  }

  .char {
    position: absolute;
    left: 30px;
    top: 30px;
  }

  #a {
    @include key-position(43px, 70px);
  }

  #b {
    @include key-position(87px, 84px);
  }

  #c {
    @include key-position(113px, 123px);
  }

  #d {
    @include key-position(45px, 52px);
  }

  #e {
    @include key-position(81px, 81px);
  }

  #f {
    @include key-position(85px, 128px);
  }

  #g {
    @include key-position(69px, 34px);
  }

  #h {
    @include key-position(79px, 82px);
  }

  #i {
    @include key-position(58px, 117px);
  }

  #j {
    @include key-position(98px, 24px);
  }

  #k {
    @include key-position(84px, 71px);
  }

  #l {
    @include key-position(48px, 100px);
  }

  #m {
    @include key-position(40px, 77px);
  }

  #n {
    @include key-position(93px, 76px);
  }

  #o {
    @include key-position(125px, 40px);
  }

  #p {
    @include key-position(36px, 26px);
  }

  #q {
    @include key-position(65px, 62px);
  }

  #r {
    @include key-position(116px, 74px);
  }

  #s {
    @include key-position(158px, 50px);
  }

  #t {
    @include key-position(66px, 36px);
  }

  #u {
    @include key-position(88px, 81px);
  }

  #v {
    @include key-position(137px, 98px);
  }

  #w {
    @include key-position(102px, 12px);
  }

  #x {
    @include key-position(85px, 58px);
  }

  #y {
    @include key-position(103px, 106px);
  }

  #z {
    @include key-position(147px, 126px);
  }

  #\, {
    @include key-position(141px, 20px);
  }

  #\. {
    @include key-position(98px, 49px);
  }

  #\! {
    @include key-position(86px, 106px);
  }

  #\? {
    @include key-position(107px, 151px);
  }

  #\31 {
    @include key-position(163px, 63px);
  }
  #\32 {
    @include key-position(115px, 65px);
  }
  #\33 {
    @include key-position(74px, 96px);
  }
  #\34 {
    @include key-position(69px, 145px);
  }
  
</style>
