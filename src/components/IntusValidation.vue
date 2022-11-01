<script setup>

import {ref} from "vue";
import intus from "intus";
import {isMax, isMin, isRequired} from "intus/rules";

const form = ref({
  name: "",
  ingredients: [],
  description: "",
});

const errors = ref({});

function onAddIngredient() {
  form.value.ingredients.push({
    name: "",
    qty: null,
  });
}

function onRemoveIngredient(index) {
  form.value.ingredients.splice(index, 1);
}

function onSubmit() {
  // validation rules:
  // name is required, min 3
  // ingredients are required
  // ingredient name is required
  // ingredient qty is required and min 1
  // description is max 255
  let validation = intus.validate(
    form.value,
    {
      name: [isRequired(), isMin(3)],
      ingredients: [isRequired()],
      "ingredients.*.name": [isRequired()],
      "ingredients.*.qty": [isRequired(), isMin(1)],
      description: [isMax(255)],
    },
    {
      "ingredients.*.name": "name",
      "ingredients.*.qty": "qty",
      "name.isRequired": "Name is super super required.",
    }
  );

  errors.value = validation.errors();

  if(validation.passes()) {
    ///
  }
}
</script>

<template>
  <div class="rounded bg-white p-5">
    <h1 class="font-bold">Create recipe</h1>

    <form
      class="mt-4"
      @submit.prevent="onSubmit"
    >
      <div class="mb-6">
        <label
          class="mb-1"
          required
          >Name
        </label>
        <input
          v-model="form.name"
          :error="errors.name"
          placeholder="Recipe name"
        />
      </div>

      <div class="mb-6">
        <label
          class="mb-1"
          required
          >Ingredients
        </label>
        <p v-if="errors.ingredients"
          >{{ errors.ingredients }}
        </p>

        <div class="mb-2 space-y-2.5">
          <div
            v-for="(ingredient, index) in form.ingredients"
            :key="index"
            class="flex gap-2.5"
          >
            <div class="flex-1">
              <input
                v-model="ingredient.name"
                :error="errors[`ingredients.${index}.name`]"
                placeholder="Ingredient name"
              />
            </div>
            <div class="w-28">
              <input
                v-model="ingredient.qty"
                :error="errors[`ingredients.${index}.qty`]"
                placeholder="Qty"
                type="number"
              />
            </div>
            <div>
              <button @click="onRemoveIngredient(index)">
                Remove
              </button>
            </div>
          </div>
        </div>

        <button @click="onAddIngredient">
          Add ingredient
        </button>
      </div>

      <div>
        <label class="mb-1">Description</label>
        <textarea
          v-model="form.description"
          :error="errors.description"
          placeholder="What's the recipe about"
        />
      </div>

      <div class="mt-2 flex justify-end">
        <button type="submit">Save recipe</button>
      </div>
    </form>
  </div>
</template>
