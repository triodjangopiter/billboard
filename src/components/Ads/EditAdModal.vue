<template>
  <v-dialog width="400px" v-model="modal">
    <v-btn class="warning" falt slot="activator">Edit</v-btn>

    <v-card>
      <v-container>

        <v-layout row>
          <v-flex xs12>
            <v-card-title>
              <h1 class="text--primary">Edit Ad</h1>
            </v-card-title>
          </v-flex>
        </v-layout>

        <v-divider></v-divider>

        <v-layout row>
          <v-flex xs12>
            <v-card-text>

              <v-text-field
              name="title"
              label="Title"
              type="title"
              v-model="editedTitle"
            ></v-text-field>

              <v-text-field
                name="description"
                label="Description"
                type="description"
                milti-line
                v-model="editedDescription"
              ></v-text-field>

            </v-card-text>
          </v-flex>
        </v-layout>

        <v-divider></v-divider>

        <v-layout row>
          <v-flex xs12>
            <v-card-actions>
              <v-spacer>
                <v-btn flat @click="onCancel">Cancel</v-btn>
                <v-btn flat class="success" @click="onSave">Save</v-btn>
              </v-spacer>
            </v-card-actions>
          </v-flex>
        </v-layout>

      </v-container>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    props: ['ad'],
    data () {
      return {
        modal: false,
        editedTitle: this.ad.title,
        editedDescription: this.ad.description
      }
    },
    methods: {
      onCancel () {
        this.editedDescription = this.ad.description
        this.editedTitle = this.ad.title
        this.modal = false
      },
      onSave () {
        if (this.editedDescription !== '' && this.editedTitle !== '') {
          this.$store.dispatch('updateAd', {
            title: this.editedTitle,
            description: this.editedDescription,
            id: this.ad.id
          })
          this.modal = false
        }
      }
    }
  }
</script>
