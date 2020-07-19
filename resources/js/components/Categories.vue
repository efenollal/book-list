<template>
    <div>
        <b-table
            id="categories"
            striped
            hover
            :items="items"
            :fields="fields"
            :per-page="perPage"
            :current-page="currentPage"
        >
            <template v-slot:cell(link)="">
                <font-awesome-icon icon="external-link-alt" class="icon alt" aria-hidden="true"></font-awesome-icon>
            </template>
        </b-table>
        <b-pagination
            v-model="currentPage"
            :total-rows="rows"
            :per-page="perPage"
            :current-page="currentPage"
            aria-controls="categories"
        ></b-pagination>

        <p class="mt-3">Current Page: {{ currentPage }}</p>

    </div>
</template>

<script>
export default {
    data() {
        return {
            perPage: 10,
            currentPage: 1,
            items: [],
            fields: [
                // {
                //     key: 'draggable',
                //     label: '',
                //     sortable: false
                // },
                {
                    key: 'display_name',
                    sortable: true,
                    label: 'Book Name'
                },
                {
                    key: 'newest_published_date',
                    sortable: true,
                    label: 'Newest Published Date'
                },
                {
                    key: 'link',
                    label: '',
                    sortable: false
                }
            ]
        }
    },
    computed: {
        rows() {
            return this.items.length
        }
    },
    mounted() {
        this.listNames()
        console.log(this.names)
    },
    methods: {

        listNames() {
            const apiKey = 'DiP60FYqGbxKfMZBBIPhwBSPhUWA2EkL';
            const booksUrl = `https://api.nytimes.com/svc/books/v3/lists/names?api-key=${apiKey}`;
            fetch(booksUrl, { method: 'get' })
                .then(res => res.json())
                .then(res => {
                    console.log(res)
                    this.items = res.results
                })
                .catch(error => {
                    console.log(error)
                })
        },
    }
}
</script>
