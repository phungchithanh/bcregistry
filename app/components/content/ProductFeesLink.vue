<template>
  <a
    :href="productFeesURL"
    target="_blank"
    class="prose">
    Learn more about applicable product fees
  </a>
</template>

<script lang="ts" setup>
import { useRuntimeConfig } from '#app'

const runtimeConfig = useRuntimeConfig()

const productFeesURL = `${runtimeConfig.public.productFeesURL}`
</script>

<style scoped>
.prose{
  color: var(--color-bcGovColor-markBlue);
  text-decoration: underline;
  font-weight: 900;
}
</style>
