<template>
  <ul class="nav-sections">
  	<li
  		v-for="section in sections"
  		class="nav-section__item xyz-in-nested"
  		@click="onSectionClick"
  		:key="section.title"
  	>
      <page-nav-sections v-if="section.sections" :sections="section.sections"></page-nav-sections>

  		<a v-if="!section.sections" :href="`#${section.anchor}`" class="nav-section__link scrollactive-item">
  			<div class="link-dot__wrap">
  				<span class="link-dot"></span>
  			</div>
  			<span class="link-title">{{ section.title }}</span>
  		</a>
  	</li>
  </ul>
</template>

<script>
export default {
	name: 'PageNavSections',
	props: ['sections'],
}
</script>

<style lang="scss" scoped>
.nav-section__item {
	font-family: $font-stack-mono;
	font-size: $fs-l;
}

.nav-section__link {
	display: flex;
	align-items: center;
	height: 2.5rem;
	padding: 0 $sp-l;
	color: primary-color(300);
	text-decoration: none;

	&:hover {
		.link-dot {
			@include size(1.25rem);
			opacity: 0.5;
			border-radius: $br-m;
			transition-duration: 0.2s;
		}

		.link-title {
			transform: translateX($sp-xxs);
		}
	}

	&.active {
		.link-dot {
			@include size(1.25rem);
			opacity: 1;
			background-color: $cyan;
			border-radius: $br-m;
			transform: none;
			transition: all 0.25s $ease-out-back;
		}

		.link-title {
			font-weight: bold;
			color: primary-color(100);
			transform: translateX($sp-s);
		}
	}
}

.link-title {
	transition: transform 0.2s $ease-in-out;
}

.link-dot__wrap {
	@include size(1.25rem);
	display: flex;
	margin-right: $sp-m;
}

.link-dot {
	@include circle(0.25rem);
	margin: auto;
	opacity: 0.2;
	background-color: primary-color(100);
	transform: rotate(-0.125turn);
	transition: all 0.25s $ease-in-out;
}
</style>
