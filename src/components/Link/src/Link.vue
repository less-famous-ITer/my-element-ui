<template>
<a
    @click="preventMove($event)"

    :href="props.href"
    :target="props.target"

    :style="{
        '--fontColor': props.fontColor,
        '--hoverColor': props.hoverColor
    }"

    :class="{
        fontColor: true,
        hoverColor: true,
        underline: (props.underline && !props.disabled),
        disabled: props.disabled
    }"

>
  <slot></slot>
</a>
</template>

<script setup lang="ts">

interface Props {
    // 原生 a 标签属性
    href?: string;
    target?: string;

    // 文字颜色
    fontColor?: string;
    // 悬停颜色
    hoverColor?: string;
    // 下划线
    underline?: boolean;
    // 禁用
    disabled?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
    href: "##",
    target: "",

    fontColor: "#000000",
    hoverColor: "#535bf2",
    underline: true,
    disabled: false
})

/**
 * 当 href==="##" 时阻止默认跳转
 */
function preventMove(e: MouseEvent): void {
  if(props.href === "##" || props.disabled) {
    e.preventDefault()
  }
}

</script>

<style scoped lang="less">
.fontColor {
    color: var(--fontColor)
}
.hoverColor:hover {
    color: var(--hoverColor)
}
.underline:hover {
    border-bottom: 1px solid var(--hoverColor);
}
.disabled {
    color: #888888;
}
.disabled:hover {
    color: #888888;
    cursor: not-allowed;
}
</style>