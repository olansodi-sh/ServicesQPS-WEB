<script setup lang="ts">
import { ref } from 'vue';
import GenericEditForm from '../shared/views/GenericEditForm.vue';
import { ExtrasServices } from './extras.services';
import { useToast } from 'primevue';
import { showToast } from '../../utils/show-toast';
import { useRoute } from 'vue-router';
import type { InputConfig } from '../../interfaces/input-config.interface';

const toast = useToast();
const route = useRoute();
const extraId = route.params.id as string;

const breadcrumbRoutes = [
  { label: 'Extras', to: { name: 'extras-default' } },
  { label: 'Edit', to: { name: 'extras-edit' } },
];

const inputs: InputConfig[] = [
  { label: 'Item', inputId: 'item', inputType: 'input' },
  { label: 'Item Price', inputId: 'itemPrice', inputType: 'numeric' },
  { label: 'Commission', inputId: 'commission', inputType: 'numeric' },
];

const initialData = {
  item: '',
  itemPrice: 0,
  commission: 0,
};

const loadData = async (id: string) => {
  const extra = await ExtrasServices.getExtraById(id);
  return {
    ...extra,
  };
};

const updateEntity = async (id: string, data: any) => {

  await ExtrasServices.updateExtra(id, data);

};
</script>

<template>
  <GenericEditForm :breadcrumb-routes="breadcrumbRoutes" view-title="Edit Extra" :inputs="inputs" :load-data="loadData"
    :update-entity="updateEntity" :initial-data="initialData" />
</template>