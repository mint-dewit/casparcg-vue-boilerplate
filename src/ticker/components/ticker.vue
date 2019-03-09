<template>
    <div class="fullscreen">
        <div class="bar ticker">
            <div class="inner" ref="ticker">
                <span ref="text" :style="{ marginLeft: `${-offset}vw` }">{{ f0 }}</span>
            </div>
        </div>
        <div class="bar clock">
            <div class="inner" ref="clock">
                {{ time }}
            </div>
        </div>
    </div>
</template>

<script>
import { TimelineLite, Circ } from 'gsap'

export default {
    props: {
        f0: String,
    },
    data () {
        return {
            timelineIntro: null,
            timelineOutro: null,
            time: '',
            offset: -100,
            lastTime: undefined
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
        },
        update () {
            if (this.lastTime) {
                this.offset += (Date.now() - this.lastTime) / 250
                if (this.offset > 100 * this.$refs.text.offsetWidth / window.screen.availWidth - 10) this.offset = -100
            }

            this.lastTime = Date.now()
            requestAnimationFrame(this.update)
        }
    },
    mounted () {
        const { clock, ticker } = this.$refs

        this.timelineIntro = new TimelineLite({ paused: true })
        this.timelineIntro.to(ticker, .75, {
            marginTop: '0vh',
            ease: Circ.easeInOut
        })
        this.timelineIntro.to(clock, .75, {
            marginTop: '0vh',
            ease: Circ.easeInOut
        }, '-= 0.5')

        this.timelineOutro = new TimelineLite({ paused: true })
        this.timelineOutro.to(clock, .75, {
            marginTop: '-5vh',
            ease: Circ.easeInOut
        })
        this.timelineOutro.to(ticker, .75, {
            marginTop: '-5vh',
            ease: Circ.easeInOut
        }, '-= 0.5')

        setInterval(() => {
            this.time = new Date().toLocaleTimeString(navigator.language, {
                hour: '2-digit',
                minute:'2-digit'
            })
        }, 1000)

        this.time = new Date().toLocaleTimeString(navigator.language, {
            hour: '2-digit',
            minute:'2-digit'
        })

        setTimeout(() => this.update(), 750)
    }
}
</script>

<style>
.bar {
    position: fixed;
    height: 5vh;
    bottom: 5vh;
    line-height: 5vh;
    font-size: 4vh;
}

.bar.clock {
    overflow: hidden;
}
.bar.clock .inner {
    margin-top: 5vh;
    background-color: var(--fill-color);
    padding-right: .5vw;
    padding-left: 5.5vw;
    font-variant-numeric: tabular-nums;
}

.bar.ticker {
    width: 100vw;
    overflow: hidden;
}
.bar.ticker .inner {
    margin-top: 5vh;
    background-color: var(--primary-accent-color);
}
</style>


