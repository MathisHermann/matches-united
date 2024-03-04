<script setup>

defineProps({
    ranking: Array,
});

</script>

<template>
    <div class="px-4 sm:px-6 lg:px-8">
        <div class="-mx-4 mt-8 overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:-mx-6 md:mx-0 md:rounded-lg">
            <table class="min-w-full divide-y divide-gray-300">
                <thead class="bg-gray-50">
                    <tr> 
                        <th scope="col"
                            class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6 lg:table-cell">
                            Rang</th>
                        <th scope="col"
                            class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell">Team
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell">Sp
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell">SoW
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 sm:table-cell">S
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 sm:table-cell">U
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 sm:table-cell">N
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 sm:table-cell">T
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell">TD
                        </th>
                        <th scope="col"
                            class="hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell">PQ
                        </th>
                        <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell">
                            P
                        </th>

                    </tr>
                </thead>
                <tbody class="divide-y divide-gray-200 bg-white">
                    <tr v-for=" item in ranking[0].rows">
                        <td
                            class=" max-w-0 py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:w-auto sm:max-w-none sm:pl-6">
                            {{ item.cells[0].text[0] }}
                        </td>
                        <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm sm:pl-6 lg:table-cell">
                            <div class="flex flex-col lg:flex-row items-left lg:items-center">
                                <div class="h-10 w-10 flex-shrink-0 mr-4">
                                    <img class="h-10 w-10 rounded-full" :src="item.cells[1].image.url"
                                        alt="Logo">
                                </div>
                                <div class="">
                                    <div class="font-medium text-gray-900">{{ item.cells[2].text[0] }}</div>
                                </div>
                            </div>
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 lg:table-cell">{{ item.cells[3].text[0] }}
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 lg:table-cell">{{ item.cells[4].text[0] }}
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 sm:table-cell">{{ item.cells[5].text[0] }}
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 sm:table-cell">{{ item.cells[6].text[0] }}
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 sm:table-cell">{{ item.cells[7].text[0] }}
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 sm:table-cell">{{ item.cells[8].text[0] }}
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 lg:table-cell">{{ item.cells[9].text[0] }}
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 lg:table-cell">{{ item.cells[10].text[0] }}
                        </td>
                        <td class="px-3 py-4 text-sm text-gray-500 table-cell font-bold">{{ item.cells[11].text[0] }}</td>
                    </tr>

                </tbody>
            </table>
        </div>
    </div>
</template>

