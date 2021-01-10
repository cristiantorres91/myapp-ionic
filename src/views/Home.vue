<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar color="primary">
        <ion-title>App Users</ion-title>
        <ion-title class="ion-text-right" size="small">Cristian Torres</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true"> 
      <ion-list>
        <ion-list-header lines="inset">
          <ion-label>Users</ion-label>
        </ion-list-header>
      <div v-for="item in dataApi"  :key="item.id">
          <ion-item >
            <ion-avatar slot="start">
              <ion-icon style="color:#26a660" :icon="personCircleOutline" size="large"/>
            </ion-avatar>
            <ion-label>
              <h2>{{ item.name }}</h2>
              <h3>{{ item.email }}</h3>
            </ion-label>
          </ion-item>
        </div>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonList,
  IonListHeader,
  IonLabel,
  IonAvatar,
  IonItem,
  IonIcon,
} from "@ionic/vue";
import { defineComponent, ref, onMounted } from "vue";
import { personCircleOutline } from "ionicons/icons";
export default defineComponent({
  name: "Home",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonList,
    IonListHeader,
    IonLabel,
    IonAvatar,
    IonItem,
    IonIcon,
  },
  setup() {
    const dataApi = ref([]);
    //metodo para obtener la data de la api
    const getData = async () => {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );
        dataApi.value = await response.json();
        console.log(dataApi.value);
      } catch (error) {
        console.log(error);
      }
    };
    //llamamos metodo para cargar la data
    onMounted(() => {
      getData();
    });
    return {
      dataApi,
      getData,
      personCircleOutline
    };
  },
});
</script>

<style scoped>
</style>