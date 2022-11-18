<template>
    <div class="video-box">
        <video controls="controls" class="demo-video" ref="player" muted @dblclick="fullScreen"></video>
    </div>
</template>
   
<script>
import flvjs from 'flv.js'
export default {
    name: 'Home',
    components: {},
    data() {
        return {
            player: null,
            loading: true
        }
    },
    mounted() {
        this.playVideo()
    },
    watch: {
        rtsp: {
            handler: function (val) {
                if (val) {
                    if (this.player) {
                        this.player.unload()
                        this.player.destroy()
                        this.player = null
                        this.loading = true
                    }
                    this.$nextTick(() => {
                        this.playVideo()
                    })
                }
            },
            immediate: true
        }
    },
    methods: {
        fullScreen() {
            if (this.$refs.player.requestFullScreen) {
                this.$refs.player.requestFullScreen()
            } else if (this.$refs.player.mozRequestFullScreen) {
                this.$refs.player.mozRequestFullScreen()
            } else if (this.$refs.player.webkitRequestFullScreen) {
                this.$refs.player.webkitRequestFullScreen()
            }
        },
        playVideo() {
            const time1 = new Date().getTime()
            if (flvjs.isSupported()) {
                let video = this.$refs.player
                if (video) {
                    this.player = flvjs.createPlayer({
                        type: 'flv',
                        hasAudio: ture, // 是否有音频
                        hanVideo: ture, // 是否有视频
                        url: `ws://192.168.0.110:8199/rtsp/1/cnRzcDovL3dvd3phZWMyZGVtby5zdHJlYW1sb2NrLm5ldC92b2QvbXA0OkJpZ0J1Y2tCdW5ueV8xMTVrLm1wNA==`

                    })
                    this.player.attachMediaElement(video)
                    try {
                        this.player.load()
                        this.player.play().then(() => {
                            console.log(new Date().getTime() - time1)
                            this.loading = false
                        })
                    } catch (error) {
                        console.log(error)
                    }
                }
            }
        }
    },
    beforeDestroy() {
        if (this.player) {
            this.player.unload()
            this.player.destroy()
            this.player = null
        }
    }
}
</script>
<style>
.video-box {
    width: 100%;
    height: 100%;
}

video {
    width: 100%;
    height: 100%;
    object-fit: fill;
}

video::-webkit-media-controls-play-button {
    display: none;
}

video::-webkit-media-controls-current-time-display {
    display: none;
}

video::-webkit-media-controls-timeline {
    display: none;
}
</style>
   
   