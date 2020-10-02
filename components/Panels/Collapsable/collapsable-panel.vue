<template>
  <div class="container">
    <div class="header" @click="isOpened = !isOpened">
      <div
        class="arrow"
        :class="{
          'arrow-down': isOpened,
        }"
      ></div>
      <h3>{{ title }}</h3>
    </div>

    <div
      class="content"
      :class="{
        'content-opened': isOpened,
      }"
    >
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpened: false,
    };
  },
  props: {
    title: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  box-shadow: 0 2px 5px -2px var(--normalShadowColor);
  margin: 10px;
  border: 1px solid #eee;
  border-radius: 15px 15px 0px 0px;
  background-color: var(--interfaceBackgroundColor);

  .header {
    display: flex;
    align-items: center;
    background-color: #fff;
    border-radius: 15px 15px 0px 0px;
    border-bottom: 1px solid var(--interfaceSeparatorColor1);
    height: 50px;
    cursor: pointer;
    transition: 0.2s;

    button {
      background: transparent;
      border: none;
      cursor: pointer;
    }

    button:focus {
      outline: none;
    }
  }

  .content {
    height: auto;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.15s ease-out;
  }

  .content-opened {
    padding: 10px;
    transition: max-height 0.15s ease-out;
    max-height: 500px !important;
  }
}

.arrow-down {
  transform: rotate(90deg);
}

.arrow {
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  border-left: 12px solid var(--interfaceItemsBorderColor);

  width: 0;
  height: 0;
  margin: 10px;
  transition: 0.3s;
  border-radius: 3px;
}

@supports (-webkit-appearance: none) or (-moz-appearance: none) {
  input[type="checkbox"],
  input[type="radio"] {
    -webkit-appearance: none;
    -moz-appearance: none;
    height: 21px;
    outline: none;
    display: inline-block;
    vertical-align: top;
    position: relative;
    cursor: pointer;
    border: 1px solid var(--bc, var(--interfaceItemsBorderColor));
    background: var(--b, var(--interfaceIdleBackgroundColor));
    transition: background 0.3s, border-color 0.3s, box-shadow 0.2s;

    &:after {
      content: "";
      display: block;
      left: 0;
      top: 0;
      position: absolute;
      transition: transform var(--d-t, 0.3s) var(--d-t-e, ease),
        opacity var(--d-o, 0.2s);
    }

    &:checked {
      --b: var(--interfaceActiveColor);
      --bc: var(--interfaceActiveColor);
      --d-o: 0.3s;
      --d-t: 0.6s;
      --d-t-e: cubic-bezier(0.2, 0.85, 0.32, 1.2);
    }

    &:disabled {
      --b: var(--disabled);
      cursor: not-allowed;
      opacity: 0.9;
      &:checked {
        --b: var(--interfaceDisabledInnerColor);
        --bc: var(--interfaceDisabledColor);
      }
      & + label {
        cursor: not-allowed;
      }
    }

    &:hover {
      &:not(:checked) {
        &:not(:disabled) {
          --bc: var(--interfaceItemsBorderHoverColor);
        }
      }
    }

    &:focus {
      box-shadow: 0 0 0 var(--interfaceFocusColor);
    }

    &:not(.switch) {
      width: 21px;
      &:after {
        opacity: var(--o, 0);
      }
      &:checked {
        --o: 1;
      }
    }

    & + label {
      font-size: 14px;
      line-height: 21px;
      display: inline-block;
      vertical-align: top;
      cursor: pointer;
      margin-left: 4px;
    }
  }

  input[type="checkbox"] {
    &:not(.switch) {
      border-radius: 7px;
      &:after {
        width: 5px;
        height: 9px;
        border: 2px solid var(--interfaceActiveInnerColor);
        border-top: 0;
        border-left: 0;
        left: 7px;
        top: 4px;
        transform: rotate(var(--r, 20deg));
      }
      &:checked {
        --r: 43deg;
      }
    }
    &.switch {
      width: 38px;
      border-radius: 11px;
      &:after {
        left: 2px;
        top: 2px;
        border-radius: 50%;
        width: 15px;
        height: 15px;
        background: var(--ab, var(--interfaceItemsBorderColor));
        transform: translateX(var(--x, 0));
      }
      &:checked {
        --ab: var(--interfaceActiveInnerColor);
        --x: 17px;
      }
      &:disabled {
        &:not(:checked) {
          &:after {
            opacity: 0.6;
          }
        }
      }
    }
  }
  input[type="radio"] {
    border-radius: 50%;
    &:after {
      width: 19px;
      height: 19px;
      border-radius: 50%;
      background: var(--interfaceActiveInnerColor);
      opacity: 0;
      transform: scale(var(--s, 0.7));
    }
    &:checked {
      --s: 0.5;
    }
  }

  input[type="text"] {
    outline: none;
    border: 1px solid var(--interfaceItemsBorderColor);
    padding: 5px;
    border-radius: 4px;
    &:hover,
    &:focus {
      border: 1px solid var(--interfaceActiveColor);
    }
  }

  input:hover,
  select:hover {
    box-shadow: 0 2px 5px -2px var(--normalShadowColor);
    transition: box-shadow 0.1s;
  }

  input,
  select {
    margin: 0 5px !important;
    font-family: "Roboto", sans-serif;
  }

  button {
    border: none;
    outline: none;
    background: var(--interfacePrimaryButtonBackgroundColor);
    color: var(--interfacePrimaryButtonForegroundColor);
    padding: 4px 8px;
    border-radius: 4px;
    cursor: pointer;
    margin: 5px;
  }

  select {
    border-radius: 4px;
    padding: 5px 35px 5px 5px;
    font-size: 15px;
    border: 1px solid var(--interfaceItemsBorderColor);
    height: 34px;
    outline: none !important;
    cursor: pointer;
    &:hover,
    &:focus {
      border: 1px solid var(--interfaceActiveColor);
    }
  }

  /* CAUTION: Internet Explorer hackery ahead */

  select::-ms-expand {
    display: none; /* Remove default arrow in Internet Explorer 10 and 11 */
  }

  /* Target Internet Explorer 9 to undo the custom arrow */
  @media screen and (min-width: 0\0) {
    select {
      background: none\9;
      padding: 5px\9;
    }
  }
}
</style>
