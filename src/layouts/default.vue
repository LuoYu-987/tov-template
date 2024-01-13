<template>
	<n-config-provider :theme="theme">
		<Navigation @changeNaiveTheme="changeNaiveTheme" />
		<div class="w-screen flex flex-col items-center justify-center">
			<router-view v-slot="{ Component }">
				<transition name="fade" mode="out-in">
					<component :is="Component" />
				</transition>
			</router-view>
		</div>
	</n-config-provider>
</template>

<script setup lang="ts">
import { darkTheme } from 'naive-ui'
import type { GlobalTheme } from 'naive-ui'
/**
 * 整合naive-ui的主题
 */
const theme = ref<GlobalTheme | null>(null)
const changeNaiveTheme = (flag: boolean = false) => {
	if (flag) {
		theme.value = darkTheme
	} else {
		theme.value = null
	}
}
</script>

<style>
.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.25s ease;
}

.fade-enter-from,
.fade-leave-to {
	opacity: 0;
}
</style>
