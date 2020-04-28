<template>
    <div>
        <Header/>
        <div :style="{display: 'flex', width: '100%', height: '700px', flexDirection: 'column', margin: '0 auto'}">
            <div id="map"></div>
            
            <div class="view-1">
                <div class="location" v-show="hidden_t">
                    <div class="location-place">
                        <div class="location-place-block">
                            <input type="text" v-model="name_pos_start" placeholder="От:" class="location-place-input">
                        </div>
                        <div class="location-place-block">
                            <input type="text" v-model="name_pos_stop" placeholder="До:" class="location-place-input">
                        </div>
                    </div>
                    <div class="location-block">
                        <div class="location-place-block">
                            <input type="text" placeholder="Ваш номер" class="location-place-input">
                        </div>
                        <!-- <input type="text" placeholder="+7 (920)-123-45-67" class="location-block-input"> -->
                        <div class="location-block-flex">
                            <input type="checkbox" class="location-block-flex__input">
                            <div class="block-flex">
                                <div class="block-flex-text">Я принимаю условия "Соглашения на обработку персональных данных"</div>
                                <!-- <div class="block-flex-text--red">"Соглашения на обработку персональных данных"</div> -->
                            </div>
                        </div>
                        <div class="location-block-heading">Выберите количество мест:</div>
                        <div class="location-block-place">
                            <a href="#" class="location-block-place__item">1</a>
                            <a href="#" class="location-block-place__item">2</a>
                            <a href="#" class="location-block-place__item">3</a>
                            <a href="#" class="location-block-place__item">4</a>
                        </div>
                        <div class="location-block-heading">Стоимость поездки:</div>
                        <div class="location-flex">
                            <div class="location-flex-item">
                                <img src="wallet-filled-money-tool%20(1).png" alt="" class="location-flex-item-img">
                                <div class="location-flex-item-cost">40 руб.</div>
                            </div>
                            <div class="location-flex-item">наличными водителю</div>
                        </div>
                    </div>
                    <div @click="setStopGeoPosition" class="location-button">Заказать</div>
                </div>

                <div class="search" v-show="hidden_search" >
                    <div class="search-block">
                    <div class="search-block-text">Идет поиск водителя.</div>
                    <div class="search-block-text">Пожалуйста ожидайте</div>
                    <div class="search-block-car">
                        <img src="~@/assets/img/car.png" alt="car" class="search-block-car__img">
                    </div>
                    </div>
                    <a href="#" @click="hidden_search = !hidden_search, hidden_t = !hidden_t" class="search-button">Отменить заказ</a>
                </div>
            </div>
        
        </div>

        <div name='modal' id="modal_ag" v-show="modal">
            <div>
                <span :style="{color: '#fee63c'}">Нам не удается Вас найти!</span><br/>
                <span>Разрешите в настройках вашего устройства использование геолокации!</span>
                <button id="modal-router" type="button" @click="modal=false">Продолжить</button>
            </div>
      </div>
      <Footer/>
    </div>
</template>

