<template>
  <div>
    <div>
      <Disclosure
        v-for="(item, idx) in items"
        :key="item.id"
        v-slot="{ open, close }"
      >
        <DisclosureButton
          class="tab"
        >
          <span 
            :class="[ open ? 'titleOpen' : 'titleClosed']"
          >
            {{ item.title }}
          </span>
          <div
              :class="[ open ? 'chevron_clicked' : 'chevron']"
          >
          <svg class="svg_chevron"
                xmlns="http://www.w3.org/2000/svg" viewBox="0 0 13.86 16">
            <g>
              <polygon points="0 16 13.86 8 0 0 0 16"/>
            </g>
          </svg>
        </div>
        </DisclosureButton>
        <DisclosurePanel
          class="panelContainer"
          static
        >
          <div 
            :class="[ open ? 'activePanel' : 'inactivePanel' ]"
            ref="el"
          >
            {{ item.content }}
          </div>
        </DisclosurePanel>
        <button
          :ref="(el) => (elements[idx] = el)"
          :data-id="item.id"
          v-show="false"
          @click="doClose(close)"
        ></button>
        <DisclosureStateEmitter :show="open" @show="hideOther(item.id)" />
      </Disclosure>
    </div>
  </div>
</template>

<script setup>
  // use the Vue 3 Composition API
  import { ref } from "vue";
  import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";
  import DisclosureStateEmitter from "./DisclosureStateEmitter.vue";

  // accept the data as props from parent component

  const props = defineProps(['items']);

  // create an empty reference array as elements

  const elements = ref([]);

  // create a function for hiding inactive panels that is triggered when v-show is truthy in child DisclosureStateEmitter component

  // pass item.id to the function as id argument

  const hideOther = (id) => {

    // scan items in elements array and return items where data-id DOES NOT equal the clicked item's id
    const items = elements.value.filter((elm) => {
      return elm.getAttribute("data-id") !== id.toString();
    });

    // for each item where data-id DOES NOT equal the clicked item's id, call click event function
    items.forEach((elm) => elm.click());
  };

  // close items where data-id DOES NOT equal the clicked item's id using the close() function in headlessUI

  const doClose = (close) => {
    close();
  };
</script>

<style scoped>

  .tab {
    width: 100%;
    position: relative;
    display: flex;
    flex-direction: row;
    padding: 1rem 2rem;
    justify-content: space-between;
    background-color: #2D2C28;
    border-radius: none;
    border-style: solid;
    border-width: 0.1rem;
    border-color: #CCFFD9;
    cursor: pointer;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    font-weight: normal;
    font-size: 20px;
  }

  .titleOpen {
    color: #FFF1A1;
    transition-property: color;
    transition-duration: 300ms;
  }

  .titleClosed {
    color: #CCFFD9;
  }
  .chevron {
    max-width: 1rem;
    transform: rotate(0deg);
    transform-origin: center;
    transition: all cubic-bezier(0.4, 0, 0.2, 1) 300ms;
    fill: #CCFFD9;
  }

  .chevron_clicked {
    max-width: 1rem;
    transform: rotate(90deg);
    transition: all cubic-bezier(0.4, 0, 0.2, 1) 300ms;
    fill: #FFF1A1;
  }

  .svg_chevron {
    width: 100%;
    height: auto;
  }

  .panelContainerClosed {
    transition: all 200ms;
    overflow: hidden;
  }

  .panelContainerOpen {
    transition: all 200ms;
    height: 100%;
  }

  .inactivePanel {
    transition: all 400ms;
    opacity: 0;
    height: 0;
    max-height: 0;
    overflow: hidden;
    color: #201616;
    background-color: #E0D9DD;
    padding: 0 2rem;
  }

  .activePanel {
    transition: all 400ms;
    opacity: 100%;
    height: auto;
    max-height: auto;
    color: #201616;
    background-color: #E0D9DD;
    padding: 2rem;
  }

</style>