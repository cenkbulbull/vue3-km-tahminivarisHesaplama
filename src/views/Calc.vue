<template>
	<div class="row">
		<form @submit.prevent="hesapla" class="col s12">
			<div class="row">
				<div class="input-field col s6">
					<i class="material-icons prefix">location_on</i>
					<input v-model="start" id="icon_prefix" type="text" class="validate">
					<label for="icon_prefix">Başlangıç Adresi</label>
				</div>
				<div class="input-field col s6">
					<i class="material-icons prefix">location_on</i>
					<input v-model="finish" id="icon_telephone" type="tel" class="validate">
					<label for="icon_telephone">Varış Adresi</label>
				</div>
				<div class="input-field col s12">
					<button class="waves-effect waves-light btn-small">Hesapla</button>
				</div>
			</div>
		</form>
	</div>
	<Transition name="fade">
		<div v-if="result" class="row">
			<div class="col s12">
				<div class="card blue-grey darken-1">
					<div class="card-content white-text">
						<b><a class="btn-floating pulse"><i class="material-icons">chevron_right</i></a> {{km}} KM </b>
						<b><a class="btn-floating pulse"> <i class="material-icons">access_time</i></a> {{time}}</b>
					</div>
					<div id="map">
						<img :src="mapSrc">
					</div>
				</div>
			</div>
		</div>
	</Transition>

	
</template>
<script>

	import {ref} from "vue"
	import axios from "axios"
	export default{


		setup(){
			const start=ref("")
			const finish=ref("")
			const km=ref("")
			const time=ref("")
			const result=ref(false)
			const apikey="WGRD5GtZHvJgk0MiYRA5stg4V4MjLl0z"
			const mapSrc=ref("")

			const hesapla = async()=>{
				if (start.value!="" && finish.value!="") {
					axios.get(`http://www.mapquestapi.com/directions/v2/route?key=${apikey}&from=${start.value}&to=${finish.value}`)
					.then(res =>{
					//console.log(res.data.route)
					km.value=(res.data.route.distance*1.6).toFixed() //mil km dönüştürme
					var minute = res.data.route.realTime / 60
					if (minute>60) {
						var hour = minute / 60
						time.value=hour.toFixed() + ' ' + 'saat'
					}else{
						time.value=minute.toFixed() + ' ' + 'dakika'
					}
					result.value=true
					mapSrc.value=`https://www.mapquestapi.com/staticmap/v5/map?start=${start.value}&end=${finish.value}&size=260,150@2x&key=${apikey}`
					})
				}else{
					alert("Lütfen başlangıç adresi ve varış adresi bilgilerini doldurun")
				}
			}

			return {start,finish,km,time,result,apikey,mapSrc,hesapla}
		}
	}
</script>
<style>
	body{
		overflow: hidden;
	}
	.row{
		margin-top: 10px;
		text-align: center;
	}
	.card{
		margin-top: -13px;
		margin-left: 25%;
		width: 50%;
	}
	.fade-enter-active,
	.fade-leave-active {
		transition: opacity 0.5s ease;
	}

	.fade-enter-from,
	.fade-leave-to {
		opacity: 0;
	}
</style>