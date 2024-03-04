<script setup>

defineProps({
    headers: Array,
    dates: Array,
});

</script>

<template>
    <div class="px-4 sm:px-6 lg:px-8">
        <div class="-mx-4 mt-8 overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:-mx-6 md:mx-0 md:rounded-lg">
            <table class="min-w-full divide-y divide-gray-300">
                <thead class="bg-gray-50">
                    <tr>
                        <th v-for="(header, index) in headers" :class="{
                            'py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6': index == 0,
                            'hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell': index == 1,
                            'hidden px-3 py-3.5 text-left text-sm font-semibold text-gray-900 sm:table-cell': index == 3 || index == 2,
                            'px-3 py-3.5 text-left text-sm font-semibold text-gray-900': header.text == 'Resultat',
                        
                        }">
                            {{ header.text }}
                        </th>
                    </tr>
                </thead>
                <tbody class="divide-y divide-gray-200 bg-white">
                    <tr v-for="{ cells } in dates">
                        <td
                            class="w-full max-w-0 py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:w-auto sm:max-w-none sm:pl-6">
                            {{ cells[0].text[0] }} {{ cells[0].text[1] }}
                            <dl class="font-normal lg:hidden">
                                <dd class="mt-1 truncate text-gray-700 sm:py-0 pb-1">
                                        <div>{{ cells[1].text[1] }}</div>
                                        <div>{{ cells[1].text[0] }}</div>
                                </dd>
                                <dd class="sm:hidden mt-1 truncate text-gray-700"><span
                                        :class="{ 'font-bold': cells[2].text[0] == 'UHC Basel United II' }">{{
                                            cells[2].text[0]
                                        }}</span></dd>
                                <dd class="sm:hidden mt-1 truncate text-gray-700"><span
                                        :class="{ 'font-bold': cells[3].text[0] == 'UHC Basel United II' }">{{
                                            cells[3].text[0]
                                        }}</span></dd>
                            </dl>
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 lg:table-cell">
                            <div>{{ cells[1].text[1] }}</div>
                            <div>{{ cells[1].text[0] }}</div>
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 sm:table-cell">
                            <span :class="{ 'font-bold': cells[2].text[0] == 'UHC Basel United II' }">{{
                                cells[2].text[0]
                            }}</span>
                        </td>
                        <td class="hidden px-3 py-4 text-sm text-gray-500 sm:table-cell">
                            <span :class="{ 'font-bold': cells[3].text[0] == 'UHC Basel United II' }">{{
                                cells[3].text[0]
                            }}</span>
                        </td>
                        <td class="px-3 py-4 text-sm text-gray-500">
                            <div v-if="cells[4].text[0].length > 0">{{
                                cells[4].text[0]
                            }}</div>
                            <div v-else>n.A</div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

