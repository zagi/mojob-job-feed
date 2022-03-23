<template>
  <div class="job-feed">
    <v-toolbar dense flat color="transparent" elevation="0">
      <position-function-dropdown
        :position-functions="positionFunctions"
        @selectedPositionFunctions="onSelectedPositionFunctionsChange"
      />
      <v-spacer></v-spacer>
      <n-items-per-page-dropdown @selectedNItemsPerPage="onSelectedNItemsPerPageChange" />
    </v-toolbar>
    
    <div>

    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";
import { JobListing, PositionFunction } from "@/models/models";
import PositionFunctionDropdown from "@/components/PositionFunctionDropdown.vue";
import NItemsPerPageDropdown from "@/components/NItemsPerPageDropdown.vue";

@Component({
  components: {
    PositionFunctionDropdown,
    NItemsPerPageDropdown
  },
})
export default class JobFeed extends Vue {
  selectedPositionFunctions: number[] = [];
  selectedNItemsPerPage: number = 5;
  @Prop({ default: () => [], type: Array as () => JobListing[] })
  private jobListings!: JobListing[];
  @Prop({ default: () => [], type: Array as () => PositionFunction[] })
  private positionFunctions!: PositionFunction[];
  @Emit()
  onSelectedPositionFunctionsChange(val: number[]) {
    this.selectedPositionFunctions = val;
  }
  @Emit()
  onSelectedNItemsPerPageChange(val: number) {
    this.selectedNItemsPerPage = val;
  }
}
</script>

<style scoped></style>
