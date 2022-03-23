<template>
  <v-menu bottom offset-y close-on-click>
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="primary" dark v-bind="attrs" v-on="on">
        Position functions
      </v-btn>
    </template>
    <v-list color="transparent">
      <v-treeview
        elevation="0"
        class="mt-10"
        :items="positionFunctions"
        selectable
        selection-type="independent"
      ></v-treeview>
    </v-list>
  </v-menu>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { PositionFunction } from "@/models/models";

@Component
export default class PositionFunctionDropdown extends Vue {
  @Prop({ default: () => [], type: Array as () => PositionFunction[] })
  private positionFunctions!: PositionFunction[];
}
</script>
