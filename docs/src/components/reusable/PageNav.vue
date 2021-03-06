<template>
	<div class="page-nav__wrap" :class="{ open }">
		<FocusLock :disabled="isMediaLarge || !open">
			<XyzTransition appear xyz="fade delay-4">
				<button class="nav-button" @click="toggle(!open)">
					<div class="logo-wrap">
						<AnimXyzLogo></AnimXyzLogo>
					</div>
					<span class="nav-button__text logo-text">AnimXYZ</span>
					<span class="nav-button__text toggle-text">{{ open ? 'Close' : 'Menu' }}</span>
				</button>
			</XyzTransition>

			<XyzTransition
				appear
				duration="auto"
				xyz="ease-in-out duration-3"
				v-xyz="{ 'left-100%': $mq.above('tablet'), 'down-100%': $mq.below('tablet') }"
			>
				<nav class="page-nav" v-show="open">
					<div class="nav-list__wrap" v-scroll-lock="$mq.below('tablet') && open">
						<ul class="nav-list" xyz="fade left-3 stagger-0.5">
							<li class="nav-item xyz-in-nested" :style="{ '--xyz-index': 0 }" key="home">
								<a class="nav-item__link link-home" href="/">
									<div class="link-dot__wrap">
										<span class="link-arrow">←</span>
									</div>
									<span class="link-title"> Splash Page</span>
								</a>
							</li>
							<li
								v-for="(section, index) in sections"
								class="nav-item xyz-in-nested"
								@click="onSectionClick"
								:style="{ '--xyz-index': index + 1 }"
								:key="section.id"
							>
								<h2 class="nav-item__header" v-if="section.header">{{ section.title }}</h2>

								<a
									class="nav-item__link"
									:class="{ active: section === activeSection }"
									v-if="!section.header"
									:href="`#${section.id}`"
									:ref="section === activeSection && 'activeLink'"
								>
									<div class="link-dot__wrap">
										<span class="link-dot"></span>
									</div>
									<span class="link-title">{{ section.title }}</span>
								</a>
							</li>
						</ul>
					</div>
					<div class="nav-extras" xyz="fade delay-3 small ease-out-back">
						<a class="github-link xyz-in-nested" href="https://github.com/ingram-projects/animxyz" target="_blank">
							<IconGithub></IconGithub>
							<span>GitHub</span>
						</a>
						<DarkModeToggle class="xyz-in-nested"></DarkModeToggle>
					</div>
				</nav>
			</XyzTransition>
		</FocusLock>
	</div>
</template>

<script>
import FocusLock from 'vue-focus-lock'
import AnimXyzLogo from '~/components/reusable/AnimXyzLogo'
import DarkModeToggle from '~/components/reusable/DarkModeToggle'

export default {
	name: 'PageNav',
	props: {
		open: Boolean,
		sections: Array,
		activeSection: Object,
	},
	components: {
		AnimXyzLogo,
		DarkModeToggle,
		FocusLock,
	},
	computed: {
		isMediaLarge() {
			return this.$mq.above('large')
		},
	},
	watch: {
		isMediaLarge: {
			immediate: true,
			handler() {
				if (this.isMediaLarge) {
					this.toggle(true)
				} else {
					this.toggle(false)
				}
			},
		},
		activeSection: {
			immediate: true,
			handler() {
				if (this.activeSection) {
					this.$nextTick(() => {
						if (this.$refs.activeLink) {
							this.$refs.activeLink[0].scrollIntoView({
								block: 'center',
								behavior: 'smooth',
							})
						}
					})
				}
			},
		},
	},
	methods: {
		toggle(toggled) {
			this.$emit('toggle', toggled)
		},
		onSectionClick() {
			this.toggle(false)
		},
	},
}
</script>

<style lang="scss" scoped>
.page-nav__wrap:not(.open) {
	.animxyz-logo ::v-deep {
		.side--red {
			transform: rotateY(0deg) translateZ($sp-xs);
		}

		.side--yellow {
			transform: rotateY(0deg);
		}

		.side--green {
			transform: translateZ(-$sp-xs);
		}

		.logo-sides {
			transform: rotateX(65deg) rotateZ(45deg);
		}
	}
}

.page-nav {
	position: fixed;
	display: flex;
	flex-direction: column;
	width: $desktop-menu-width;
	top: 0;
	bottom: 0;
	background-color: primary-color(900, 0.95);
	z-index: 3;

	@include media('<tablet') {
		left: 0;
		right: 0;
		width: auto;
		backdrop-filter: blur(4px);
	}
}

