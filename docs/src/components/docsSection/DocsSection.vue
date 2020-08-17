<template>
	<article class="docs-section__wrap" :id="section.id">
		<header class="section-header">
			<div class="header-content">
				<div class="section-title__wrap">
					<h1 class="section-title">
						{{ section.title }}
					</h1>
					<a :href="`#${section.id}`" class="section-anchor">
						<icon-link></icon-link>
						<span class="screen-reader-only">Link to {{ section.title }}</span>
					</a>
				</div>

				<button class="section-examples-button">View Examples</button>
			</div>
		</header>
		<div class="section-content__wrap">
			<div class="section-content">
				<span class="section-quote" v-if="section.quote">{{ section.quote }}</span>
				<markdown-content :content="section.content"></markdown-content>
			</div>
		</div>
	</article>
</template>

<script>
import IconLink from '~/assets/icons/IconLink.svg'
import MarkdownContent from '~/components/reusable/MarkdownContent'

export default {
	name: 'DocsSection',
	props: ['section'],
	components: {
		IconLink,
		MarkdownContent,
	},
}
</script>

<style lang="scss" scoped>
$active-border-width: 0.5rem;

.docs-section__wrap {
	position: relative;
	min-height: 60vh;
}

.section-content__wrap {
	padding: 0 0 6vw;

	@include media('>=laptop') {
		padding: 4rem $sp-m;
	}

	@include media('>=desktop') {
		padding: 4rem $sp-m;
	}
}

.section-header {
	position: sticky;
	top: 0;
	z-index: 1;
	background-color: primary-color(50);
	padding: $sp-xs;
	border-bottom: 1px solid primary-color(200);

	@include media('<laptop') {
		margin-bottom: $sp-m;
	}
}

.header-content {
	display: flex;
	align-items: center;
}

.section-title__wrap {
	display: flex;
	align-items: center;
	position: relative;
}

.section-title {
	font-size: 1.5rem;
	line-height: 1;
	font-weight: 640;
	color: primary-color(700);

	@include media('<phone') {
		font-size: 1.25rem;
	}
}

.section-anchor {
	@include circle(1.25rem);
	display: flex;
	background-color: primary-color(700, 0.15);
	margin-left: $sp-xxs;
	transition: background-color 0.2s $ease-in-out, transform 0.2s $ease-in-out;

	svg {
		--icon-color: #{primary-color(600)};
		@include size(0.75rem);
		margin: auto;
	}

	&:focus,
	&:hover {
		outline: none;
		background-color: primary-color(600);

		svg {
			--icon-color: white;
		}
	}

	&:hover {
		transform: scale(1.25);
	}

	&:active {
		background-color: $cyan;
		transform: scale(1);

		svg {
			--icon-color: #{$white};
		}
	}
}

.section-examples-button {
	margin-left: auto;
	height: 1.75rem;
	display: none;
	align-items: center;
	padding: 0 $sp-xxs;
	border-radius: $br-m;
	background-color: primary-color(100);
	color: primary-color(700);
	font-weight: 500;
	font-size: $fs-s;
	transition: background-color 0.3s $ease-out, color 0.3s $ease-out;

	&::after {
		display: inline-block;
		content: '→';
		margin-left: $sp-xxxs;
		transition: transform 0.2s $ease-out-back;
	}

	&:hover,
	&:focus {
		background-color: primary-color(300);
		color: primary-color(800);

		&::after {
			transform: translateX(0.75rem);
		}
	}

	@include media('<laptop') {
		display: flex;
	}
}

.section-quote {
	display: block;
	font-weight: 450;
	font-size: $fs-l;
	line-height: 1.75rem;
	color: primary-color(600);
	margin-bottom: $sp-m;
}

.section-content {
	position: relative;
	padding: 0 $sp-s $sp-l;
	max-width: 48rem;
	width: 100%;
	margin: auto;
	transition: background-color 0.5s $ease-in-out;

	@include media('>=laptop') {
		padding: $sp-xl $sp-l;

		.docs-section__wrap.active & {
			background-color: white;
			border-radius: 1rem;
		}
	}

	@include media('>=x-large') {
		padding: $sp-xl;
	}
}
</style>
