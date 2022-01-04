<template>
	<div id="app" class="container-fluid">
		<h1>Animações</h1>

    <b-card>
      <transition name="fade" type="animation">
        <b-alert variant="info" show v-if="info" dismissible>{{ msg }}</b-alert>
      </transition>
    <b-button type="primary" @click="info = !info">Alert Infor</b-button>
    </b-card>
		
    <b-card>
      <transition name="slide" type="animation">
        <b-alert variant="success" show v-if="sucess" dismissible>{{ msg }}</b-alert>
      </transition>
    <b-button type="primary" @click="sucess = !sucess">Alert Sucess</b-button>
    </b-card>

    <b-card>
      <transition enter-active-class="animated bounce" leave-active-class="animated shake">
        <b-alert variant="danger" show v-if="danger" dismissible>Alert Danger</b-alert>
      </transition>
    <b-button type="primary" @click="danger = !danger">Alert Sucess</b-button>
    </b-card>

    <b-alert
      :show="dismissCountDown"
      dismissible
      variant="warning"
      @dismissed="dismissCountDown=0"
      @dismiss-count-down="countDownChanged"
    >
      <p>This alert will dismiss after {{ dismissCountDown }} seconds...</p>
      <b-progress
        variant="warning"
        :max="dismissSecs"
        :value="dismissCountDown"
        height="4px"
      ></b-progress>
    </b-alert>

    <b-button @click="showAlert" variant="info" class="m-1">
      Show alert with count-down timer
    </b-button>
    <b-button @click="showDismissibleAlert=true" variant="info" class="m-1">
      Show dismissible alert ({{ showDismissibleAlert ? 'visible' : 'hidden' }})
    </b-button>

    <hr>
    <b-button variant="primary" @click="componenteSelecionado = 'AlertInfo'">Info</b-button>
    <b-button variant="primary" @click="componenteSelecionado = 'AlertAdvertencia'">Advertencia</b-button>
    <hr>
    <transition name="fade" mode="out-in">
      <component :is="componenteSelecionado"></component>
    </transition>
    
	</div>
</template>

<script>
import AlertAdvertencia from './AlertAdvertencia.vue'
import AlertInfo from './AlertInfo.vue'
import alertMixin from './alertMixin'
export default {
  mixins: [alertMixin],
  components: {AlertAdvertencia, AlertInfo},
  data () {
    return {
      msg: 'SUCESSO!!!',
      info: false,
      sucess: false,
      danger: false,
      componenteSelecionado: 'AlertInfo'
    }
  },
}
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
	font-size: 1.5rem;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.fade-enter-active,.fade-leave-active {
  transition: opacity 2s;
}

@keyframes slide-in {
    from { transform: translateY(40px);}
    to { transform: translateY(0);}
}
@keyframes slide-out {
    from { transform: translateY(0);}
    to { transform: translateY(40px);}
}

.slide-enter-active {
  animation: slide-in 2s ease;
  transition: opacity 2s;
}
.slide-leave-active {
  animation: slide-out 2s ease;
  transition: opacity 2s;
}
.slide-enter, .slide-leave-to {
  opacity: 0;
}
</style>