<script>
  import axios from 'axios';
  import DG from '2gis-maps';
  import Header from '@/components/Header'
  import Footer from '@/components/Footer'

  export default {
    data() {
      return{
        pos_start: [],
        data_c: [],

        id_region: 0,
        sity: '',

        name_pos_start: '',
        id_start: 0,

        name_pos_stop: '',
        pos_stop: [],
        id_stop: 0,

        data_distance_start: {},
        data_distance_stop: {},

        map: '',

        hidden_t: false,

        modal: false,
        hidden_search: false,

        status: 'Идет загрузка..!',
      }
    },
    components: {
        Header,
        Footer
    },
    methods: {
          getPosition(position) {
              this.pos_start.push([position.coords.longitude, position.coords.latitude])
          },

          errorPosition(error) {
              this.modal = true;
          },

          setStartGeoPosition() {
              // id региона
              axios.get('http://catalog.api.2gis.ru/2.0/region/search?key=rubrmr0030&q=Курск&lang=ru&locale=ru_RU')
              .then(res => {
                  this.id_region = res.data.result.items[0].id
                  this.sity = res.data.result.items[0].name
              })

              let interval_data = setInterval(() => {

                  if (this.pos_start.length > 0) {
                      this.hidden_t = !this.hidden_t

                      this.map.setView([this.pos_start[0][1], this.pos_start[0][0]])
                      this.map.setZoom(17)

                      let icon = DG.icon({
                          iconUrl: 'https://d-assets.2gis.ru/markers/bigbullet.svg',
                          iconAnchor: [15, 30]
                      })	

                      DG.marker([this.pos_start[0][1], this.pos_start[0][0]], {icon: icon}).addTo(this.map);


                      clearInterval(interval_data);
                  }
              }, 1000)
              
              axios.get('http://catalog.api.2gis.ru/2.0/geo/search?key=rubrmr0030&region_id=73&point=36.143172%2C51.732346&type=building')
              .then(res => {
                  this.name_pos_start = res.data.result.items[0].full_name
                  this.id_start = res.data.result.items[0].id
              })
          },

          setStopGeoPosition() {
            if (this.name_pos_stop.length > 0) {
              this.hidden_search = !this.hidden_search
              this.hidden_t = !this.hidden_t

              let data = this.name_pos_stop.replace(/ /g, '+')

              axios.get(`http://catalog.api.2gis.ru/2.0/geo/search?key=rubrmr0030&q=${data}&region_id=73&fields=items.address.is_conditional`)
              .then(res => {
                  this.id_stop = res.data.result.items[0].id
                  this.name_pos_stop = res.data.result.items[0].full_name
                  axios.get(`http://catalog.api.2gis.ru/2.0/geo/get?key=rubrmr0030&id=${this.id_stop}&fields=items.geometry.centroid`)
                  .then(res_1 => {
                      this.pos_stop.push([Number(res_1.data.result.items[0].geometry.centroid.split(' ')[1].replace(/[^.\d]+/g,"")), Number(res_1.data.result.items[0].geometry.centroid.split(' ')[0].replace(/[^.\d]+/g,""))]) 

                      DG.marker([this.pos_stop[0][0], this.pos_stop[0][1]]).addTo(this.map);

                      this.map.setZoom(12)

                      let pos_center_1 = (Number(this.pos_start[0][0])+Number(this.pos_stop[0][1]))/2
                      let pos_center_2 = (Number(this.pos_start[0][1])+Number(this.pos_stop[0][0]))/2
                      
                      this.map.setView([pos_center_2, pos_center_1])
                  })
                  if (res.data.length) {
                      this.status = 'Загрузка завершена!'
                  }
              }) 

              let interval_data_stop = setInterval(() => {
                  if (this.pos_stop.length > 0) {
                      console.log(this.pos_start, this.pos_stop)

                      // для прода заменить имя города
                      axios.post(`http://catalog.api.2gis.ru/ctx/1.0/kursk/?key=rubrmr0030`, {
                          "locale": "ru",
                          "source": {
                              "name": this.name_pos_start,
                              "point": {
                              "lat": Number(this.pos_start[0][1]), 
                              "lon": Number(this.pos_start[0][0])
                              },
                              "object_id": this.id_start
                          },
                          "target": {
                              "name": this.name_pos_stop,
                              "point": {
                              "lat": Number(this.pos_stop[0][0]),
                              "lon": Number(this.pos_stop[0][1])
                              },
                              "object_id": this.id_stop
                          },
                          "purpose": "routeSearch",
                          "transport": [
                              "pedestrian",
                              "bus",
                              "trolleybus",
                              "tram",
                              "shuttle_bus",
                              "metro",
                              "suburban_train",
                              "funicular_railway",
                              "monorail",
                              "river_transport",
                              "cable_car",
                              "light_rail",
                              "premetro",
                              "light_metro",
                              "aeroexpress"
                          ]
                      })
                      .then(res => {
                          for (let i=0; i<res.data.length; i++) {
                              if (res.data[i].movements.length > 2) {
                                  this.data_distance_start[res.data[i].movements[0].distance] = res.data[i].movements[0].waypoint.navigation.to_name;
                              }
                          }

                          let station_start = this.data_distance_start[Math.min.apply(null, Object.keys(this.data_distance_start))]

                          axios.get(`http://catalog.api.2gis.ru/2.0/transport/station/search?key=rubrmr0030&q=${station_start}&region_id=73`)
                          .then((res_station_1) => {
                              let loc_1 = res_station_1.data.result.items[0].platforms[0].geometry.centroid.split(' ')[0].replace(/[^.\d]+/g,"")
                              let loc_2 = res_station_1.data.result.items[0].platforms[0].geometry.centroid.split(' ')[1].replace(/[^.\d]+/g,"")

                              DG.marker([loc_2, loc_1]).addTo(this.map);
                          })

                          console.log(station_start, 1)

                      })
                      .catch(err => {
                          console.log(err)
                      })


                      axios.post(`http://catalog.api.2gis.ru/ctx/1.0/kursk/?key=rubrmr0030`, {
                          "locale": "ru",
                          "source": {
                              "name": this.name_pos_stop,
                              "point": {
                              "lat": Number(this.pos_stop[0][0]),
                              "lon": Number(this.pos_stop[0][1])
                              },
                              "object_id": this.id_stop
                          },
                          "target": {
                              "name": this.name_pos_stop,
                              "point": {
                              "lat": Number(this.pos_start[0][1]), 
                              "lon": Number(this.pos_start[0][0])
                              },
                              "object_id": this.id_start
                          },
                          "purpose": "routeSearch",
                          "transport": [
                              "pedestrian",
                              "bus",
                              "trolleybus",
                              "tram",
                              "shuttle_bus",
                              "metro",
                              "suburban_train",
                              "funicular_railway",
                              "monorail",
                              "river_transport",
                              "cable_car",
                              "light_rail",
                              "premetro",
                              "light_metro",
                              "aeroexpress"
                          ]
                      })
                      .then(res => {
                          for (let i=0; i<res.data.length; i++) {
                              if (res.data[i].movements.length > 2) {
                                  this.data_distance_stop[res.data[i].movements[0].distance] = res.data[i].movements[0].waypoint.navigation.to_name;
                              }
                          }

                          let station_stop = this.data_distance_stop[Math.min.apply(null, Object.keys(this.data_distance_stop))]

                          axios.get(`http://catalog.api.2gis.ru/2.0/transport/station/search?key=rubrmr0030&q=${station_stop}&region_id=73`)
                          .then((res_station_1) => {
                              let loc_1 = res_station_1.data.result.items[0].platforms[0].geometry.centroid.split(' ')[0].replace(/[^.\d]+/g,"")
                              let loc_2 = res_station_1.data.result.items[0].platforms[0].geometry.centroid.split(' ')[1].replace(/[^.\d]+/g,"")

                              DG.marker([loc_2, loc_1]).addTo(this.map);
                          })
                      })
                      .catch(err => {
                          console.log(err)
                      })

                      clearInterval(interval_data_stop);
                  }
              }, 1000)
            } else {

            }
        },
    },
    mounted() {
        this.map = DG.map('map', {
            'center': [50.627393, 36.799845],
            'zoom': 13,
            'setView' : true,
            'enableHighAccuracy': true,
            'watch': true,
            'skin': 'light'
        })
        this.map.locate()

        
        if ("geolocation" in navigator) {
            navigator.geolocation.getCurrentPosition(this.getPosition, this.errorPosition);
        } else {
            console.log('Геолокация недоступна')
        }


        this.setStartGeoPosition()
        
    }
    
  }
