<script setup lang="ts">
import { getRoutes } from '@/plugins/router'
import { SwitchIcon } from 'vue-dark-switch'

const { te, t } = useI18n()

const routes = getRoutes()
	.filter((r: { path: string | string[] }) => !r.path.includes('notFound'))
	.map((r: { path: any; name: any }) => {
		let { path, name } = r
		if (path === safeResolve('/')) {
			return { path, name: 'home' }
		}

		if (!name) {
			name = path
		}

		return { path, name: name.toString().slice(1).replaceAll('/', ' · ') }
	})
const changeNaiveThemeFlag = ref(false)
const emit = defineEmits(['changeNaiveTheme'])
function changeTheme() {
	changeNaiveThemeFlag.value = !changeNaiveThemeFlag.value
	emit('changeNaiveTheme', changeNaiveThemeFlag.value)
}
</script>

<template>
	<nav
		data-tauri-drag-region
		aria-label="Site Nav"
		class="mx-auto h-40px flex items-center justify-between pl-2"
		style="border-bottom: 1px solid #767472"
	>
		<div class="flex items-center justify-center space-x-5">
			<SwitchIcon @click="changeTheme" unmount-persets />
		</div>

		<ul class="flex items-center gap-2 text-sm font-medium">
			<li v-for="r of routes" :key="r.path" class="hidden !block">
				<RouterLink class="rounded-lg px-3 py-2" :to="r.path">
					{{ te(r.name) ? t(r.name) : r.name }}
				</RouterLink>
			</li>

			<li class="hidden !block">
				<Dropdown />
			</li>
			<li>
				<WindowBtn></WindowBtn>
			</li>
		</ul>
	</nav>
</template>
