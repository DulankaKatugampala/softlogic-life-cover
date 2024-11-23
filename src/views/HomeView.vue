<template>
  <div class="min-h-full">
    <Popover v-slot="{ open }" as="header" class="bg-indigo-600 pb-24 flex-grow">
      <div class="mx-auto px-4 sm:px-6 max-w-7xl lg:px-8">
        <div class="relative flex items-center py-5 justify-between">
          <!-- Logo -->
          <div class="left-0 shrink-0 static">
            <a href="#">
              <span class="sr-only">Your Company</span>
              <img alt="Your Company" class="h-8 w-auto"
                   src="https://tailwindui.com/plus/img/logos/mark.svg?color=indigo&shade=300"/>
            </a>
          </div>

          <!-- Right section on desktop -->
          <div class="ml-4 flex items-center lg:pr-0.5">
            <Listbox v-model="selected" as="div" class="min-w-52">
              <div class="relative">
                <ListboxButton
                    class="relative w-full cursor-default rounded-md bg-white py-1.5 pl-3 pr-10 text-left text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 sm:text-sm/6">
                    <span class="inline-flex w-full truncate">
                      <span class="truncate">{{ selected.plan }}</span>
                      <span class="ml-2 truncate text-gray-500">{{ selected.value }}</span>
                    </span>
                    <span class="pointer-events-none absolute inset-y-0 right-0 flex items-center pr-2">
                      <ChevronUpDownIcon aria-hidden="true" class="size-5 text-gray-400"/>
                    </span>
                </ListboxButton>

                <transition leave-active-class="transition ease-in duration-100" leave-from-class="opacity-100"
                            leave-to-class="opacity-0">
                  <ListboxOptions
                      class="absolute z-10 mt-1 max-h-60 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black/5 focus:outline-none sm:text-sm">
                    <ListboxOption v-for="person in data" :key="person.plan" v-slot="{ active, selected }"
                                   :value="person"
                                   as="template">
                      <li :class="[active ? 'bg-indigo-600 text-white' : 'text-gray-900', 'relative cursor-default select-none py-2 pl-3 pr-9']">
                        <div class="flex">
                          <span :class="[selected ? 'font-semibold' : 'font-normal', 'truncate']">{{
                              person.plan
                            }}</span>
                          <span :class="[active ? 'text-indigo-200' : 'text-gray-500', 'ml-2 truncate']">{{
                              person.value
                            }}</span>
                        </div>

                        <span v-if="selected"
                              :class="[active ? 'text-white' : 'text-indigo-600', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                <CheckIcon aria-hidden="true" class="size-5"/>
              </span>
                      </li>
                    </ListboxOption>
                  </ListboxOptions>
                </transition>
              </div>
            </Listbox>
          </div>

          <!-- Menu button -->
          <div class="absolute right-0 shrink-0 hidden">
            <!-- Mobile menu button -->
            <PopoverButton
                class="relative inline-flex items-center justify-center rounded-md bg-transparent p-2 text-indigo-200 hover:bg-white/10 hover:text-white focus:outline-none focus:ring-2 focus:ring-white">
              <span class="absolute -inset-0.5"/>
              <span class="sr-only">Open main menu</span>
              <Bars3Icon v-if="!open" aria-hidden="true" class="block size-6"/>
              <XMarkIcon v-else aria-hidden="true" class="block size-6"/>
            </PopoverButton>
          </div>
        </div>

        <div class="border-t border-white/20 py-5 block">
          <div class="grid grid-cols-3 items-center gap-8">
            <div class="col-span-3">
              <nav class="flex gap-3 flex-wrap">
                <a v-for="item in navigation" :key="item.name" :aria-current="item.current ? 'page' : undefined"
                   :class="[activeTab === item.key ? 'text-white bg-white/10' : 'text-indigo-100', 'rounded-md px-3 py-2 text-sm font-medium hover:bg-white/10 whitespace-nowrap']"
                   @click="activeTab = item.key">{{ item.name }}</a>
              </nav>
            </div>
          </div>
        </div>
      </div>

      <TransitionRoot :show="open" as="template">
        <div class="hidden">
          <TransitionChild as="template" enter="duration-150 ease-out" enter-from="opacity-0" enter-to="opacity-100"
                           leave="duration-150 ease-in" leave-from="opacity-100" leave-to="opacity-0">
            <PopoverOverlay class="fixed inset-0 z-20 bg-black/25"/>
          </TransitionChild>

          <TransitionChild as="template" enter="duration-150 ease-out" enter-from="opacity-0 scale-95"
                           enter-to="opacity-100 scale-100" leave="duration-150 ease-in"
                           leave-from="opacity-100 scale-100" leave-to="opacity-0 scale-95">
            <PopoverPanel
                class="absolute inset-x-0 top-0 z-30 mx-auto w-full max-w-3xl origin-top transform p-2 transition"
                focus>
              <div class="divide-y divide-gray-200 rounded-lg bg-white shadow-lg ring-1 ring-black/5">
                <div class="pb-2 pt-3">
                  <div class="flex items-center justify-between px-4">
                    <div>
                      <img alt="Your Company"
                           class="h-8 w-auto"
                           src="https://tailwindui.com/plus/img/logos/mark.svg?color=indigo&shade=600"/>
                    </div>
                    <div class="-mr-2">
                      <PopoverButton
                          class="relative inline-flex items-center justify-center rounded-md bg-white p-2 text-gray-400 hover:bg-gray-100 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500">
                        <span class="absolute -inset-0.5"/>
                        <span class="sr-only">Close menu</span>
                        <XMarkIcon aria-hidden="true" class="size-6"/>
                      </PopoverButton>
                    </div>
                  </div>
                  <div class="mt-3 space-y-1 px-2">
                    <a class="block rounded-md px-3 py-2 text-base font-medium text-gray-900 hover:bg-gray-100 hover:text-gray-800"
                       href="#">Home</a>
                    <a class="block rounded-md px-3 py-2 text-base font-medium text-gray-900 hover:bg-gray-100 hover:text-gray-800"
                       href="#">Profile</a>
                    <a class="block rounded-md px-3 py-2 text-base font-medium text-gray-900 hover:bg-gray-100 hover:text-gray-800"
                       href="#">Resources</a>
                    <a class="block rounded-md px-3 py-2 text-base font-medium text-gray-900 hover:bg-gray-100 hover:text-gray-800"
                       href="#">Company
                      Directory</a>
                    <a class="block rounded-md px-3 py-2 text-base font-medium text-gray-900 hover:bg-gray-100 hover:text-gray-800"
                       href="#">Openings</a>
                  </div>
                </div>
                <div class="pb-2 pt-4">
                  <div class="flex items-center px-5">
                    <div class="shrink-0">
                      <img :src="user.imageUrl" alt="" class="size-10 rounded-full"/>
                    </div>
                    <div class="ml-3 min-w-0 flex-1">
                      <div class="truncate text-base font-medium text-gray-800">{{ user.name }}</div>
                      <div class="truncate text-sm font-medium text-gray-500">{{ user.email }}</div>
                    </div>
                    <button
                        class="relative ml-auto shrink-0 rounded-full bg-white p-1 text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                        type="button">
                      <span class="absolute -inset-1.5"/>
                      <span class="sr-only">View notifications</span>
                      <BellIcon aria-hidden="true" class="size-6"/>
                    </button>
                  </div>
                  <div class="mt-3 space-y-1 px-2">
                    <a v-for="item in userNavigation" :key="item.name" :href="item.href"
                       class="block rounded-md px-3 py-2 text-base font-medium text-gray-900 hover:bg-gray-100 hover:text-gray-800">{{
                        item.name
                      }}</a>
                  </div>
                </div>
              </div>
            </PopoverPanel>
          </TransitionChild>
        </div>
      </TransitionRoot>
    </Popover>

    <main class="-mt-24 pb-8">
      <div class="mx-auto px-4 sm:px-6 max-w-7xl lg:px-8">
        <h1 class="sr-only">Page title</h1>
        <!-- Main 3 column grid -->
        <div class="grid grid-cols-1 items-start gap-4 lg:grid-cols-3 lg:gap-8">
          <!-- Left column -->
          <div class="grid grid-cols-1 gap-4 lg:col-span-3">
            <section aria-labelledby="section-1-title">
              <h2 id="section-1-title" class="sr-only">Section title</h2>
              <div class="overflow-hidden rounded-lg bg-white shadow">
                <div class="p-6">
                  {{ selected[activeTab] }}
                </div>
              </div>
            </section>
          </div>

          <!-- Right column -->
