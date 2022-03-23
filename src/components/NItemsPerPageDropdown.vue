<template>
  <v-menu bottom offset-y close-on-click>
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="transparent" v-bind="attrs" v-on="on">
        {{ itemsPerPage > 0 ? `${itemsPerPage} per page` : "Display all" }}
        <v-icon>
          mdi-menu-down
        </v-icon>
      </v-btn>
    </template>
    <v-list color="transparent">
      <v-list-item
        v-for="(item, i) in itemsPerPageOptionsFilter"
        :key="i"
        class="dropdown-item"
      >
        <v-list-item-content>
          <v-list-item-title
            @click="itemsPerPage = item.value"
            v-text="item.text"
          ></v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-menu>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";
import { FIVE_PER_PAGE, TWENTYFIVE_PER_PAGE, DISPLAY_ALL } from "@/config/app";

@Component
export default class NItemsPerPageDropdown extends Vue {
  itemsPerPage: number = 5;
  itemsPerPageOptions: { text: string; value: number }[] = [
    { text: "5 per page", value: FIVE_PER_PAGE },
    { text: "25 per page", value: TWENTYFIVE_PER_PAGE },
    { text: "Display all", value: DISPLAY_ALL },
  ];
  get itemsPerPageOptionsFilter() {
    return this.itemsPerPageOptions.filter(
      (el) => el.value != this.itemsPerPage
    );
  }
  @Watch("selectedPositionFunctions")
  onSelectedPositionFunctionsChange(val: number[], oldVal: number[]) {
    this.$emit("selectedPositionFunctions", val);
  }
}
</script>
<style scoped>
.dropdown-item {
  cursor: pointer;
}
</style>