</script>

<style scoped>
  .hidden {
    display: none;
  }

    @media (min-width: 1000px) and (max-width: 2800px) {
    #map {width: 100%; height: 700px}
    }

    @media only screen and (max-device-width: 500px)  {
    #map {width: 100%; height: 400px}
    #modal_ag div {width: 100% !important; display: flex; justify-content: center; flex-direction: column;}
    }

    #modal_ag {
        position: fixed;
        z-index: 9999;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, .5);
        display: flex;
        overflow: hidden;
        justify-content: center;
        flex-direction: column; 
        text-align: center;
    }

    #modal_ag div {
        width: 60%;
        margin: 0 auto;
    }

    #modal_ag div span{
        color: #fff;
        font-size: 22px;
        font-weight: 500;
    }

    #modal-router {
        padding: 10px 50px 10px 50px;
        background-color: #55ce63;
        border: none;
        border-radius: .25rem;
        font-size: 18px;
        margin-top: 20px;
        color: #fff;
    }

    .view-1 {
        width: 550px;
        height: auto;
        position: absolute;
        margin-top: 5%;
        margin-left: 5%;
    }

  .search {
  max-width: 687px;
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: 0 21px 18px rgba(6, 7, 7, 0.34);
  display: flex;
  flex-direction: column;
}

.search-block {
  padding-top: 30px;
  width: 100%;
  border-bottom: 1px solid #333F50;
}

