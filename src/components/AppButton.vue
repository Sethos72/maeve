<template>
  <v-btn
    :round="round"
    @click="$emit('on-click')"
    :color="color"
    :style="buttonColorStyle"
    @block="block"
  >
    <slot></slot>
  </v-btn>
</template>

<script lang="ts">
import Vue from 'vue';
import { isLight, TEXT_PRIMARY_DARK, TEXT_PRIMARY_LIGHT } from '@/themes';
import { Prop, Component } from 'vue-property-decorator';
import { State } from 'vuex-class';
import { ButtonStyle } from '@/utils/constants';

@Component
export default class AppButton extends Vue {
  @Prop({ default: 'accent' }) color!: string;
  @Prop({ default: false }) block!: boolean;

  @State(state => state.settings.buttonStyle) buttonStyle!: ButtonStyle;

  get buttonColorStyle() {
    return {
      color: isLight(this.$vuetify.theme.accent as string)
        ? TEXT_PRIMARY_LIGHT
        : TEXT_PRIMARY_DARK
    };
  }

  get round(): boolean {
    return this.buttonStyle === ButtonStyle.round;
  }
}
</script>
