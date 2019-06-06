<script>
import { SlotsMixin } from '../../mixins/slots'
import { ParentMixin } from '../../mixins/relation'
export default {
  mixins: [SlotsMixin, ParentMixin('vanDropdownMenu')],
  props: {
    overlay: {
      type: Boolean,
      default: true
    },
    zIndex: {
      type: Number,
      default: 10
    },
    duration: {
      type: Number,
      default: 0.2
    },
    activeColor: {
      type: String,
      default: '#1989fa'
    },
    closeOnClickOverlay: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      children: [],
      top: 0
    }
  },
  methods: {
    toggleItem(active) {
      const { menu } = this.$refs
      const rect = menu.getBoundingClientRect()
      this.top = rect.top + rect.height

      this.children.forEach((item, index) => {
        if (index === active) {
          item.toggle()
        } else if (item.showPopup) {
          item.hide(true)
        }
      })
    },

    onClickOutside() {
      this.children.forEach(item => {
        item.hide()
      })
    }
  },
  render(h) {
    const Titles = this.children.map((item, index) => (
      <div
        role="button"
        tabindex={item.disabled ? -1 : 0}
        class={['van-dropdown-menu__item', { disabled: item.disabled }]}
        onClick={() => {
          if (!item.disabled) {
            this.toggleItem(index)
          }
        }}
      >
        <span
          class={['van-dropdown-menu__title', { active: item.show }, item.titleClass]}
          style={{ color: item.showPopup ? this.activeColor : '' }}
        >
          {item.displayTitle}
        </span>
      </div>
    ))

    return (
      <div ref="menu" class={['van-dropdown-menu', 'van-hairline--top-bottom']}>
        {Titles}
        {this.slots('default')}
      </div>
    )
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
// @import '../../style/var';

.van-dropdown-menu {
  display: flex;
  height: 50px;
  background-color: white;
  user-select: none;

  &__item {
    display: flex;
    flex: 1;
    align-items: center;
    justify-content: center;

    &:active {
      opacity: 0.7;
    }

    &--disabled {
      &:active {
        opacity: 1;
      }

      .van-dropdown-menu__title {
        color: #969799;
      }
    }
  }

  &__title {
    position: relative;
    font-size: 15px;

    &::after {
      position: absolute;
      top: 3px;
      right: -12px;
      border: 3px solid;
      border-color: transparent transparent currentColor currentColor;
      transform: rotate(-45deg);
      opacity: 0.6;
      content: '';
    }

    &--active {
      &::after {
        top: 7px;
        transform: rotate(135deg);
        opacity: 1;
      }
    }
  }
}
</style>
