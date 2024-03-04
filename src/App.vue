<script setup>
import List from './components/List.vue';
import Ranking from './components/Ranking.vue';
</script>

<script>

const UNIHOCKEY_API_URL = `https://api-v2.swissunihockey.ch/api/games?mode=team&season=$season&team_id=428375`;
const TABLE_API_URL = `https://api-v2.swissunihockey.ch/api/rankings?league=5&season=$season&game_class=12&group=Gruppe%204`;
const SEASONS_API_URL = `https://api-v2.swissunihockey.ch/api/seasons?league=5`;
const CURRENT_SEASON = `https://api-v2.swissunihockey.ch/api/rankings?league=5`;

export default {
  data() {
    return {
      headers: ['header'],
      dates: null,
      ranking: null,
      page: null,
      pages: [1, 2],
      seasons: null,
      season: null,
      current_tab: "Matches"
    }
  },
  created() {
    // fetch on init
    this.initialFetch();
  },
  methods: {
    async initialFetch() {
      await this.fetchSeason();
      await this.fetchSeasons();
      await this.fetchRankings();
      await this.fetchUnihockeyData();
    },
    async fetchSeason() {
      let response = await (await fetch(CURRENT_SEASON)).json();
      this.season = response.data.context.season;
    },
    async fetchSeasons() {
      const all_seasons = await (await fetch(SEASONS_API_URL)).json();
      this.seasons = all_seasons.entries.slice(0, 5).map(season => season.text.split('/')[0]);
    },
    async fetchUnihockeyData() {
      let api = UNIHOCKEY_API_URL.replace('$season', this.season);
      const url = api + (this.page !== null ? `&page=${this.page}` : '');
      let response = await (await fetch(url)).json();
      this.dates = response.data.regions[0].rows;
      this.headers = response.data.headers;
      this.page = response.data.context.page;
      this.fetchRankings();
    },
    async fetchRankings() {
      let api = TABLE_API_URL.replace('$season', this.season);
      let response = await (await fetch(api)).json();
      this.ranking = response.data.regions;
    },
    selectTab(tab) {
      this.current_tab = tab;
    }
  },
  watch: {
    page(val, oldVal) {
      if (oldVal !== null);
      this.fetchUnihockeyData();
    },
    season(val, oldVal) {
      if (oldVal !== null) {
        this.season = val;
        this.page = 1;
        this.fetchUnihockeyData();
      }
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
            <div>
              <a v-on:click="selectTab('Matches')" type="button"
                class="cursor-pointer inline-flex items-center rounded-l bg-white py-2 text-base font-medium text-gray-700 hover:bg-red-50">
                <h1 class="text-xl sm:text-3xl border-r border-gray-400 px-4 leading-tight tracking-tight text-gray-900"
                  :class="{ 'font-bold': current_tab == 'Matches' }">
                  Matches
                </h1>
              </a>
              <a v-on:click="selectTab('Ranking')" type="button"
                class="cursor-pointer inline-flex items-center rounded-r bg-white px-4 py-2 text-base font-medium text-gray-700 hover:bg-red-50">
                <h1 class="text-xl sm:text-3xl leading-tight tracking-tight text-gray-900"
                  :class="{ 'font-bold': current_tab == 'Ranking' }">
                  Ranking
                </h1>
              </a>
            </div>
            <div class="flex flex-row space-x-4 items-center">
              <label for="season" class="block text-sm font-medium text-gray-700">Saison</label>
              <select v-model="season" id="season" name="season"
                class="block w-full rounded-md border-gray-300 py-2 pl-3 pr-10 text-base focus:border-red-500 focus:outline-none focus:ring-red-500 sm:text-sm">
                <option disabled value="">-</option>
                <template v-for="season in seasons">
                  <option :id="season" :value="season">
                    {{ season }}
                  </option>
                </template>
              </select>
            </div>
            <div v-if="current_tab == 'Matches'" class="flex flex-row space-x-4 items-center">
              <label for="page" class="block text-sm font-medium text-gray-700">Seite</label>
              <select v-model="page" id="page" name="page"
                class="block w-full rounded-md border-gray-300 py-2 pl-3 pr-10 text-base focus:border-red-500 focus:outline-none focus:ring-red-500 sm:text-sm">
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
      <List v-if="current_tab == 'Matches'" :dates="dates" :headers="headers" />
      <Ranking v-if="current_tab == 'Ranking'" :ranking="ranking" />
    </div>
  </div>
</template>