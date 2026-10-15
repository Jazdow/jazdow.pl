<template lang='pug'>
	.oj-gallery
		.thumbs(@click="onClick")
			slot
		.lightbox(v-if="current !== null", @click.self="close")
			img(:src="images[current].src", :alt="images[current].alt")
			button.close(@click="close", aria-label="Zamknij") ×
			template(v-if="images.length > 1")
				button.prev(@click="step(-1)", aria-label="Poprzednie") ‹
				button.next(@click="step(1)", aria-label="Następne") ›
</template>

<script>
export default {
	name: 'oj-gallery',
	data() { return { images: [], current: null } },
	mounted() {
		this.images = Array.from(this.$el.querySelectorAll('.thumbs img'))
		document.addEventListener('keydown', this.onKey)
	},
	beforeDestroy() {
		document.removeEventListener('keydown', this.onKey)
	},
	methods: {
		onClick(e) {
			const i = this.images.indexOf(e.target)
			if (i !== -1) this.current = i
		},
		close() { this.current = null },
		step(d) {
			const n = this.images.length
			this.current = (this.current + d + n) % n
		},
		onKey(e) {
			if (this.current === null) return
			if (e.key === 'Escape') this.close()
			else if (e.key === 'ArrowLeft') this.step(-1)
			else if (e.key === 'ArrowRight') this.step(1)
		}
	}
}
</script>

<style scoped lang='stylus'>
@import '../theme/styles/component'
.thumbs
	display flex
	flex-wrap wrap
	gap 0.5rem
	margin 1em 0
	>>> p
		flex 1 1 unquote('calc((100% - 1rem) / 3)')
		margin 0
		min-width 0
	>>> img
		display block
		width 100%
		aspect-ratio 4 / 3
		object-fit cover
		cursor zoom-in
		transition opacity .2s
		&:hover
			opacity 0.85
.lightbox
	position fixed
	inset 0
	z-index 1000
	background rgba(0, 0, 0, 0.85)
	display flex
	align-items center
	justify-content center
	img
		max-width 90vw
		max-height 90vh
		object-fit contain
	button
		position absolute
		background none
		border none
		color white
		font-size 3rem
		line-height 1
		cursor pointer
		padding 1rem
		&:hover
			opacity 0.7
	.close
		top 0
		right 0
	.prev
		left 0
	.next
		right 0
</style>
