<template>
    <div class="titlesafe left">
        <div class="block" ref="box">
            <div class="img"></div>
        </div>
        <div class="bars">
            <div class="bar f0" ref="f0">{{ f0 }}</div>
            <div class="bar f1" ref="f1">{{ f1 }}</div>
        </div>
    </div>
</template>

<script>
import { TimelineLite, Back, Power2, Power4 } from 'gsap'

export default {
    props: {
        f0: String,
        f1: String
    },
    data () {
        return {
            timelineIntro: null,
            timelineOutro: null
        }
    },
    methods: {
        play () {
            this.timelineIntro.seek(0)
            this.timelineIntro.play()
        },
        stop () {
            this.timelineOutro.seek(0)
            this.timelineOutro.play()
        }
    },
    mounted () {
        const { box, f0, f1 } = this.$refs

        this.timelineIntro = new TimelineLite({ paused: true })
        this.timelineIntro.to(box, 0.8, {
            // bottom: '5vh',
            left: '5vw',
            // height: '6vw',
            // width: '6vw',
            ease: Back.easeOut.config(1.7)
        })
        this.timelineIntro.to(f0, 0.4, {
            marginLeft: 0,
            opacity: 1,
            ease: Power2.easeOut
        }, '-= .2')
        this.timelineIntro.to(f1, 0.4, {
            marginLeft: 0,
            opacity: 1,
            ease: Power2.easeOut
        }, '-= .3')

        this.timelineOutro = new TimelineLite({ paused: true })
        this.timelineOutro.to(f0, 0.4, {
            marginLeft: '3vw',
            opacity: 0,
            ease: Power2.easeIn
        })
        this.timelineOutro.to(f1, 0.4, {
            marginLeft: '3vw',
            opacity: 0,
            ease: Power2.easeIn
        }, '-= .3')
        this.timelineOutro.to(box, 1, {
            left: '100vw',
            ease: Power4.easeIn
        }, '-= .5')
    }
}
</script>

<style scoped>
.block {
    width: 6vw;
    height: 6vw;
    background: var(--fill-color);
    position: fixed;
    bottom: 5vh;
    left: -6vw;
    z-index: 1;
    padding: 1vw;
}
.img {
    position: relative;
    height: 100%;
    width: 100%;
    background-image: url(../../assets/logo.png);
    background-size: contain;
    background-repeat: no-repeat;
}

.bars {
    position: fixed;
    height: 6vw;
    bottom: 5vh;
    left: 11vw;
}
.bar {
    height: 3vw;
    position: fixed;
    font-size: 2vw;
    line-height: 3vw;
    padding-left: .5vw;
    padding-right: .5vw;
    color: var(--primary-text-color);
    opacity: 0;
    margin-left: -3vw;
}
.bar.f0 {
    background: var(--primary-accent-color);
}
.bar.f1 {
    background: var(--secondary-accent-color);
    margin-top: 3vw;
}
</style>


