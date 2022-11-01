<script setup>
// import Logo from "../components/Logo.vue";
import NavItem from "../components/NavItem.vue";
import IntusValidation from "../components/IntusValidation.vue";
import { HomeIcon, NewspaperIcon, PhotoIcon } from "@heroicons/vue/24/outline";

const navItems = [
  {href: "#", active: false, label: "Home", children: [], icon: HomeIcon},
  {
    href: "#", active: false,
    label: "Posts",
    children: [
      {href: "#", active: false, label: "All posts", children: [], icon: null},
      {href: "#", active: false, label: "Add new", children: [], icon: null},
      {href: "#", active: false, label: "Categories", children: [], icon: null},
    ],
    icon: NewspaperIcon,
  },
  {
    href: "#", active: false,
    label: "Media",
    children: [
      {href: "#", active: false, label: "Library", children: [], icon: null},
      {
        href: "#", active: false,
        label: "Add new",
        children: [{href: "#", active: false, label: "Third level", children: [], icon: null}],
        icon: null,
      },
    ],
    icon: PhotoIcon,
  },
];
</script>
<template>
  <div class="flex min-h-screen">
    <div class="w-64 shrink-0 border-r border-gray-200 bg-gray-50 py-4">
      <div class="px-4">
        <!-- <a
          href="#"
          class="inline-block"
        >
          <Logo class="h-8 w-auto"/>
        </a> -->
      </div>

      <nav class="mt-2 px-2">
        <NavItem
          :item="item"
          v-for="item in navItems"
          :key="item.label"
        />
      </nav>
    </div>

    <main class="p-4"><IntusValidation/></main>
  </div>
</template>
