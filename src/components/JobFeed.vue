<template>
  <div class="job-feed">
    <v-toolbar dense flat color="transparent" elevation="0">
      <position-function-dropdown :position-functions="positionFunctions" />
      <v-spacer></v-spacer>
      Dropdown n items per page
    </v-toolbar>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { JobListing, PositionFunction } from '@/models/models';
import PositionFunctionDropdown from '@/components/PositionFunctionDropdown.vue';

@Component({
  components: {
    PositionFunctionDropdown,
  },
})
export default class JobFeed extends Vue {
  @Prop({ default: () => [], type: Array as () => JobListing[] })
  private jobListings!: JobListing[];
  @Prop({ default: () => [], type: Array as () => PositionFunction[] })
  private positionFunctions!: PositionFunction[];
}
</script>

<style scoped></style>
