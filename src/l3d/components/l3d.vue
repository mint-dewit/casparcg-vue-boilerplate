<template>
    <div class="titlesafe left">
        <div class="block">
            <div class="inner-block" ref="box">
                <div class="img"></div>
            </div>
        </div>
        <div class="bars">
            <div class="bar f0">
                <div class="inner" ref="f0">{{ f0 }}</div>
            </div>
            <div class="bar f1">
                <div class="inner" ref="f1">{{ f1 }}</div>
            </div>
        </div>
    </div>
</template>

<script>
import { TimelineLite, Circ, Power2, Power4 } from 'gsap'

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
            marginTop: '0vw',
            ease: Circ.easeInOut
        })
        this.timelineIntro.to(f0, 0.4, {
            marginTop: 0,
            ease: Power2.easeOut
        }, '-= .2')
        this.timelineIntro.to(f1, 0.4, {
            marginTop: 0,
            ease: Power2.easeOut
        }, '-= .3')

        this.timelineOutro = new TimelineLite({ paused: true })
        this.timelineOutro.to(f0, 0.4, {
            marginTop: '-3vw',
            ease: Power2.easeIn
        })
        this.timelineOutro.to(f1, 0.4, {
            marginTop: '-3vw',
            ease: Power2.easeIn
        }, '-= .3')
        this.timelineOutro.to(box, 1, {
            marginTop: '-6vw',
            ease: Power4.easeIn
        }, '-= .5')
    }
}
</script>

<style>
.block {
    width: 6vw;
    height: 6vw;
    position: fixed;
    bottom: 5vh;
    left: 5vw;
    z-index: 1;
    overflow: hidden;
}
.inner-block {
    width: 100%;
    height: 100%;
    background: var(--fill-color);
    margin-top: 6vw;
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
    overflow: hidden;
}
.bar {
    height: 3vw;
    position: fixed;
    font-size: 2vw;
    line-height: 3vw;
    overflow: hidden;
}
.bar.f1 {
    margin-top: 3vw;
}
.bar .inner {
    color: var(--primary-text-color);
    padding-left: .5vw;
    padding-right: .5vw;
    margin-top: 3vw;
}
.bar.f0 .inner {
    background: var(--primary-accent-color);
}
.bar.f1 .inner {
    background: var(--secondary-accent-color);
    margin-top: 3vw;
}
</style>


