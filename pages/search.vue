<template>
  <UDashboardPage>
    <UDashboardPanel grow>
      <UDashboardNavbar title="Search">
        <template #right>
          <UTooltip text="Notifications" :shortcuts="['N']">
            <UButton color="gray" variant="ghost" square @click="isNotificationsSlideoverOpen = true">
              <UChip color="red" inset>
                <UIcon name="i-heroicons-bell" class="w-5 h-5" />
              </UChip>
            </UButton>
          </UTooltip>
        </template>
        <UDropdown :items="items">
          <UButton icon="i-heroicons-plus" size="md" class="ml-1.5 rounded-full" />
        </UDropdown>
      </UDashboardNavbar>
      <div
        class="relative overflow-x-scroll flex min-h-screen flex-col justify-center overflow-hidden bg-gray-50 py-6 sm:py-12">
        <div
          class="lg:my-4 pt-50 absolute inset-0 bg-[url(/grid.svg)] bg-center [mask-image:linear-gradient(180deg,white,rgba(255,255,255,0))]">
        </div>
        <h2 class=" text-3xl mb-4 mx-auto">💡 Knowledge Brings Light</h2>
        <div class="relative mx-4 w-full bg-white shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:max-w-lg sm:rounded-lg">
          <form class=" max-w-full">
            <div class="group relative bg-white p-4 rounded-xl border border-gray-200">
              <UTextarea :padded="false" :rows="3" :maxrows="5" placeholder="Ask any question..." size="2xl"
                variant="none" class="w-full text-xl focus:text-blue-900" />
              <div class="flex items-center gap-2 align-center">
                <USelectMenu v-model="selectedLocations" icon="i-heroicons-funnel" placeholder="Focus" mode="hover"
                  :options="defaultLocations" multiple />
                <div class="flex items-center">
                  <UToggle on-icon="i-heroicons-globe-alt" off-icon="i-heroicons-document-chart-bar" v-model="withFiles"
                    class="mr-2" />
                  Web
                </div>
                <UButton type="submit" color="black" icon="i-heroicons-paper-airplane"
                  class="absolute bottom-2.5 right-3.5" />
              </div>
            </div>
          </form>
          
        </div>
        <div class="mx-auto mt-10 max-w-xl">
              <ul role="list" class="mt-4 flex flex-wrap gap-2 content-start justify-center">
                <li v-for="( questions ) in  questions " :key="questionIdx">
                  <button type="button">
                  <span class="inline-flex items-center rounded-md bg-gray-50 px-2 py-1 text-xs font-medium text-gray-600 ring-1 ring-inset ring-gray-500/10 question-btn">{{ questions.name }}</span>
                </button>
                </li>
              </ul>
            </div>
      </div>
      
    </UDashboardPanel>
  </UDashboardPage>
</template>

<script setup>

const questions = [
  {
    name: "🌍 What is the largest country in the world by land area?", // Geography
  },
  {
    name: "🔬 What is the smallest particle in the universe?", // Physics/Science
  },
  {
    name: "🤔 What is the meaning of life?", // Philosophy
  },
  {
    name: "🚀 Who was the first person to walk on the moon?", // Space exploration/History
  },
  {
    name: "🧮 What is the square root of 144?", // Mathematics
  },
  {
    name: "🎨 What are the primary colors?", // Art/Design
  },
  {
    name: "🏛️ What is the capital of France?", // Geography
  },
  {
    name: "🧬 What is the process of DNA replication called?", // Biology
  },
  {
    name: "🏟️ When were the first Olympic Games held?", // History/Sports
  },
  {
    name: "📚 Who wrote the play Hamlet?", // Literature
  },
];


const items = [
  [{
    label: 'Profile',
    avatar: {
      src: 'https://avatars.githubusercontent.com/u/739984?v=4'
    }
  }]
]





</script>