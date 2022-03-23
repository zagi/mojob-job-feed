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
      <v-list-item v-for="(item, i) in itemsPerPageOptionsFilter" :key="i">
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
import { Component, Vue } from "vue-property-decorator";

@Component
export default class NItemsPerPageDropdown extends Vue {
  itemsPerPage: number = 5;
  itemsPerPageOptions: { text: string; value: number }[] = [
    { text: "5 per page", value: 5 },
    { text: "25 per page", value: 25 },
    { text: "Display all", value: -1 },
  ];
  get itemsPerPageOptionsFilter() {
    return this.itemsPerPageOptions.filter(
      (el) => el.value != this.itemsPerPage
    );
  }
}
</script>
