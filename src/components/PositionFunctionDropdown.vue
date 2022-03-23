<template>
  <v-menu bottom offset-y close-on-click>
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="primary" dark v-bind="attrs" v-on="on">
        Position functions
      </v-btn>
    </template>
    <v-list color="transparent">
      <v-treeview
      v-model="selectedPositionFunctions"
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
import { Component, Prop, Vue, Watch } from "vue-property-decorator";
import { PositionFunction } from "@/models/models";

@Component
export default class PositionFunctionDropdown extends Vue {
  selectedPositionFunctions: number[] = [];
  @Prop({ default: () => [], type: Array as () => PositionFunction[] })
  private positionFunctions!: PositionFunction[];
  @Watch('selectedPositionFunctions')
  onSelectedPositionFunctionsChange(val: number[], oldVal: number[]) {
    this.$emit("selectedPositionFunctions", val);
  }
}
</script>
