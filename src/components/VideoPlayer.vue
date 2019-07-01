<template>
    <div class="c-video">
        <video :width="width" ref="video">
            <source :src="vidSrc" :type="type">
            Your browser does not support HTML5 video.
        </video>
        <div class="controls">
            <div class="outer-progress-bar">
                <div ref="progressBar" class="inner-progress-bar"></div>
            </div>
            <div class="buttons">
                <button ref="playBtn" @click="tooglePlay" id="play-pause"></button>
                <span ref="currentTime"></span>
            </div>

        </div>
    </div>
</template>
<script>
export default{
    props: {
        vidSrc: {
            type: String,
            default: "./assets/sample.mp4"
        },
        type: {
            type: String,
            default: "video/mp4"
        },
        width: {
            type: String,
            default: "100%"
        }
    },
    mounted(){
        let vid = this.$refs.video
        let playBtn = this.$refs.playBtn
        vid.addEventListener('timeupdate', () => {
            let progressPos = vid.currentTime / vid.duration
            let progressbar = this.$refs.progressBar
            progressbar.style.width = progressPos * 100 + "%"
            if(vid.ended){
                playBtn.className = 'play'
            }
        })
    },
    methods: {
        tooglePlay() {
            let vid = this.$refs.video
            let playBtn = this.$refs.playBtn
            if(vid.paused){
                playBtn.className = 'pause'
                vid.play()
            } else {
                playBtn.className = 'play'
                vid.pause()
            }
        }
    }
}
</script>
<style scoped>
video {
    outline:none;
    width:100%;
}
.c-video{
    position:relative;
    width:100%;
    max-width:800px;
    overflow:hidden;
}

.c-video:hover .controls{
    transform: translateY(0);
}
.controls{
    display:flex;
    position:absolute;
    flex-wrap:wrap;
    width:100%;
    bottom:0;
    background: rgba(0, 0, 0, 0.7);
    transform: translateY(100%) translateY(-4px);
    transition: all .2s;
}

.buttons button{
    background:none;
    border:none;
    outline:none;
    cursor:pointer;
}
.buttons{
    padding:10px;
}

.buttons button:before{
    content: "\f144";
    width:30px;
    height:30px;
    display:inline-block;
    font-size:28px;
    color:white;
    -webkit-font-smoothing:antialiased;
    font-family: FontAwesome;
}

.buttons button.play:before{
    content: "\f144";
}
.buttons button.pause:before{
    content: "\f28b";
}

.outer-progress-bar{
    top:0;
    height:10px;
    left:0;
    width:100%;
    background-color:black;
}

.inner-progress-bar{
    height:4px;
    background-color:orangered;

}



</style>