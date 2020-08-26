<template>
  <v-container fluid>
    <v-card color="transparent" flat>
      <v-card-title v-if="userProfile.name !== '' && typeof userProfile !== 'undefined'">Olá {{ userProfile.name.split(' ')[0] }} {{ userProfile.name.split(' ').length > 1 ? userProfile.name.split(' ').reverse()[0] : '' }},</v-card-title>
      <v-card-text v-if="userProfile.isAdmin" class="pt-0 pb-0 red--text">CONTA ADMINISTRATIVA</v-card-text>
      <v-card-subtitle>Escolha uma opção para continuar...</v-card-subtitle>
    </v-card>
    <v-row align="stretch" justify="center">
      <v-col class="col-6 pl-6">
        <v-card hover color="#145991" link :to="(userProfile.isAdmin && userProfile.adminPermissions.rides) ? '/admin/rides' : '/rides'" :disabled="(userProfile.isAdmin && !userProfile.adminPermissions.rides) ? true : false">
          <v-card-title>
            <v-icon size="40" color="white">directions_car</v-icon>
          </v-card-title>
          <v-card-subtitle class="white--text">
            Carona Solidária
          </v-card-subtitle>
        </v-card>
      </v-col>
      <v-col class="col-6 pr-6">
        <v-card hover color="#85241D" link :to="(userProfile.isAdmin && userProfile.adminPermissions.parkeds) ? '/admin/parkeds' : '/parkeds'" :disabled="(userProfile.isAdmin && !userProfile.adminPermissions.parkeds) ? true : false">
          <v-card-title>
            <v-icon size="40" color="white">local_parking</v-icon>
          </v-card-title>
          <v-card-subtitle class="white--text">
            Estacione Aqui
          </v-card-subtitle>
        </v-card>
      </v-col>
      <v-col class="col-6 pl-6">
        <v-card hover color="#4F382F" link :to="(userProfile.isAdmin && userProfile.adminPermissions.garbageAds) ? '/admin/garbageAds' : '/garbageAds'" :disabled="(userProfile.isAdmin && !userProfile.adminPermissions.garbageAds) ? true : false">
          <v-card-title>
            <v-icon size="40" color="white">restore_from_trash</v-icon>
          </v-card-title>
          <v-card-subtitle class="white--text">
            Coleta
          </v-card-subtitle>
        </v-card>
      </v-col>
      <v-col class="col-6 pr-6">
        <v-card hover color="#275C29" link :to="(userProfile.isAdmin && userProfile.adminPermissions.organicAds) ? '/admin/organicAds' : '/organicAds'" :disabled="(userProfile.isAdmin && !userProfile.adminPermissions.organicAds) ? true : false">
          <v-card-title>
            <v-icon size="40" color="white">shopping_basket</v-icon>
          </v-card-title>
          <v-card-subtitle class="white--text">
            Orgânicos
          </v-card-subtitle>
        </v-card>
      </v-col>
    </v-row>
    <div class="text-body-2 pl-3 pt-2 pb-2">Mais informações</div>
    <v-row align="stretch" justify="center">
      <v-col class="col-6 pl-6">
        <v-card hover color="#545454" link @click="showPrefectureModal = true">
          <v-card-title>
            <v-icon size="40" color="white">account_balance</v-icon>
          </v-card-title>
          <v-card-subtitle class="white--text">
            Prefeitura
          </v-card-subtitle>
        </v-card>
      </v-col>
      <v-col class="col-6 pr-6">
        <v-card hover color="#545454" disabled link>
          <v-card-title>
            <v-icon size="40" color="white">add</v-icon>
          </v-card-title>
          <v-card-subtitle class="white--text">
            Em breve...
          </v-card-subtitle>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog v-model="showPrefectureModal">
      <v-card>
        <v-card-title class="headline">Prefeitura</v-card-title>
        <v-card-text>
          <p>SIC - Serviço de Informação ao Cidadão</p>
          <p>Seg. a Sex. das 8:00 as 17:00 horas</p>
          <v-list>
            <v-list-item-group color="primary">
              <v-list-item href="tel:01239799005">
                <v-list-item-icon>
                  <v-icon>phone</v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                  <v-list-item-title>Ligar</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
              <v-list-item href="mailto:administracao@monteirolobato.sp.gov.br">
                <v-list-item-icon>
                  <v-icon>email</v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                  <v-list-item-title>Enviar e-mail</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data() {
    return {
      showPrefectureModal: false
    }
  },
  computed: {
    ...mapState(['userProfile'])
  }
}
</script>
