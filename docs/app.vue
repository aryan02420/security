<script setup>
useServerSeoMeta({
  ogSiteName: 'Nuxt Security',
  twitterCard: 'summary_large_image',
})
useHead({
  htmlAttrs: {
    lang: 'en',
  },
})
const links = [
  {
    label: 'Documentation',
    to: '/getting-started/installation',
  },
  {
    label: 'Playground',
    to: '/playground',
  },
  {
    label: 'Releases',
    to: 'https://github.com/Baroshem/nuxt-security/releases',
    target: '_blank',
  },
]
const { data: files } = useLazyFetch('/api/search.json', {
  default: () => [],
  server: false,
})
const { data: navigation } = await useAsyncData('navigation', () =>
  fetchContentNavigation(),
)

// Provide
provide('navigation', navigation)
</script>

<template>
  <UHeader :links="links">
    <template #logo>
      <Logo />
    </template>

    <template #right>
      <UColorModeButton v-if="!$colorMode.forced" />
      <UButton
        aria-label="Nuxt Website"
        icon="i-simple-icons-nuxtdotjs"
        to="https://nuxt.com"
        target="_blank"
        color="gray"
        variant="ghost"
      />
      <UButton
        aria-label="Nuxt on X"
        icon="i-simple-icons-x"
        to="https://x.com/nuxt_js"
        target="_blank"
        color="gray"
        variant="ghost"
      />
      <UButton
        aria-label="Nuxt Security on GitHub"
        icon="i-simple-icons-github"
        to="https://github.com/Baroshem/nuxt-security"
        target="_blank"
        color="gray"
        variant="ghost"
      />
    </template>
    <!-- Mobile panel -->
    <template
      v-if="$route.path !== '/'"
      #panel
    >
      <LazyUDocsSearchButton
        size="md"
        class="mb-4 w-full"
      />
      <LazyUNavigationTree
        :links="mapContentNavigation(navigation)"
        default-open
        :multiple="false"
      />
    </template>
  </UHeader>

  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>

  <UFooter :links="links">
    <template #left>
      <span class="text-sm">
        Published under
        <NuxtLink
          to="https://github.com/Baroshem/nuxt-security"
          target="_blank"
          class="underline"
        >MIT License</NuxtLink>
      </span>
    </template>
    <template #right>
      <UColorModeButton v-if="!$colorMode.forced" />
      <UButton
        aria-label="Nuxt Website"
        icon="i-simple-icons-nuxtdotjs"
        to="https://nuxt.com"
        target="_blank"
        color="gray"
        variant="ghost"
      />
      <UButton
        aria-label="Nuxt on X"
        icon="i-simple-icons-x"
        to="https://x.com/nuxt_js"
        target="_blank"
        color="gray"
        variant="ghost"
      />
      <UButton
        aria-label="Nuxt Security on GitHub"
        icon="i-simple-icons-github"
        to="https://github.com/Baroshem/nuxt-security"
        target="_blank"
        color="gray"
        variant="ghost"
      />
    </template>
  </UFooter>
  <ClientOnly>
    <LazyUDocsSearch
      :files="files"
      :navigation="navigation"
      :links="links"
    />
  </ClientOnly>
</template>
