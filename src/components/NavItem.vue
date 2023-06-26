<!-- для настройки передачи атрибута setup не должен быть -->
<!-- отключаем наследование атрибута корневым элементом компонента, т.к. мы явно указали (v-bind="$attrs") что все атрибуты будут
унаследованы элементом ссылки -->
<script>
export default {
  inheritAttrs: false
}
</script>

<template>
  <li class="flex-1">
    <a v-bind="$attrs" class="flex flex-col items-center p-2 text-xs capitalize">
      <slot></slot>
    </a>
  </li>
</template>