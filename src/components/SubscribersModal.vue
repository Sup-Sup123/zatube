<template>
  <v-dialog
    v-model="dialog"
    persistent
    transition="fab-transition"
    max-width="800"
  >
    <v-card tile>
      <div class="d-flex justify-space-between mb-5">
        <v-card-title class="py-3">Subscribers</v-card-title>

        <v-btn icon text @click="closeModal">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </div>

      <v-card-text class="px-3">
        <v-row>
          <v-col cols="12" sm="12" md="12" lg="12" class="pt-0 px-0">
            <v-data-table
              :headers="headers"
              :items="subscribers"
              sort-by="calories"
            >
              <template v-slot:item.channelName="{ item }">
                <v-avatar size="35">
                  <img :src="item.avatar" :alt="item.ChannelName" />
                </v-avatar>
                <span class="pl-2">{{ item.channelName }}</span>
              </template>
              <template v-slot:item.actions="{ item }">
                <v-btn
                  text
                  small
                  class="mr-2 blue--text text--darken-4"
                  @click="subscribe(item)"
                >
                  Subscribe
                </v-btn>
              </template>
              <template v-slot:no-data>
                <v-btn color="primary" @click="initialize">Reset</v-btn>
              </template>
            </v-data-table>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: 'SubscribersModal',
  props: ['openDialog'],
  data: function() {
    return {
      headers: [
        {
          text: 'Channel',
          align: 'start',
          value: 'channelName'
        },
        { text: 'Date Subscribed', value: 'createdAt' },
        { text: 'Subcriber count', value: 'subscribers' },
        { text: 'Actions', value: 'actions', align: 'end', sortable: false }
      ],
      subscribers: []
    }
  },
  computed: {
    dialog() {
      return this.openDialog
    }
  },
  methods: {
    initialize() {
      this.subscribers = [
        {
          channelName: 'Brad Traversy',
          avatar: 'https://cdn.vuetifyjs.com/images/john.jpg',
          createdAt: 'Apr 20, 2020',
          subscribers: 5
        },
        {
          channelName: 'John Doe',
          avatar: 'https://cdn.vuetifyjs.com/images/john.jpg',
          createdAt: 'Apr 20, 2020',
          subscribers: 10
        }
      ]
    },
    subscribe(item) {
      console.log(item)
    },
    closeModal() {
      this.$emit('closeDialog')
    }
  },
  mounted() {
    this.initialize()
  }
}
</script>
