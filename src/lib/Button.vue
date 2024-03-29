<template>
  <button class="good-button"
          :class="classes"
          :disabled="disabled">
    <span v-if="loading" class="good-loadingIndicator"></span>
    <slot/>
  </button>
</template>

<script lang='ts'>
import {computed} from 'vue';

export default {
  props: {
    theme: {
      type: String,
      default: 'button'
    },
    size: {
      type: String,
      default: 'normal'
    },
    level: {
      type: String,
      default: 'level'
    },
    disabled: {
      type: Boolean,
      default: false
    },
    loading: {
      type: Boolean,
      default: false
    },
  },
  setup(props) {
    const {theme, size, level} = props;
    const classes = computed(() => {
      return {
        [`good-theme-${theme}`]: theme,
        [`good-size-${size}`]: size,
        [`good-level-${level}`]: level,
      };
    });
    return {classes};
  }
};
</script>

<style lang='scss'>
.good-button {
  box-sizing: border-box;
  height: 32px;
  padding: 0 12px;
  cursor: pointer;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  white-space: nowrap;
  background: white;
  color: #333;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  box-shadow: 0 1px 0 fade-out(black, 0.95);
  transition: background 250ms;

  & + & {
    margin-left: 8px;
  }

  &:hover, &:focus {
    color: #1313ff;
    border-color: #1313ff;
  }

  &:focus {
    outline: none;
  }

  &::-moz-focus-inner {
    border: 0;
  }

  &.good-theme-link {
    box-shadow: none;
    color: black;
    border: 1px solid #d9d9d9;

    &:hover, &:focus {
      color: #1313ff;
      border-color: #1313ff;
    }
  }

  &.good-theme-text {
    box-shadow: none;
    color: inherit;
    border: 1px solid #d9d9d9;

    &:hover, &:focus {
      color: #1313ff;
      border-color: #1313ff;
    }
  }

  &.good-size-big {
    font-size: 24px;
    height: 48px;
    padding: 0 16px;
  }

  &.good-size-small {
    font-size: 12px;
    height: 20px;
    padding: 0 4px;
  }

  &.good-theme-button {
    &.good-level-main {
      background: blue;
      color: white;
      border-color: blue;

      &:hover, &:focus {
        background: darken(blue, 10%);
        border-color: darken(blue, 10%);
      }
    }

    &.good-level-danger {
      background: red;
      color: white;
      border-color: red;

      &:hover, &:focus {
        background: darken(red, 10%);
        border-color: darken(red, 10%);
      }
    }

    &.good-level-warning {
      background: #ffce3d;
      color: white;
      border-color: #ffce3d;

      &:hover, &:focus {
        background: darken(#ffce3d, 10%);
        border-color: darken(#ffce3d, 10%);
      }
    }

    &.good-level-success {
      background: #00a854;
      color: white;
      border-color: #00a854;

      &:hover, &:focus {
        background: darken(#00a854, 10%);
        border-color: darken(#00a854, 10%);
      }
    }
  }

  &.good-theme-link {
    &.good-level-danger {
      color: red;

      &:hover, &:focus {
        color: darken(red, 10%)
      }
    }
  }

  &.good-theme-text {
    &.good-level-main {
      color: blue;

      &:hover, &:focus {
        color: darken(blue, 10%)
      }
    }

    &.good-level-danger {
      color: red;

      &:hover, &:focus {
        color: darken(red, 10%)
      }
    }
  }

  &.good-theme-button {
    &[disabled] {
      cursor: not-allowed;
      color: grey;

      &:hover {
        border-color: #d9d9d9;
      }
    }
  }

  &.good-theme-link, &.good-theme-text {
    &[disabled] {
      cursor: not-allowed;
      color: grey;

      &:hover {
        border: none;
        background: none;
      }
    }
  }

  > .good-loadingIndicator {
    width: 14px;
    height: 14px;
    display: inline-block;
    margin-right: 4px;
    border-radius: 8px;
    border-color: blue blue blue transparent;
    border-style: solid;
    border-width: 2px;
    animation: good-loading 1s infinite linear;
  }
}

@keyframes good-loading {
  0% {
    transform: rotate(0deg)
  }
  100% {
    transform: rotate(360deg)
  }
}


</style>