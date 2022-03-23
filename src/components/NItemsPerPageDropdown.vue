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
    <v-list color="transparent"> </v-list>
  </v-menu>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from "vue-property-decorator";

@Component
export default class NItemsPerPageDropdown extends Vue {
  itemsPerPage: number = 5;
}
</script>
