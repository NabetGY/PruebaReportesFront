<template>
  <q-stepper v-model="step" vertical color="primary" animated>
    <q-step :name="1" title="Nuevo Evento" icon="settings" :done="step > 1">
      <form>
        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.titulo"
          label="Titulo del Reporte:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.categoria"
          label="Categoria:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.prioridad"
          label="Prioridad."
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.puestoSeguridad"
          label="Puesto de Seguridad:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.creadoPor"
          label="Reporte creado por:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.fechaInicio"
          label="Fecha de comienzo:"
        >
          <template v-slot:prepend>
            <q-icon name="event" class="cursor-pointer">
              <q-popup-proxy
                cover
                transition-show="scale"
                transition-hide="scale"
              >
                <q-date
                  v-model="EventoForm.fechaInicio"
                  mask="YYYY-MM-DDTHH:mm:ss.SSSZ"
                >
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Close" color="primary" flat />
                  </div>
                </q-date>
              </q-popup-proxy>
            </q-icon>
          </template>

          <template v-slot:append>
            <q-icon name="access_time" class="cursor-pointer">
              <q-popup-proxy
                cover
                transition-show="scale"
                transition-hide="scale"
              >
                <q-time
                  v-model="EventoForm.fechaInicio"
                  mask="YYYY-MM-DDTHH:mm:ss.SSSZ"
                  format24h
                >
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Close" color="primary" flat />
                  </div>
                </q-time>
              </q-popup-proxy>
            </q-icon>
          </template>
        </q-input>

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.cerradoPor"
          label="Reporte cerrado por:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.fechaFin"
          label="Fecha final:"
        >
          <template v-slot:prepend>
            <q-icon name="event" class="cursor-pointer">
              <q-popup-proxy
                cover
                transition-show="scale"
                transition-hide="scale"
              >
                <q-date
                  v-model="EventoForm.fechaFin"
                  mask="YYYY-MM-DDTHH:mm:ss.SSSZ"
                >
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Close" color="primary" flat />
                  </div>
                </q-date>
              </q-popup-proxy>
            </q-icon>
          </template>

          <template v-slot:append>
            <q-icon name="access_time" class="cursor-pointer">
              <q-popup-proxy
                cover
                transition-show="scale"
                transition-hide="scale"
              >
                <q-time
                  v-model="EventoForm.fechaFin"
                  mask="YYYY-MM-DDTHH:mm:ss.SSSZ"
                  format24h
                >
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Close" color="primary" flat />
                  </div>
                </q-time>
              </q-popup-proxy>
            </q-icon>
          </template>
        </q-input>

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.coordenadas"
          label="Posicion GPS:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.mapaUrl"
          label="Imagen en el Mapa:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.tipoEvento"
          label="Tipo de Evento:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="EventoForm.tipoEventoImagen"
          label="Imagen de evento:"
        />

        <div class="q-gutter-sm">
          <q-toggle
            :label="`Este Incidente tiene impacto ambiental o lesión menor
            (Primer auxilio en sitio o casos no registrables por salud ocupaciuonal)? ${confirmacion(
              EventoForm.impacto
            )}`"
            color="green"
            v-model="EventoForm.impacto"
            left-label
          />
        </div>
      </form>

      <q-stepper-navigation>
        <q-btn @click="step = 2" color="primary" label="Continue" />
      </q-stepper-navigation>
    </q-step>

    <q-step
      :name="2"
      title="Generar aviso en SAP PM"
      icon="create_new_folder"
      :done="step > 2"
    >
      <form>
        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.ubicacionTecnica"
          label="Ubicacion tecnica:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.ubicacionTecnicaImg"
          label="Imagen de ubicacion tecnica:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.parteObjectoAfectada"
          label="Parte objecto afectada:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.parteObjectoAfectadaImg"
          label="Imagen de Parte objecto afectada:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.modoFalla"
          label="Modo de falla:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.modoFallaImg"
          label="Imagen de Modo de falla:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.descripcionCorta"
          label="Descripcion corta:"
        />

        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoSapPmForm.fechaIncioAveria"
          label="Fecha de inicio de la averia:"
        >
          <template v-slot:prepend>
            <q-icon name="event" class="cursor-pointer">
              <q-popup-proxy
                cover
                transition-show="scale"
                transition-hide="scale"
              >
                <q-date
                  v-model="AvisoSapPmForm.fechaIncioAveria"
                  mask="YYYY-MM-DDTHH:mm:ss.SSSZ"
                >
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Close" color="primary" flat />
                  </div>
                </q-date>
              </q-popup-proxy>
            </q-icon>
          </template>

          <template v-slot:append>
            <q-icon name="access_time" class="cursor-pointer">
              <q-popup-proxy
                cover
                transition-show="scale"
                transition-hide="scale"
              >
                <q-time
                  v-model="AvisoSapPmForm.fechaIncioAveria"
                  mask="YYYY-MM-DDTHH:mm:ss.SSSZ"
                  format24h
                >
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Close" color="primary" flat />
                  </div>
                </q-time>
              </q-popup-proxy>
            </q-icon>
          </template>
        </q-input>

        <div class="q-gutter-sm">
          <q-toggle
            :label="`El equipo continua operando?: ${confirmacion(
              AvisoSapPmForm.equipoContinuaOperando
            )}`"
            color="green"
            v-model="AvisoSapPmForm.equipoContinuaOperando"
            left-label
          />

          <q-toggle
            :label="`El Modo de Falla puede ser solucionado a través de un BEC Por Operaciones?: ${confirmacion(
              AvisoSapPmForm.solucionadoPorBEC
            )}`"
            color="green"
            v-model="AvisoSapPmForm.solucionadoPorBEC"
            left-label
          />
        </div>
      </form>

      <q-stepper-navigation>
        <q-btn @click="step = 3" color="primary" label="Continue" />
        <q-btn
          flat
          @click="step = 1"
          color="primary"
          label="Back"
          class="q-ml-sm"
        />
      </q-stepper-navigation>
    </q-step>

    <q-step
      :name="3"
      title="Registrar numero de aviso Y2"
      icon="assignment"
      :done="step > 3"
    >
      <form>
        <q-input
          class="q-mb-md"
          outlined
          v-model="AvisoY2.numeroAvisoY2"
          label="Numero de aviso Y2:"
        />

        <div class="q-gutter-sm">
          <q-toggle
            :label="`Se corrigió por Mantenimiento?: ${confirmacion(
              AvisoY2.corregidoPorMantenimiento
            )}`"
            color="green"
            v-model="AvisoY2.corregidoPorMantenimiento"
            left-label
          />
        </div>
      </form>
      <q-stepper-navigation>
        <q-btn @click="step = 4" color="primary" label="Continue" />
        <q-btn
          flat
          @click="step = 2"
          color="primary"
          label="Back"
          class="q-ml-sm"
        />
      </q-stepper-navigation>
    </q-step>

    <q-step :name="4" title="Información de quien reporta" icon="add_comment">
      <form>
        <q-input
          class="q-mb-md"
          outlined
          v-model="firma.firmaImagen"
          label="Firma del reportante:"
        />
      </form>

      <q-stepper-navigation>
        <q-btn
          flat
          @click="step = 3"
          color="primary"
          label="Back"
          class="q-ml-sm"
        />

        <q-btn
          type="summit"
          flat
          label="Guardar"
          color="primary"
          @click="saveData()"
          v-close-popup
        />
      </q-stepper-navigation>
    </q-step>
  </q-stepper>
</template>

<script setup lang="ts">
import { useQuasar } from 'quasar';
import { ref } from 'vue';
import { api } from 'src/boot/axios';

const $q = useQuasar();

const EventoForm = ref({
  titulo: '',
  categoria: '',
  prioridad: '',
  puestoSeguridad: '',
  creadoPor: '',
  fechaInicio: '',
  cerradoPor: '',
  fechaFin: '',
  coordenadas: '',
  mapaUrl: '',
  tipoEvento: '',
  tipoEventoImagen: '',
  impacto: false,
});

const AvisoSapPmForm = ref({
  eventoId: '',
  ubicacionTecnica: '',
  ubicacionTecnicaImg: '',
  parteObjectoAfectada: '',
  parteObjectoAfectadaImg: '',
  modoFalla: '',
  modoFallaImg: '',
  descripcionCorta: '',
  fechaIncioAveria: '',
  equipoContinuaOperando: false,
  solucionadoPorBEC: false,
});

const AvisoY2 = ref({
  idEvento: '',
  numeroAvisoY2: 0,
  corregidoPorMantenimiento: false,
});

const firma = ref({
  eventoId: '',
  firmaImagen: '',
});

const step = ref(1);

const saveData = async () => {
  const eventoResponse = await api.post(
    '/reportes/save_evento',
    EventoForm.value
  );

  AvisoSapPmForm.value.eventoId = eventoResponse.data.id;

  await api.post('/reportes/save_aviso_sap_pm', AvisoSapPmForm.value);

  AvisoY2.value.idEvento = eventoResponse.data.id;

  await api.post('/reportes/save_aviso_y2', AvisoY2.value);

  firma.value.eventoId = eventoResponse.data.id;

  await api.post('/reportes/save_firma', firma.value);

  $q.notify({
    color: 'positive',
    position: 'top',
    message: 'Reporte Creado',
  });
};

const confirmacion = (value: boolean) => {
  return value ? 'SI' : 'NO';
};
</script>
