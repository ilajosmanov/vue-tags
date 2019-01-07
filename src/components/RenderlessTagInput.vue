<script lang="ts">
import { Component, Vue, Model, Prop, Emit } from 'vue-property-decorator';

@Component({
  name: "RenderlessTagInput"
})
export default class extends Vue {
  @Model("update", { required: true }) tags!: string[];
  @Prop({ default: true }) removeOnBackspace!: boolean;

  @Emit()
  update(tags: string[]) { }

  input = "";

  removeTag(tag: string) {
    this.update(this.tags.filter(t => t != tag))
  }

  clearInput() {
    this.input = "";
  }

  handleBackspace() {
    if (this.newTag.length === 0 && this.removeOnBackspace) {
      this.update(this.tags.slice(0, -1));
    }
  }

  addTag() {
    if (this.newTag.length === 0 || this.tags.includes(this.newTag)) {
      return;
    };

    this.update([...this.tags, this.newTag]);
    this.clearInput();
  }

  get newTag() {
    return this.input.trim();
  }

  render() {
    return this.$scopedSlots.default!({
      tags: this.tags,
      removeTag: this.removeTag,
      removeButtonEvents: (tag: string) => ({
        click: () => {
          this.removeTag(tag)
        }
      }),
      inputProps: {
        value: this.input
      },
      inputEvents: {
        input: (e: Event) => {
          const target = e.target;
          if (target instanceof HTMLInputElement) {
            this.input = target.value;
          }
        },
        keydown: (e: KeyboardEvent) => {
          if (e.key == "Backspace") {
            this.handleBackspace();
          }
          if (e.key == "Enter") {
            e.preventDefault();
            this.addTag();
          }
        }
      }
    })
  }
}
</script>
