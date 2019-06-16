<template>
    <div class="titlesafe">
        <div class="bar">
            <div class="bar-inner">
                <div class="accent" ref="accent"></div>
                <div class="content" ref="bar">
                    {{ f0 }}
                </div>
            </div>
        </div>
        <div class="bar sub" :class="{ 'opacity': displaySub ? 1 : 0 }">
            <div class="bar-inner" ref="subBar">
                {{ f1 }}
            </div>
        </div>
    </div>
</template>

<script>
import { TimelineLite, Circ, Power2 } from 'gsap'

export default {
    props: {
        f0: String,
        f1: String
    },
    computed: {
        displaySub () {
            if (this.f1) return true
            return false
        }
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
        const { accent, bar, subBar } = this.$refs

        this.timelineIntro = new TimelineLite({ paused: true })
        this.timelineIntro.to(accent, 0.6, {
            marginTop: '0vh',
            ease: Circ.easeInOut
        })
        this.timelineIntro.to(bar, 0.4, {
            marginTop: '0vh',
            ease: Power2.easeOut
        }, '-= .2')
        this.timelineIntro.to(subBar, 0.4, {
            marginTop: '0vh',
            ease: Power2.easeOut
        }, '-= .3')
        

        this.timelineOutro = new TimelineLite({ paused: true })
        this.timelineOutro.to(bar, 0.4, {
            marginTop: '-5vh',
            ease: Circ.easeIn
        })
        this.timelineOutro.to(subBar, 0.4, {
            marginTop: '-3vh',
            ease: Circ.easeIn
        }, '-= .3')
        this.timelineOutro.to(accent, 0.4, {
            marginTop: '-5vh',
            ease: Circ.easeInOut
        }, '+= .1')
        
    }
}
</script>

<style>
.bar {
    position: fixed;
    height: 5vh;
    line-height: 5vh;
    font-size: 4vh;
    overflow: hidden;
}

.bar.sub {
    height: 3vh;
    line-height: 3vh;
    font-size: 2.2vh;
    margin-top: 5vh;
    margin-left: 1vw;
}

/* .bar .bar-inner {
    margin-top: 5vh;
} */

.bar.sub .bar-inner {
    margin-top: 3vh;
    background-color: var(--secondary-accent-color);
    padding-left: .6vw;
    padding-right: .6vw;
}

.bar .bar-inner .accent {
    float: left;
    width: 1vw;
    height: 5vh;
    background-color: var(--fill-color);
    margin-top: 5vh;
}

.bar .bar-inner .content {
    float: left;
    height: 5vh;
    background-color: var(--primary-accent-color);
    padding-left: 1vw;
    padding-right: 1vw;
    margin-top: 5vh;
}

/* .bar.sub .bar-inner {
    display: inline-block;
    height: 5vh;
    background-color: var(--primary-accent-color);
    padding-left: 1vw;
    padding-right: 1vw;
} */
</style>


