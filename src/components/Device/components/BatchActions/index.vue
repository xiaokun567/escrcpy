<template>
  <Scrollable>
    <div class="flex items-center space-x-2">
      <component
        :is="item.component || 'div'"
        v-for="(item, index) in actionModel"
        :key="index"
        class="flex-none"
        v-bind="{
          devices,
          ...(item.command
            ? {
              onClick: () => handleShell(item),
            }
            : {}),
        }"
      >
        <template #default="{ loading = false } = {}">
          <el-button
            plain
            :title="$t(item.tips || item.label)"
            :loading="loading"
          >
            <template #icon>
              <svg-icon
                v-if="item.svgIcon"
                :name="item.svgIcon"
                :class="item.iconClass"
              ></svg-icon>
              <el-icon v-else-if="item.elIcon" :class="item.iconClass">
                <component :is="item.elIcon" />
              </el-icon>
            </template>
            {{ $t('common.batch') }}-{{ $t(item.label) }}
          </el-button>
        </template>
      </component>
    </div>
  </Scrollable>
</template>

<script setup>
import Application from './Application/index.vue'
import FilePush from './FilePush/index.vue'
import Screenshot from './Screenshot/index.vue'
import Shell from './Shell/index.vue'
import Tasks from './Tasks/index.vue'

const props = defineProps({
  devices: {
    type: Array,
    default: () => [],
  },
})

const actionModel = [
  {
    label: 'device.control.capture',
    elIcon: 'Crop',
    component: Screenshot,
  },
  {
    label: 'device.control.install',
    svgIcon: 'install',
    component: Application,
  },
  {
    label: 'device.control.file.push',
    svgIcon: 'file-send',
    component: FilePush,
  },
  {
    label: 'device.control.shell.name',
    svgIcon: 'command',
    component: Shell,
  },
  {
    label: 'device.task.name',
    elIcon: 'Clock',
    component: Tasks,
  },
]
</script>

<style></style>
