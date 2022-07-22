<template>
  <div :class="'container mx-auto p-2 max-w-lg' + darkClass">
    <div
      class="fixed cursor-pointer hover:font-bold top-[10px] right-[10px]"
      @click="darkTheme = !darkTheme"
    >
      {{ darkTheme ? 'Светлая тема' : 'Темная тема' }}
    </div>
    <div
      class="
        fixed
        top-[0]
        left-[0]
        w-[100vw]
        h-[100vh]
        bg-[#fff]
        dark:bg-[#000]
        z-[-100]
      "
    ></div>
    <form @submit.prevent="search">
      <div class="relative">
        <search-icon />
        <app-input
          placeholder="Введите название репозитория..."
          v-model="query"
        />
        <btn v-if="!!query" type="submit">Поиск</btn>
      </div>
    </form>
    <div class="mt-10">
      <list-item v-for="repo of repos" :key="repo.id">
        <div class="flex justify-between items-center">
          <span class="text-black dark:text-white text-2xl">{{
            repo.name
          }}</span>
          <chip>
            <chip-img :src="repo.owner.avatar_url" />
            {{ repo.owner.login }}
          </chip>
        </div>
        <div class="text-grey text-sm">
          {{ repo.description }}
        </div>
        <star> {{ repo.stargazers_count }} звезд </star>
      </list-item>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue';
import { useSearch } from './useSearch';
import Star from '../ui/star.vue';
import Btn from '../ui/btn.vue';
import AppInput from '../ui/input.vue';
import SearchIcon from '../ui/search-icon.vue';
import ListItem from '../ui/list-item.vue';
import Chip from '../ui/chip.vue';
import ChipImg from '../ui/chip-img.vue';

const { query, repos, search } = useSearch();
const darkTheme = ref(false);

const darkClass = computed({
  get() {
    return darkTheme.value ? ' dark' : '';
  },
});
</script>
