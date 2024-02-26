<script setup lang="ts">
const route = useRoute()
const appConfig = useAppConfig()
const { isHelpSlideoverOpen } = useDashboard()

const links = [{
  id: 'home',
  label: 'Search',
  icon: 'i-heroicons-magnifying-glass',
  to: '/',
  tooltip: {
    text: 'Search',
    shortcuts: ['G', 'H']
  }
}, {
  id: 'chat',
  label: 'Chat',
  icon: 'i-heroicons-chat-bubble-bottom-center-text',
  to: '/chat',
  tooltip: {
    text: 'Inbox',
    shortcuts: ['Alt', 'C']
  }
}, {
  id: 'docs',
  label: 'Ask Docs',
  icon: 'i-heroicons-document',
  to: '/docs',
  tooltip: {
    text: 'Docs',
    shortcuts: ['Alt', 'D']
  }
}, {
  id: 'translate',
  label: 'Translate',
  icon: 'i-heroicons-language',
  to: '/translate',
  tooltip: {
    text: 'Translate',
    shortcuts: ['Alt', 'T']
  }
}, {
  id: 'summarize',
  label: 'Summarize',
  icon: 'i-heroicons-funnel',
  to: '/summarize',
  tooltip: {
    text: 'Summarize',
    shortcuts: ['Alt', 'S']
  }
}, {
  id: 'discover',
  label: 'Discover',
  icon: 'i-heroicons-cube-transparent',
  to: '/discover',
  tooltip: {
    text: 'Discover',
    shortcuts: ['Alt', 'D']
  }
}]

const footerLinks = [{
  label: 'Invite people',
  icon: 'i-heroicons-plus',
  to: '/settings/members'
}, {
  label: 'Help & Support',
  icon: 'i-heroicons-question-mark-circle',
  click: () => isHelpSlideoverOpen.value = true
}]

const groups = [{
  key: 'links',
  label: 'Go to',
  commands: links.map(link => ({ ...link, shortcuts: link.tooltip?.shortcuts }))
}, {
  key: 'code',
  label: 'Code',
  commands: [{
    id: 'source',
    label: 'View page source',
    icon: 'i-simple-icons-github',
    click: () => {
      window.open(`https://github.com/nuxt-ui-pro/dashboard/blob/main/pages${route.path === '/' ? '/index' : route.path}.vue`, '_blank')
    }
  }]
}]

const threads = [
  {
    label: 'How to Make Homemade Pizza',
    to: '/homemade-pizza'
  },
  {
    label: 'The Basics of Astrophysics',
    to: '/astrophysics-basics'
  },
  {
    label: 'Learning French: Where to Start',
    to: '/learn-french'
  },
  {
    label: 'DIY Home Gardening Tips',
    to: '/home-gardening'
  },
  {
    label: 'Understanding Artificial Intelligence',
    to: '/ai-understanding'
  },
  {
    label: 'Exploring the Great Barrier Reef',
    to: '/great-barrier-reef'
  },
  {
    label: 'The History of Japanese Samurai',
    to: '/japanese-samurai-history'
  },
  {
    label: 'Creating Your First Mobile App',
    to: '/first-mobile-app'
  },
  {
    label: 'Effective Time Management Strategies',
    to: '/time-management-strategies'
  },
  {
    label: 'Introduction to Meditation',
    to: '/meditation-introduction'
  }
];


const defaultColors = ref(['green', 'teal', 'cyan', 'sky', 'blue', 'indigo', 'violet'].map(color => ({ label: color, chip: color, click: () => appConfig.ui.primary = color })))
const colors = computed(() => defaultColors.value.map(color => ({ ...color, active: appConfig.ui.primary === color.label })))
</script>

<template>
  <UDashboardLayout>
    <UDashboardPanel :width="250" :resizable="{ min: 200, max: 300 }" collapsible>
      <UDashboardNavbar class="!border-transparent" :ui="{ left: 'flex-1' }">
        <template #left>
          <div class="text-center text-xl font-bold flex flex-row items-center gap-2">
        <img class="block w-8 mx-auto dark:hidden" src="/execoLogo.png" alt="Execo" />
        <img class="hidden w-8 mx-auto dark:block" src="/execoLogoLight.png" alt="Execo" />
        <h2>Execo</h2></div>
        </template>
      </UDashboardNavbar>

      <UDashboardSidebar>
        <template #header>
          <UButton icon="i-heroicons-plus-circle" size="md" color="primary" variant="solid" label="Create New Thread"
            :trailing="false" block />
        </template>

        <UDashboardSidebarLinks :links="links" />

        <UDivider />
        <h2>Recent Threads</h2>
        <div>
        <UVerticalNavigation :links="threads" :ui="{
          wrapper: 'border-s border-gray-200 dark:border-gray-800 space-y-2 overflow-hidden truncate	',
          base: 'group block border-s -ms-px leading-6 before:hidden mb-2',
          padding: 'p-0 ps-4',
          rounded: '',
          font: 'text-ellipsis',
          ring: '',
          active: 'text-primary-500 dark:text-primary-400 border-current font-semibold',
          inactive: 'border-transparent hover:border-gray-400 dark:hover:border-gray-500 text-gray-700 hover:text-gray-900 dark:text-gray-400 dark:hover:text-gray-300'
        }" /></div>

        <!-- <UDashboardSidebarLinks :links="[{ label: 'Colors', draggable: true, children: colors }]"
          @update:links="colors => defaultColors = colors" /> -->

        <div class="flex-1" />

        

        <UDivider class="sticky bottom-0" />
        <UDashboardSidebarLinks :links="footerLinks" />
        <template #footer>
          <!-- ~/components/UserDropdown.vue -->
          
          <UserDropdown />
          
        </template>
      </UDashboardSidebar>
    </UDashboardPanel>

    <slot />

    <!-- ~/components/HelpSlideover.vue -->
    <HelpSlideover />
    <!-- ~/components/NotificationsSlideover.vue -->
    <NotificationsSlideover />

    <ClientOnly>
      <LazyUDashboardSearch :groups="groups" />
    </ClientOnly>
  </UDashboardLayout>
</template>
