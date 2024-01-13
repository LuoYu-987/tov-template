<script setup lang="ts">
import { FilterOutline, ScanOutline, Close } from '@vicons/ionicons5'
import { appWindow } from '@tauri-apps/api/window'

const closeOptions = reactive([
	{
		label: '隐藏到托盘',
		key: 'hide',
	},
	{
		label: '退出',
		key: 'close',
	},
])
const handleSelect = (key: string | number) => {
	if (key == 'close') {
		appWindow.close()
	} else if (key == 'hide') {
		appWindow.hide()
	}
}
onMounted(() => {
	document
		.getElementById('titlebar-minimize')!
		.addEventListener('click', () => appWindow.minimize())
	document
		.getElementById('titlebar-maximize')!
		.addEventListener('click', () => appWindow.toggleMaximize())
})
</script>

<template>
	<div>
		<n-button id="titlebar-minimize" size="small" quaternary type="info">
			<template #icon>
				<n-icon><FilterOutline /></n-icon>
			</template>
		</n-button>
		<n-button id="titlebar-maximize" quaternary size="small" type="info">
			<template #icon>
				<n-icon><ScanOutline /></n-icon>
			</template>
		</n-button>

		<n-dropdown
			size="small"
			trigger="click"
			:options="closeOptions"
			@select="handleSelect"
		>
			<n-button quaternary size="small" type="info">
				<template #icon>
					<n-icon><Close /></n-icon>
				</template>
			</n-button>
		</n-dropdown>
	</div>
</template>
