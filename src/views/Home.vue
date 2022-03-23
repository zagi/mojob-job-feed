<template>
  <div class="home">
    {{ selectedPositionFunctions }}
    <job-feed
      :job-listings="jobListing"
      :position-functions="positionFunctionFilters"
      @selectedPositionFunctions="onSelectedPositionFunctionsChange"
      @selectedNItemsPerPage="onSelectedNItemsPerPageChange"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import JobFeed from "@/components/JobFeed.vue";
import BaseApi from "@/api-requests/api";
import { IPage, PositionFunction, JobListing } from "@/models/models";
import { FIVE_PER_PAGE, JOB_LISTING_DEFAULT_PARAMS } from "@/config/app";

@Component({
  components: {
    JobFeed,
  },
})
export default class Home extends Vue {
  selectedPositionFunctions: number[] = [];
  selectedNItemsPerPage: number = FIVE_PER_PAGE;
  private mojobApi: BaseApi = new BaseApi(
    "https://test-api.mojob.io/public/",
    this.axios
  );
  private positionFunctionFilters: PositionFunction[] = [];
  private jobListing: JobListing[] = [];

  onSelectedPositionFunctionsChange(val: number[]) {
    this.selectedPositionFunctions = val;
    this.refreshJobListing();
  }
  onSelectedNItemsPerPageChange(val: number) {
    this.selectedNItemsPerPage = val;
    this.refreshJobListing();
  }

  async refreshJobListing() {
    try {
      var paramsTmp: Object = {
        page_size:
          this.selectedNItemsPerPage > -1 ? this.selectedNItemsPerPage : null,
        use_pagination: this.selectedNItemsPerPage == -1 ? "False" : "True",
        position_functions:
          this.selectedPositionFunctions.length > 0
            ? this.selectedPositionFunctions.join(",")
            : null,
      };
      var params: Object = { ...JOB_LISTING_DEFAULT_PARAMS, ...paramsTmp };
      const jobListingResponsePage: IPage<JobListing> = await this.mojobApi.getJobListings(
        params
      );
      if (jobListingResponsePage.results) {
        this.jobListing = jobListingResponsePage.results;
        console.log(JSON.stringify(this.jobListing, null, 2));
        console.log(this.jobListing);
      } else {
        console.log("Failed loading job listing");
      }
    } catch (e) {
      console.log("Failed loading job listing");
      console.log(e);
    }
  }
  /**
   * Here you can do necessary request to our
   * public test-API in order to retrieve a list of job listings and a list of
   * position function filters.
   *
   * You can test the endpoints and see the documentation at:
   * https://test-api.mojob.io/public/docs/
   *
   * @private
   */

  private async mounted() {
    // Here is an example on how to retrieve job position function filters
    try {
      const jobLocationFiltersResponsePage: IPage<PositionFunction> = await this.mojobApi.getPositionFunctions();
      if (jobLocationFiltersResponsePage.results) {
        this.positionFunctionFilters = jobLocationFiltersResponsePage.results;
        console.log(JSON.stringify(this.positionFunctionFilters, null, 2));
        console.log(this.positionFunctionFilters);
      } else {
        console.log("Failed loading position function filters");
      }
    } catch (e) {
      console.log("Failed loading position function filters");
      console.log(e);
    }

    await this.refreshJobListing();
  }
}
</script>