.nav-list__wrap {
	display: flex;
	margin-top: 5rem;
	flex-grow: 1;
	overflow-y: auto;

	@include media('<laptop') {
		margin-top: 0;
		margin-bottom: 5.5rem;
		order: 2;
	}

	@include media('<tablet') {
		display: block;
		margin-bottom: 0;
		padding-bottom: 2rem;
	}
}

.nav-list {
	width: 100%;
	margin: auto 0;
	list-style: none;

	@include media('<tablet') {
		margin: 0;
	}
}

.nav-item__header {
	color: primary-color(200);
	font-size: $fs-m;
	font-family: $font-stack-mono;
	text-transform: uppercase;
	letter-spacing: 0.05em;
	padding: 0 $sp-l;
	margin-top: $sp-s;
	margin-bottom: $sp-xxs;
}

.nav-item {
	font-family: $font-stack-mono;
	font-size: 1.125rem;
}

.nav-item__link {
	display: flex;
	align-items: center;
	height: 2.25rem;
	padding: 0 $sp-l;
	color: primary-color(300);
	text-decoration: none;

	&:hover,
	&:focus {
		outline: none;
		color: primary-color(200);

		.link-dot {
			@include size(1.25rem);
			opacity: 0.5;
			border-radius: $br-m;
			transition-duration: 0.2s;
		}

		.link-arrow {
			transform: translateX(-0.5rem);
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

	.link-home & {
		transform: none !important;
	}
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

.link-arrow {
	font-size: 1.5rem;
	line-height: 1.25rem;
	transition: all 0.25s $ease-in-out;
}

.nav-button {
	display: flex;
	align-items: center;
	position: fixed;
	top: $sp-m;
	left: $sp-m;
	z-index: 4;

	&:hover,
	&:focus {
		.nav-button__text {
			transform: translateX($sp-xxxs);
			opacity: 1;
		}

		.animxyz-logo {
			--logo-scale: 1.125;
			transform: scale(var(--logo-scale));

			@include media('<tablet') {
				--logo-scale: 1;
			}
		}
	}

	@include media('<laptop') {
		left: $sp-m;
		right: initial;
		top: initial;
		bottom: $sp-m;
	}

	@include media('<tablet') {
		left: initial;
		right: $sp-m;
		top: initial;
		bottom: $sp-m;
	}

	@include media('>=large') {
		pointer-events: none;
	}
}

.logo-wrap {
	margin-right: $sp-xxs;

	@include media('<tablet') {
		@include size(initial);
		margin: 0;
	}
}

.nav-button__text {
	font-family: $font-stack-mono;
	font-size: $fs-xl;
	font-weight: bold;
	margin-left: $sp-xs;
	opacity: 0.85;
	transition: color 0.2s $ease-in-out, opacity 0.2s $ease-in-out, transform 0.3s $ease-out-back;

	@include media('<tablet') {
		display: none;
	}
}

.logo-text {
	color: primary-color(50);

	@include media('<large') {
		display: none;
	}
}

.toggle-text {
	color: primary-color(800);

	@include dark-mode {
		color: primary-color(200);
	}

	.open & {
		color: primary-color(50);
	}

	.tab--examples & {
		@include media('<laptop') {
			color: primary-color(300);
		}
	}

	@include media('>=large') {
		display: none;
	}
}

.nav-extras {
	display: flex;
	align-items: center;
	margin: $sp-s;
	flex-shrink: 0;

	@include media('<laptop') {
		order: 1;
	}
}

.dark-mode-toggle {
	margin-left: $sp-s;
}

.github-link {
	--icon-color: #{primary-color(200)};
	height: 3rem;
	border-radius: $br-l;
	padding: 0 $sp-s;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-grow: 1;
	z-index: 3;
	background-color: primary-color(500, 0.2);
	color: var(--icon-color);
	text-decoration: none;
	transition: 0.2s $ease-in-out;
	transition-property: background-color, box-shadow;

	svg {
		@include size(1.5rem);
		transition: transform 0.3s $ease-out-back;
		margin-right: $sp-xs;
	}

	&:hover,
	&:focus {
		--icon-color: #{primary-color(50)};
		outline: none;
		background-color: primary-color(500, 0.3);

		svg {
			transform: scale(1.15);
		}
	}

	&:focus {
		box-shadow: 0 0 0 4px primary-color(200, 0.5);
	}
}
</style>
