<template>
  <renderless-tag-input :tags="tags" @update="update($event)" :remove-on-backspace="removeOnBackspace">
    <div class="tag-input" slot-scope="{ tags, removeTag, removeButtonEvents, inputProps, inputEvents }">
      <span v-for="tag in tags" :key="tag" class="tag-input-tag">
        <span>{{ tag }}</span>
        <button v-on="removeButtonEvents(tag)" type="button" class="tag-input-remove">&times;</button>
      </span>
      <input v-bind="inputProps" v-on="inputEvents" class="tag-input-text" placeholder="Add tag...">
    </div>
  </renderless-tag-input>
</template>

<script lang="ts">
import { Component, Vue, Model, Prop, Emit } from 'vue-property-decorator';
import RenderlessTagInput from '@/components/RenderlessTagInput.vue';

@Component({
  name: "InlineTagInput",
  components: {
    RenderlessTagInput
  }
})
export default class extends Vue {
  @Model("update", { required: true }) tags!: string[];
  @Prop({ default: true }) removeOnBackspace!: boolean;

  @Emit()
  update(tags: string[]) { }
}
</script>

