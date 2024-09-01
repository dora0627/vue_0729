<script setup lang="ts">
import { ref } from 'vue'
</script>
<template>
    <v-app>
        <v-main>
            <div class="button-bar">
                <v-btn color="primary">Button 1</v-btn>
                <v-btn color="secondary">Button 2</v-btn>
                <v-btn color="success">Button 3</v-btn>
            </div>
        </v-main>
    </v-app>
</template>

<script>
export default {
  name: 'ButtonBar'
}
</script>

<style scoped>
.button-bar {
  display: flex;
  justify-content: space-around;
  padding: 16px;
}
</style>