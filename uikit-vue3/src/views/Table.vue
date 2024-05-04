<template>
    <h1 class="heading-1">Table</h1>
    <span>Sort field: {{ sortField }}</span><br/>
    <span>Type sort: {{ typeSort }}</span>
    <base-table
        :head="tableHeads"
        :columnTemplate="tableSizeColumns"
        @sort="setSort"
    >
        <table-row
            v-for="book in booksSorting" 
            :key="book.id" 
            :columnTemplate="tableSizeColumns"
            :bgRow="book.bg"
        >
            <table-column :columnTitle="tableHeads[0]">
                {{ book.id }}
            </table-column>
            <table-column :columnTitle="tableHeads[1]">
                {{ book.author }}
            </table-column>
            <table-column :columnTitle="tableHeads[2]">
                {{ book.title }}
            </table-column>
            <table-column :image="true" :srcImage="book.image" />
            <table-column>
                <Button lable="Читать Онлайн"></Button>
            </table-column>
        </table-row>
    </base-table>
</template>

<script setup>
import BaseTable from '../components/Table/BaseTable.vue';
import TableRow from '../components/Table/TableRow.vue';
import TableColumn from '../components/Table/TableColumn.vue';
import Button from '../components/Button.vue'
import { ref, computed } from 'vue'

const tableHeads = ['Id', 'Author', 'Title', 'Cover', '']
const tableSizeColumns = '50px 1fr 2fr 150px 140px'

const sortField = ref('id')
const typeSort = ref('desc')

const books = ref([
  {
    id: 1,
    author: 'Dmitry Glukhovsky',
    title: 'Metro 2033',
    image: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T2/images/I/81pNKLAG-cL._AC_UY436_FMwebp_QL65_.jpg',
    bg: '#FFA26B'
  },
  {
    id: 12,
    author: 'James Clear',
    title: 'Atomic Habits: An Easy',
    image: 'https://m.media-amazon.com/images/P/0735211299.01._SCLZZZZZZZ_SX500_.jpg',
    bg: '#00C48C'
  },
  {
    id: 2,
    author: 'J. K. Rowling',
    title: 'Harry Potter and the Order of the Phoenix',
    image: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T2/images/I/51bZujlJxlL._SX218_BO1,204,203,200_QL40_FMwebp_.jpg',
    bg: '#00C48C'
  }
])

const booksSorting = computed(() => {
    return books.value.sort((a, b) => {
        let modifier = typeSort.value === 'desc' ? -1 : 1
        let aValue = a[sortField.value]
        let bValue = b[sortField.value]
        if (aValue === undefined || bValue === undefined) return 0
        if (typeof aValue === 'string') aValue = aValue.toLowerCase()
        if (typeof bValue === 'string') bValue = bValue.toLowerCase()
        return (typeof aValue === 'number' && typeof bValue === 'number') 
            ? (aValue - bValue) * modifier 
            : aValue.localeCompare(bValue) * modifier
    })
})

const setSort = (name) => {
    if(name === 'Cover') return // Игнорировать сортировку при клике на поле "Cover"
    if(sortField.value === name) {
        typeSort.value = typeSort.value === 'asc' ? 'desc' : 'asc'
    } else {
        sortField.value = name
    }
}

</script>