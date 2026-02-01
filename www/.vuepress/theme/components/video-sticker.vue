<template lang="pug">
.video-sticker
	.letters(:class="state", :style="styles.shift")
		img.letter.wol(v-if="time > 1" src="../assets/ui/sticker/wol.svg")
		img.letter.ny(v-if="time > 1.2" src="../assets/ui/sticker/ny.svg")
		img.letter.jaz(v-if="time > 1.2" src="../assets/ui/sticker/jaz.svg")
		img.letter.do(v-if="time > 1.4" src="../assets/ui/sticker/do.svg")
		img.letter.w(v-if="time > 1.1" src="../assets/ui/sticker/w.svg")
</template>

<script>
export default {
	name: 'video-sticker',
	components: {},

	data(){
		return {
			styles: { shift: '' }
		}
	},

	props: {
		time: Number
	},

	computed: {
		state(){
			if (this.time > 3) return 'in'
			else return null
		}
	},

	methods: {
		scrollEvents(){
			const scrolled = window.pageYOffset
			this.styles.shift = {
				transform: `translateY(${ scrolled * -0.3 }px)`,
				maxWidth: 48 + scrolled * .03 + 'rem'
			}
		}
	},

	mounted() {
		window.addEventListener('scroll', this.scrollEvents)
	},

	destroyed(){
		window.removeEventListener('scroll', this.scrollEvents)
	}
}
</script>

<style lang="stylus" scoped>
$letterHeight = 25%

.video-sticker
	position relative
	margin 0 auto
	width 100%
	height 100%
	display flex
	flex-flow column
	justify-content center
.letters
	position relative
	height 80%
	width 100%
	max-width 48rem
	margin 0 auto
.letter
	display inline-block
	position absolute
	transition .2s all ease
	height $letterHeight
	&.wol
		left 5%
		top 5%
		animation a 3s linear infinite
	&.ny
		bottom 25%
		left 15%
		animation c 4s linear infinite
	&.jaz
		top 15%
		right 10%
		animation b 3s linear infinite
	&.do
		height $letterHeight * 1.3
		top 35%
		right 0
		animation a 4s linear infinite
	&.w
		bottom 5%
		right 10%
		animation c 2s linear infinite

@keyframes a
	0%
		transform translate3d(0, 0, 0)
	15%
		transform translate3d(-2%, -3%, 0)
	50%
		transform translate3d(1%, -1%, 0)
	100%
		transform translate3d(0, 0, 0)
@keyframes b
	0%
		transform translate3d(0, 0, 0)
	25%
		transform translate3d(1%, -3%, 0)
	60%
		transform translate3d(-1%, -2%, 0)
	100%
		transform translate3d(0, 0, 0)
@keyframes c
	0%
		transform translate3d(0, 0, 0)
	25%
		transform translate3d(2%, -2%, 0)
	50%
		transform translate3d(1%, 1%, 0)
	100%
		transform translate3d(0, 0, 0)
</style>
