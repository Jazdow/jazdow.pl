<template lang='pug'>
	.oj-faq-item
		h3.question(@click="open = !open")
			| {{question}}
			span.toggle {{ open ? ' ↑' : ' ↓' }}
		.answer(:class="{open, closed: !open}")
			slot
</template>

<script>
export default {
	name: 'oj-faq-item',
	props: { question: String },
	data() { return { open: false } }
}
</script>

<style scoped lang='stylus'>
@import '../styles/component'
.question
	cursor pointer
	user-select none
	color $oj-violet
	&:hover
		opacity 0.8
.toggle
	font-weight 400
	font-size 0.9em
.answer
	overflow hidden
	&.open
		animation expander-open .2s ease
	&.closed
		animation expander-close .2s ease forwards
</style>
