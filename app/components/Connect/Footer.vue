<!-- This is temporary until pricelist gets implemented and finalized -->
<script setup lang="ts">
const uiVersion = useRuntimeConfig().public.version
const ac = useAppConfig().connect.core.footer
const localePath = useLocalePath()
const links = [
  {
    label: 'ConnectFooter.home',
    to: localePath('/')
  },
  {
    label: 'ConnectFooter.releaseNotes',
    to: 'https://www.release-notes.bcregistry.gov.bc.ca',
    target: '_blank'
  },
  {
    label: 'ConnectFooter.disclaimer',
    to: 'https://www2.gov.bc.ca/gov/content/home/disclaimer',
    target: '_blank'
  },
  {
    label: 'ConnectFooter.privacy',
    to: 'https://www2.gov.bc.ca/gov/content/home/privacy',
    target: '_blank'
  },
  {
    label: 'ConnectFooter.ally',
    to: 'https://www2.gov.bc.ca/gov/content/home/accessibility',
    target: '_blank'
  },
  {
    label: 'ConnectFooter.copyright',
    to: 'https://www2.gov.bc.ca/gov/content/home/copyright',
    target: '_blank'
  }
]

const appVersions = computed<string[]>(() => {
  const items = [...ac.versions]

  items.unshift(uiVersion)

  return items
})
</script>

<template>
  <footer
    id="connect-main-footer"
    data-testid="connect-main-footer"
    class="border-t-2 border-bcGovColor-navDivider bg-bcGovColor-footer dark:border-t dark:bg-bcGovColor-darkGray"
  >
    <div class="mx-auto flex max-w-bcGovLg items-center justify-between p-2">
      <nav :aria-label="$t('ConnectFooter.navLabel')" class="flex grow">
        <ul class="list-none flex-col gap-1 p-0 sm:-ml-2 sm:flex-row sm:flex-wrap">
          <li
            v-for="link in links"
            :key="link.to"
            class="flex-col gap-2 border-r-0 pr-2 last:mr-0 last:border-r-0 sm:mr-2 sm:inline-block sm:flex-none sm:border-r sm:first:ml-2 border-blue-100"
          >
            <NuxtLink
              :to="link.to === '/' ? `/${$i18n.locale}` : link.to"
              :target="link.target"
              class="rounded p-1 text-sm text-white hover:underline focus:outline-none focus-visible:ring-2 focus-visible:ring-white"
            >
              {{ $t(link.label) }}
            </NuxtLink>
          </li>
        </ul>
      </nav>
      <div class="-mb-1 flex items-center">
        <span class="italic text-bcGovColor-navDivider">{{ $t('ConnectFooter.bcApp') }}</span>
        <UTooltip arrow :ui="{ content: 'h-fit' }">
          <UButton :aria-label="$t('btn.appVersion')" color="white" icon="i-mdi-info-outline" />

          <template #content>
            <div class="flex flex-col">
              <span v-for="(item, i) in appVersions" :key="i">{{ item }}</span>
            </div>
          </template>
        </UTooltip>
      </div>
    </div>
  </footer>
</template>
