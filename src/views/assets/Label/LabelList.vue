<template>
  <GenericListPage :table-config="tableConfig" :header-actions="headerActions" />
</template>

<script>
import { GenericListPage } from '@/layout/components'
import { ActionsFormatter } from '@/components/ListTable/formatters/index'

export default {
  components: {
    GenericListPage
  },
  data() {
    return {
      tableConfig: {
        url: '/api/v1/assets/labels/',
        columns: [
          {
            prop: 'name',
            label: this.$t('assets.Name'),
            showOverflowTooltip: true,
            sortable: true
          },
          {
            prop: 'value',
            label: this.$t('assets.Value'),
            showOverflowTooltip: true,
            sortable: 'custom'
          },
          {
            prop: 'asset_count',
            label: this.$t('assets.Assets'),
            width: '80px'
          },
          {
            prop: 'id',
            align: 'center',
            formatter: ActionsFormatter,
            label: this.$t('assets.Action'),
            width: '200px',
            formatterArgs: {
              performDelete: ({ row, col }) => {
                const id = row.id
                const url = `/api/v1/assets/labels/${id}/`
                return this.$axios.delete(url)
              }
            }
          }
        ]
      },
      headerActions: {
        hasRightActions: false,
        hasExport: false,
        hasImport: false,
        hasRefresh: true,
        hasSearch: true,
        hasMoreActions: false,
        createRoute: 'LabelCreate'
      }
    }
  }
}
</script>

<style>

</style>
