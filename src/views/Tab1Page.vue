<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>

          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
      <div v-text="teste.estaCarregando"></div>
      <div v-text="teste.porcentagem"></div>

      <ExploreContainer name="Tab 1 page" />
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { ref, onMounted, watch } from 'vue';
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';
import { Device } from '@capacitor/device';

export default defineComponent({
  name: 'Tab1Page',
  components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },

  setup() {


    let Bateria = {
      estaCarregando: false,
      porcentagem: 0
    }

    let teste = ref(Bateria);

    const logBatloteryInfo = async () => {
      const info = await Device.getBatteryInfo();
      console.log(info);
      teste.value.estaCarregando = !!info.isCharging;
      teste.value.porcentagem = info.batteryLevel !==undefined ? info.batteryLevel :0;
    
    }
    onMounted(logBatloteryInfo);
    return {
      //retornas coisas para o frontend aqui
      teste,
    };
  }


});
</script>