.search-block-text {
  font-size: 37px;
  font-weight: bold;
  line-height: 44px;
  text-align: center;
  color: #333F50;
}

.search-block-car {
  margin-top: 40px;
  align-self: flex-start;
}

.search-button {
  text-decoration: none;
  display: block;
  width: 83%;
  height: 81px;
  text-align: center;
  transition: all 0.3s;
  line-height: 81px;
  background-color: #7F241E;
  font-weight: bold;
  font-size: 38px;
  border-radius: 10px;
  border: 1px solid #707070;
  box-shadow: rgba(0, 0, 0, 0.16);
  color: #ffffff;
  align-self: center;
  margin-top: 20px;
  margin-bottom: 20px;
  text-transform: uppercase;
}

.search-button:hover {
  color: #7F241E;
  border: 1px solid #7F241E;
  background-color: #ffffff;
}


.location {
  display: flex;
  flex-direction: column;
  width: 100%;
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: 0 21px 18px rgba(6, 7, 7, 0.34);
}

.location-place {
  display: flex;
  flex-direction: column;
}

.location-place-input::placeholder {
  font-weight: 100;
  font-size: 20px;
  padding-left: 20px;
  padding-right: 20px;
  color: #A3A3A3;
  width: 100%;
}

.location-place-input {
  width: 96%;
  padding: 10px 0px 10px 20px;
  border: 0;
  outline: 0;
  font-size: 18px;
}

.location-place-block {
  border-bottom: 1px solid #333F50;
  color: #333F50;
  font-size: 29px;
  font-weight: 100;
  width: 100%;
}

.location-block {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  border-bottom: 1px solid #333F50;
  /* margin-top: 20px; */
  /* padding-left: 40px; */
  padding-bottom: 20px;
  width: 100%;
}

.location-block-input::placeholder {
  font-weight: 100;
  font-size: 20px;
  padding-left: 20px;
  padding-right: 20px;
  color: #A3A3A3;
}

.location-block-input {
  width: 60%;
  padding: 5px;
  border: 1px solid #707070;
  border-radius: 10px;
  outline: 0;
  font-size: 20px;
  margin-left: 40px;
}

.location-block-flex {
  display: flex;
  margin: 20px auto 20px auto;
  /* margin-bottom: 20px; */
}

.block-flex {
  display: flex;
  flex-direction: column;
}

.block-flex-text {
  color: #116E77;
  font-size: 14px;
  font-weight: 100;
}

.block-flex-text--red {
  font-size: 14px;
  font-weight: 100;
  color: #7F241E;
}


.location-block-heading {
  color: #A3A3A3;
  font-weight: 100;
  font-size: 20px;
  margin-bottom: 10px;
  margin-top: 10px;
  margin-left: 40px;
}

.location-block-place {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  margin: 0 auto;
}

.location-block-place__item {
  width: 60px;
  height: 60px;
  text-align: center;
  line-height: 65px;
  border: 1px solid #707070;
  color: #000000;
  font-weight: 900;
  font-size: 50px;
  text-decoration: none;
  transition: all 0.3s;
  display: block;
}

.location-block-place__item:hover {
  background-color: #000000;
  color: #ffffff;
}

.location-block-place__item:not(:last-of-type) {
  margin-right: 40px;
}

.location-flex {
  display: flex;
  margin-left: 40px;
}

.location-flex-item {
  color: #333F50;
  font-size: 20px;
  font-weight: 100;
  display: flex;
}

.location-flex-item:first-of-type {
  padding-right: 95px;
  border-right: 2px solid #b4b4b4;
}

.location-flex-item:last-of-type {
  padding-left: 43px;
}

.location-flex-item-img {
  margin-right: 0px;
}

.location-flex-item-cost {
  color: #333F50;
  font-weight: 900;
  font-size: 25px;
}

.location-button {
  text-decoration: none;
  display: block;
  width: 83%;
  height: 51px;
  text-align: center;
  transition: all 0.3s;
  line-height: 51px;
  background-color: #116E77;
  font-weight: bold;
  font-size: 20px;
  border-radius: 10px;
  border: 1px solid #707070;
  box-shadow: rgba(0, 0, 0, 0.16);
  color: #ffffff;
  text-transform: uppercase;
  margin-bottom: 20px;
  margin-top: 20px;
  align-self: center;
}

.location-button:hover {
  background-color: #7F241E;
  cursor: pointer;
}
</style>

  




