<script setup>
import List from './components/List.vue'
</script>

<script>

const UNIHOCKEY_API_URL = `https://api-v2.swissunihockey.ch/api/games?mode=team&season=2022&team_id=428375`

export default {
  data() {
    return {
      headers: ['header'],
      dates: null,
      page: null,
      pages: [1, 2],
    }
  },
  created() {
    // fetch on init
    this.fetchUnihockeyData()
  },
  methods: {
    async fetchUnihockeyData() {
      const url = `${UNIHOCKEY_API_URL}` + (this.page !== null ? `&page=${this.page}` : '')
      let response = await (await fetch(url)).json()
      this.dates = response.data.regions[0].rows
      this.headers = response.data.headers
      this.page = response.data.context.page
    }
  },
  watch: {
    page(val, oldVal) {
      if (oldVal !== null)
        this.fetchUnihockeyData()
    }
  },
}
</script>

<template>
  <div class="min-h-full">
    <nav class="border-b border-gray-200 bg-white">
      <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <div class="flex h-16 justify-between">
          <div class="flex">
            <div class="flex flex-shrink-0 items-center">
              <img class="block h-8 w-auto lg:hidden" src="https://www.uhcbaselunited.ch/logo/logo.png"
                alt="Logo UHC Basel United">
              <img class="hidden h-8 w-auto lg:block" src="https://www.uhcbaselunited.ch/logo/logo.png"
                alt="Logo UHC Basel United">
            </div>
          </div>
        </div>
      </div>
    </nav>


    <div class="mx-auto max-w-7xl py-10">
      <header>
        <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
          <div class="flex flex-row justify-between">
            <h1 class="text-3xl font-bold leading-tight tracking-tight text-gray-900">Matches</h1>

            <div class="flex flex-row space-x-4 items-center">
              <label for="page" class="block text-sm font-medium text-gray-700">Seite</label>
              <select v-model="page" id="page" name="page"
                class="mt-1 block w-full rounded-md border-gray-300 py-2 pl-3 pr-10 text-base focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
                <option disabled value="">-</option>
                <template v-for="page in pages">
                  <option :id="page" :value="page">
                    {{ page }}
                  </option>
                </template>
              </select>
            </div>
          </div>

        </div>
      </header>

      <List :dates="dates" :headers="headers" />
    </div>
  </div>
</template>