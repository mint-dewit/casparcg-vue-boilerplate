<template>
    <div class="fullscreen">
        <div class="box accent" ref="accentBox"></div>
        <div class="box main" ref="mainBox"></div>
        <div class="logo" ref="logo"></div>
        <div class="text" ref="text">
            Vue x CasparCG
        </div>
    </div>
</template>

<script>
import { TimelineLite, Power2 } from 'gsap'

export default {
    methods: {
        play () {
            this.introAnimation.seek(0);
            this.introAnimation.play()

            setTimeout(() => this.stop(), 2000)
        },
        stop () {
            this.outroAnimation.seek(0);
            this.outroAnimation.play()
        }
    },
    data () {
        return {
            introAnimation: null,
            outroAnimation: null
        }
    },
    mounted () {
        const { accentBox, mainBox, logo, text } = this.$refs
        this.introAnimation = new TimelineLite({ paused: true })
        this.outroAnimation = new TimelineLite({ paused: true })
        
        this.introAnimation.to(accentBox, 0.3, {
            width: '100vw',
            ease: Power2.out
        })
        this.introAnimation.to(mainBox, 0.3, {
            width: '100vw',
            ease: Power2.out
        }, '-= .2')
        this.introAnimation.to(logo, 0.5, {
            marginLeft: '-20vh',
            opacity: 1
        })
        this.introAnimation.to(text, 0.5, {
            marginLeft: '0vw',
            opacity: 1,
        }, '-= .5')
        this.introAnimation.fromTo(text, 5, {
            letterSpacing: '0vw',
            ease: Power2.easeInOut
        }, {
            letterSpacing: '.7vw',
        }, '-= .5')

        this.outroAnimation.to(text, 0.5, {
            marginLeft: '5vw',
            opacity: 0
        })
        this.outroAnimation.to(logo, 0.5, {
            marginLeft: '-15vh',
            opacity: 0
        }, '-= .5')
        this.outroAnimation.to(mainBox, 0.3, {
            width: '0vw',
            left: '100vw',
            ease: Power2.out
        }, '-= .3')
        this.outroAnimation.to(accentBox, 0.3, {
            width: '0vw',
            left: '100vw',
            ease: Power2.out
        }, '-= .2')

// dev
        // this.introAnimation.seek(2)
        // setTimeout(() => this.stop(), 2500)
    }
}
</script>

<style scoped>
.box {
    position: fixed;
    width: 0;
    height: 100vh;
}
.box.accent {
    background-color: var(--primary-accent-color);
}
.box.main {
    background-color: var(--fill-color);
}
.text {
    position: fixed;
    width: 100vw;
    top: 60vh;
    text-align: center;
    font-size: 6vh;
    letter-spacing: 0vw;
    opacity: 0;
    margin-left: -5vh;
}
.logo {
    position: fixed;
    width: 40vh;
    height: 40vh;
    top: 20vh;
    left: 50vw;
    margin-left: -25vh;

    background-image: url(../../assets/logo.png);
    background-size: contain;
    background-repeat: no-repeat;
    opacity: 0;
}
</style>


