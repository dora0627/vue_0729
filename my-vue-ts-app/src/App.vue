<template>
  <v-app>
    <v-container>
      <!-- 選單區塊 -->
      <v-row no-gutters>
        <v-col cols="6">
          <Permission_practice v-model="selected"></Permission_practice>
        </v-col>
      </v-row>
      <!-- 內容區塊 -->
      <v-row no-gutters>
        <v-col cols="6">
          <v-card v-if="selected === 'Teacher'">
            <v-card-title>Teacher</v-card-title>
            <v-card-text>
              <v-checkbox v-model="checked" label="Check me"></v-checkbox>
            </v-card-text>
          </v-card>
          <v-card v-else>
            <v-card-title>Student</v-card-title>
            <v-card-text>
              Sorry, you don't have permission to view this content.
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>

      <!-- 固定顯示 Network Status 到左下角 -->
      <v-card class="network-status">
        <v-card-title>Network
          <v-icon>{{ networkStatus === '連線' ? 'mdi-wifi' : 'mdi-wifi-off' }}</v-icon>
        </v-card-title>
        
        <v-card-text>
          {{ networkStatus }}
        </v-card-text>
      </v-card>
    </v-container>
  </v-app>
</template>

<script lang="ts">
import Permission_practice from './components/Permission_practice.vue'
import { onMounted, onBeforeUnmount, ref } from 'vue'

export default {
  components: {
    Permission_practice
  },
  setup() {
    const selected = ref('')
    const checked = ref(false)
    
    const networkStatus = ref('正在檢查...')
    const checkNetworkStatus = async () => {
      try {
        const response = await fetch('www.google.com', { mode: 'no-cors' })
        networkStatus.value = response.ok ? '連線' : '離線'
      } catch {
        networkStatus.value = '離線'
      }
    }
    const updateNetworkStatus = () => {
      networkStatus.value = navigator.onLine ? '連線' : '離線'
      if (networkStatus.value === '連線') {
        window.location.reload()
      } else {
        console.log('離線')
      }
    }

    onMounted(() => {
      checkNetworkStatus()
      window.addEventListener('online', updateNetworkStatus)
      window.addEventListener('offline', updateNetworkStatus)
    })

    onBeforeUnmount(() => {
      window.removeEventListener('online', updateNetworkStatus)
      window.removeEventListener('offline', updateNetworkStatus)
    })

    return {
      networkStatus,
      selected,
      checked
    }
  },
}
</script>

<style>
@import '@mdi/font/css/materialdesignicons.css';

/* Network Status 固定在左下角 */
.network-status {
  position: fixed;
  bottom: -800px;
  left: 0px;
  width: 200px;
}
</style>
