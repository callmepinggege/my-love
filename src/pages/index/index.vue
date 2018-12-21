<style lang="stylus" scoped>
.canvas,.box
    width 100%
    height 100%
    position absolute
    top 0
    img 
      position absolute
      top 20px
      right 20px
      width 20px
      height 20px
      z-index 999
    
</style>

<style scoped>
  @keyframes myfirst {
    0% {
      transform: rotate(0deg)
    }
    50% {
      transform: rotate(180deg)
    }
    100% {
      transform: rotate(360deg)
    }
  }
  .cd {
    animation: myfirst 2s;
    animation-iteration-count: infinite;
  }
</style>

<template lang="pug">
  .box
    canvas.canvas(canvas-id="firstCanvas" disable-scroll=true)
    img(@click="change" src="http://fpi.imfancy.cn/CD.png" :class="computedClassStr")
    audio(id="myAudio" )
</template>

<script>
  import Draw from '../../utils/wxdraw'
  let wxDraw = Draw.wxDraw;
  let Shape = Draw.Shape;
  export default {
    data() {
      return {
        wxCanvas: null,
        audioCtx: null,
        paly: true
      }
    },
    components: {},
    computed: {
      computedClassStr() {
        return this.paly ? 'cd' : ''
      },
    },
    methods: {
      change() {
        this.paly = !this.paly
        if (this.paly === true) {
          this.audioCtx.play()
        } else {
          this.audioCtx.pause()
        }
      }
    },
    created() {},
    onReady(e) {
      this.audioCtx = wx.createAudioContext('myAudio')
      this.audioCtx.setSrc('http://fpi.imfancy.cn/wanghou.mp3')
      this.audioCtx.play()
      let context = wx.createCanvasContext('firstCanvas')
      wx.getSystemInfo({
        success(res) {
          let width = res.windowWidth * res.pixelRatio
          let height = res.windowHeight * res.pixelRatio
          this.wxCanvas = new wxDraw(context, 0, 0, res.windowWidth * res.pixelRatio, res.windowHeight * res.pixelRatio)
          let rect = new Shape('rect', {
            x: 0,
            y: 0,
            w: res.windowWidth * res.pixelRatio,
            h: res.windowHeight * res.pixelRatio,
            fillStyle: "#c0f3fb"
          })
          this.wxCanvas.add(rect)
          for (let i = 0; i < 1000; i++) {
            let img = new Shape('image', {
              x: Math.round(Math.random() * width),
              y: 0,
              w: 10,
              h: 10,
              file: "http://fpi.imfancy.cn/snow.png"
            }, 'fill', true)
            this.wxCanvas.add(img)
            img.animate({
              "x": "+=10",
              "y": "+=" + Math.round(Math.random() * height)
            }, {
              duration: Math.round(Math.random() * 10000)
            }).animate("rotate", Math.PI * 5, {
              duration: 1000
            }).start(true);
          }
          let text = new Shape('text', {
              x: 60,
              y: 100,
              text: "亲爱的然然宝贝",
              fillStyle: "#E6781E",
            },
            'fill', true)
          this.wxCanvas.add(text)
          text.animate({
            fillStyle: "#2B4E72"
          }, {
            duration: 1000
          }).animate({
            fontSize: "+=16"
          }, {
            duration: 1000,
            onEnd: () => {
              let text = new Shape('text', {
                  x: 60,
                  y: 150,
                  text: "圣诞快乐",
                  fillStyle: "#E6781E",
                },
                'fill', true)
              this.wxCanvas.add(text)
              text.animate({
                fillStyle: "#2B4E72"
              }, {
                duration: 1000
              }).animate({
                fontSize: "+=16"
              }, {
                duration: 1000,
                onEnd: () => {
                  let text = new Shape('text', {
                      x: 60,
                      y: 200,
                      text: "往后余生",
                      fillStyle: "#E6781E",
                    },
                    'fill', true)
                  this.wxCanvas.add(text)
                  text.animate({
                    fillStyle: "#2B4E72"
                  }, {
                    duration: 1000
                  }).animate({
                    fontSize: "+=16"
                  }, {
                    duration: 1000,
                    onEnd: () => {
                      let text = new Shape('text', {
                          x: 60,
                          y: 250,
                          text: "由我陪你一起走下去",
                          fillStyle: "#E6781E",
                        },
                        'fill', true)
                      this.wxCanvas.add(text)
                      text.animate({
                        fillStyle: "#2B4E72"
                      }, {
                        duration: 1000
                      }).animate({
                        fontSize: "+=16"
                      }, {
                        duration: 1000,
                        onEnd: () => {
                          let shou = new Shape('image', {
                            x: 180,
                            y: 380,
                            w: 300,
                            h: 200,
                            file: "http://fpi.imfancy.cn/qianshou.png"
                          }, 'fill', true)
                          this.wxCanvas.add(shou)
                        }
                      }).start(1)
                    }
                  }).start(1)
                }
              }).start(1)
            }
          }).start(1)
        }
      })
    },
  }
</script>


