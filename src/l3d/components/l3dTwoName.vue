<template>
    <div class="titlesafe left">
        <div class="block">
            <div class="inner-block" ref="box">
                <div class="img"></div>
            </div>
        </div>
        <div class="bars">
            <div class="bar f0">
                <div class="inner" ref="f0">
                    {{ f0 }}
                    <span class="right-align">{{ f2 }}</span>
                </div>
            </div>
            <div class="bar f1">
                <div class="inner" ref="f1">
                    {{ f1 }}
                    <span class="right-align">{{ f3 }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import l3d from './l3d'

export default {
    extends: l3d,
    props: {
        f2: String,
        f3: String
    }
}
</script>

<style scoped>
.bar .inner {
    width: 84vw;
}
.right-align {
    text-align: right;
    float: right;
}
</style>


