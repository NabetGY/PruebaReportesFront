<template>
  <div class="q-pa-md">
    <q-table title="Treats" :rows="rows" :columns="columns" row-key="title">
      <template v-slot:top>
        <q-btn color="primary" label="Agregar Reporte" @click="crear = true" />
        <q-space />
        <!-- <q-input borderless dense debounce="300" color="primary" v-model="filter">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input> -->
      </template>
    </q-table>

    <q-dialog v-model="crear">
      <q-card style="width: 700px; max-width: 80vw">
        <q-card-section>
          <div class="text-h6">Crear Reporte</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <CrearComponent />
        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script setup>
import { api } from 'src/boot/axios';
import { ref } from 'vue';
import CrearComponent from './CrearComponent.vue';

const columns = [
  {
    name: 'titulo',
    required: true,
    label: 'Titulo',
    align: 'left',
    field: (row) => row.titulo,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: 'categoria',
    align: 'center',
    label: 'Categoria',
    field: 'categoria',
    sortable: true,
  },
  { name: 'prioridad', label: 'Prioridad', field: 'prioridad', sortable: true },
  {
    name: 'puestoSeguridad',
    label: 'Puesto Seguridad',
    field: 'puestoSeguridad',
  },
  { name: 'creadoPor', label: 'Creado Por', field: 'creadoPor' },
  { name: 'cerradoPor', label: 'cerrado Por', field: 'cerradoPor' },
  {
    name: 'fechaInicio',
    label: 'Fecha Inicio',
    field: 'fechaInicio',
    sortable: true,
  },
  {
    name: 'fechaFin',
    label: 'Fecha Fin',
    field: 'fechaFin',
    sortable: true,
  },

  {
    name: 'options',
    label: 'Opciones',
    field: 'options',
    sortable: false,
  },
];

const rows = ref([]);

const crear = ref(false);

const getData = async () => {
  const request = await api.get('/reportes');

  rows.value = request.data.eventos;
};

getData();
</script>
