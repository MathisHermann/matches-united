<script setup>

defineProps({
    pages: Array,
    page: Number,
});

</script>

<template>
    {{ page }}
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
</template>