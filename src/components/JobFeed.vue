<template>
  <div class="job-feed">
    <v-toolbar dense flat color="transparent" elevation="0">
      <position-function-dropdown
        :position-functions="positionFunctions"
        v-on="$listeners"
      />
      <v-spacer></v-spacer>
      <n-items-per-page-dropdown v-on="$listeners" />
    </v-toolbar>
    <v-container>
      <v-row>
        <v-col cols="12" v-for="(item, i) in jobListings" :key="i">
          <v-card>
            <v-card-title>
              {{ item.job.title }}
            </v-card-title>
            <v-card-text>
              {{ item.job.unit.display_name }} •
              {{ item.job.position_function.name_en }} •
              {{ item.job.due_date }}
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { JobListing, PositionFunction } from "@/models/models";
import PositionFunctionDropdown from "@/components/PositionFunctionDropdown.vue";
import NItemsPerPageDropdown from "@/components/NItemsPerPageDropdown.vue";

@Component({
  components: {
    PositionFunctionDropdown,
    NItemsPerPageDropdown,
  },
})
export default class JobFeed extends Vue {
  @Prop({ default: () => [], type: Array as () => JobListing[] })
  private jobListings!: JobListing[];
  @Prop({ default: () => [], type: Array as () => PositionFunction[] })
  private positionFunctions!: PositionFunction[];
}
</script>