<!--          <div class="grid grid-cols-1 gap-4">-->
<!--            <section aria-labelledby="section-2-title">-->
<!--              <h2 id="section-2-title" class="sr-only">Section title</h2>-->
<!--              <div class="overflow-hidden rounded-lg bg-white shadow">-->
<!--                <div class="p-6">-->
<!--                  &lt;!&ndash; Your content &ndash;&gt;-->
<!--                </div>-->
<!--              </div>-->
<!--            </section>-->
<!--          </div>-->
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import {
  Listbox,
  ListboxButton,
  ListboxOption,
  ListboxOptions,
  Popover,
  PopoverButton,
  PopoverOverlay,
  PopoverPanel,
  TransitionChild,
  TransitionRoot,
} from '@headlessui/vue'
import {Bars3Icon, BellIcon, XMarkIcon} from '@heroicons/vue/24/outline'
import {CheckIcon, ChevronUpDownIcon, MagnifyingGlassIcon} from '@heroicons/vue/20/solid';
import {ref} from 'vue';
import data from '@/data/data.json';

const selected = ref(data[0])

const user = {
  name: 'Tom Cook',
  email: 'tom@example.com',
  imageUrl:
      'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
}
const navigation = [
  {name: 'Pre-Hospitalization', key: 'preHospitalization', current: true},
  {name: 'Post-Hospitalization', key: 'postHospitalization', current: false},
  {name: 'Hospitalization in Non-Paying Ward', key: 'hospitalizationInNonPayingWard', current: false},
  {name: 'Optical Cover', key: 'opticalCover', current: false},
  {name: 'Maternity Cover', key: 'maternityCover', current: false},
  {name: 'Pharmacy Cover', key: 'pharmacyCover', current: false},
  {name: 'Dental Cover', key: 'dentalCover', current: false},
  {name: 'Wellbeing Cover', key: 'wellbeingCover', current: false},
  {name: 'Escalation Benefit / No claim bonus yearly increment', key: 'escalationYearlyIncrement', current: false},
  {name: 'Reinstatement Benefit / yearly limit', key: 'escalationLimit', current: false},
]
const userNavigation = [
  {name: 'Your Profile', href: '#'},
  {name: 'Settings', href: '#'},
  {name: 'Sign out', href: '#'},
]

const activeTab = ref("preHospitalization");
</script>