<template>
    <footer class="footer">
      <div class="footer-block container outer-wrapper" :style="{marginLeft: '5%', marginRight: '5%'}">
          <div class="footer-block__flex">
              <div class="footer-block__item">
                  <div class="footer-block__heading">KRON AUTO</div>
                  <ul class="footer-list">
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Тарифы</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Новости</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Партнерство</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Карьера</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Контакты</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">FAQ</router-link></li>
                  </ul>
              </div>
              <div class="footer-block__item">
                  <div class="footer-block__heading">KRON SHIP</div>
                  <ul class="footer-list">
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Грузоперевозки</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Сервисы</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Партнерам</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Карьера</router-link></li>
                  </ul>
              </div>
              <div class="footer-block__item">
                  <div class="footer-block__heading">KRON FOOD</div>
                  <ul class="footer-list">
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Доставка еды</router-link></li>
                      <li class="footer-list__item"><router-link class="footer-list__link" to="">Партнерам</router-link></li>
                  </ul>
              </div>
          </div>
          <div class="footer-block__contacts">
              <img class="footer-block__img" src='~@/assets/img/logo-footer.png' alt="logo"/>
              <div class="footer-app">
                  <router-link to="" class="footer-app__link">
                      <img class="footer-app__img" src='~@/assets/img/kron-auto.png' alt="kron"/>
                      <p class="footer-app__kron">Доехать к нам<br/><span class="footer-app__heading">KRON AUTO</span></p>
                  </router-link>
                  <router-link to="" class="footer-app__link">
                      <img class="footer-img" src='~@/assets/img/apple-brands.svg' alt="apple"/>
                      <div class="footer-app__text">App Store</div>
                  </router-link>
                  <router-link to="" class="footer-app__link">
                      <img class="footer-img" src='~@/assets/img/google-play-brands.svg' alt="google"/>
                      <p class="footer-app__google">Google Play</p>
                  </router-link>
              </div>
              <div class="footer-social">
                  <router-link to="" class="footer-social__link">
                      <img src='~@/assets/img/vk-social-network-logo.png' alt="vk"/>
                  </router-link>
                  <router-link to="" class="footer-social__link">
                      <img class="footer-social__facebook" src='~@/assets/img/instagram_(1).png' alt="instagram"/>
                  </router-link>
                  <router-link to="" class="footer-social__link">
                      <img class="footer-social__facebook" src='~@/assets/img/facebook-logo.png' alt="facebook"/>
                  </router-link>
              </div>
          </div>
      </div>
      <div class="footer-line container outer-wrapper"></div>
      <div class="footer-copyrights container outer-wrapper" :style="{marginLeft: '5%', marginRight: '5%'}">
          <div class="footer-copyrights__item">
              <router-link class="footer-copyrights__link" to="">Условия использования</router-link>
              <router-link class="footer-copyrights__link" to="">Политика конфиденциальности</router-link>
          </div>
          <div class="footer-copyrights__item">
              <p class="footer-copyrights__text">{{new Date().getFullYear()}} KRON, LLC Все права защищены.</p>
          </div>
      </div>
      <div class="footer__block container outer-wrapper" :style="{marginLeft: '5%', marginRight: '5%'}">
          <div class="footer-pay">
              <img src='~@/assets/img/visa.png' alt="visa" class="footer-pay-img"/>
              <img class="footer-pay__img" src='~@/assets/img/mastercard_(1).png' alt="mastercard"/>
              <img src='~@/assets/img/mir.png' alt="mir" class="footer-pay-img"/>
          </div>
          <div class="footer-form">
              <form action="" class="footer-form-flex">
                  <input type="email" placeholder="Email" class="footer-form__input"/>
              </form>
              <router-link to="" class="footer-button">Подписаться на рассылку</router-link>
          </div>
      </div>
  </footer>
</template>

<style scoped>
.footer {
  background-image: url("~@/assets/img/footer-back.png");
  min-height: 664px;
}
@media only screen and (max-device-width: 480px) {
  .footer {
    min-height: 0;
  }
}

.footer-block {
  display: flex;
  padding-top: 78px;
}
@media only screen and (max-device-width: 480px) {
  .footer-block {
    padding-top: 50px;
  }
}

.footer-block__flex {
  display: flex;
  justify-content: space-between;
  flex: 1;
  margin-right: 5%;
}
@media only screen and (max-device-width: 480px) {
  .footer-block__flex {
    display: none;
  }
}

.footer-block__heading {
  margin-bottom: 12px;
  color: #ffffff;
  font-size: 22px;
  font-weight: bold;
}
@media only screen and (max-device-width: 480px) {
  .footer-block__heading {
    font-size: 20px;
  }
}
@media only screen and (max-device-width: 480px) {
  .footer-block__heading {
    font-size: 16px;
  }
}

.footer-list {
  list-style-type: none;
  padding: 0;
}

.footer-list__link {
  text-decoration: none;
  color: #ffffff;
  font-size: 16px;
  font-weight: bold;
  transition: all 0.5s;
}
@media only screen and (max-device-width: 480px) {
  .footer-list__link {
    font-size: 14px;
  }
}
@media only screen and (max-device-width: 480px) {
  .footer-list__link {
    font-size: 12px;
  }
}

.footer-list__link:hover {
  color: #344051;
}

.footer-list__item:not(:last-child) {
  margin-bottom: 15px;
}

.footer-app {
  display: flex;
  justify-content: flex-end;
}
@media (min-width: 500px) and (max-width: 1025px) {
  .footer-app {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    width: 100%;
    margin: 0;
  }
}
@media only screen and (max-device-width: 480px) {  
  .footer-app {
    width: 100%;
    flex-direction: column;
    align-items: center;
    order: 3;
    margin-top: 10%;
    justify-content: space-between;
  }
}

@media (min-width: 500px) and (max-width: 1250px) {
  .footer-app {
    width: 100%;
    flex-direction: column;
    align-items: center;
  }
  .footer-app__link {
    width: 30% !important;
    margin-bottom: 10px !important;
    height: 48px !important;
  }
  .footer-app__link:nth-child(2) {
    width: 30% !important;
    margin-bottom: 10px !important;
    height: 48px !important;
  }

  .footer-app__link:nth-child(2) {
    width: 30% !important;
    margin-bottom: 10px !important;
    height: 48px !important;
  }
}


.footer-app__link {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  text-decoration: none;
  width: 26%;
  height: auto;
  box-shadow: 1px 2px 0 rgba(6, 7, 7, 0.23);
  background-color: #344051;
  color: #f8f8f8;
  border-radius: 5px;
}
@media (min-width: 500px) and (max-width: 1025px)  {
  .footer-app__link {
    width: 50% !important;
    height: 46px !important;
    margin: 10px 0 0 0 ;
    
  }
  .footer-app__link:nth-child(2) {

    margin: 10px 0 0 0 !important;
  }
}
@media only screen and (max-device-width: 480px) {  
  .footer-app__link {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 50%;
    height: 40px;
    margin-bottom: 20px;
  }
}

.footer-app__link:nth-child(2) {
  margin-left: 2%;
  margin-right: 2%;
}
@media only screen and (max-device-width: 480px)  {
  .footer-app__link:nth-child(2) {
    margin-top: 20px;
    margin-bottom: 20px;
    margin-left: 0;
    margin-right: 0;
  }
}

.footer-app__link:last-child {
  width: 27%;
  height: auto;
}
@media only screen and (max-device-width: 480px)  {
  .footer-app__link:last-child {
    width: 50%;
    
  }
}
@media only screen and (max-device-width: 480px) {  
  .footer-app__link:last-child {
  width: 50%;
  height: 40px;
  }
}

@media only screen and (max-device-width: 480px) {  
  .footer-app__link:nth-of-type(2) {
    margin: 0;
    width: 50%;
    height: 40px;
    margin-bottom: 20px;
  }
}

.footer-app__text {
  color: #f8f8f8;
  font-size: 20px;
  font-weight: bold;
}
@media only screen and (max-device-width: 480px) {
  .footer-app__text {
    font-size: 20px;
  }
}
@media only screen and (max-device-width: 480px) {  .footer-app__text {
    font-size: 14px;
    padding: 0;
  }
}

.footer-app__google {
  color: #f8f8f8;
  font-size: 20px;
  font-weight: bold;
}
@media only screen and (max-device-width: 480px) {
  .footer-app__google {
    font-size: 16px;
  }
}
@media only screen and (max-device-width: 480px) {  .footer-app__google {
    font-size: 14px;
    padding: 0;
  }
}

.footer-app__kron {
  color: #f8f8f8;
  font-size: 14px;
  font-weight: bold;
}
@media only screen and (max-device-width: 480px) {
  .footer-app__kron {
    font-size: 13px;
  }
}
@media only screen and (max-device-width: 480px) {  .footer-app__kron {
    font-size: 10px;
    padding-top: 0;
  }
}

.footer-app__img {
  width: 24px;
  height: auto;
}
@media only screen and (max-device-width: 480px) {  .footer-app__img {
    margin: 0;
    width: 14%;
    height: auto;
  }
}

.footer-img {
  filter: invert(1);
  width: 17%;
  height: auto;
}
@media only screen and (max-device-width: 480px) {  
  .footer-img {
    margin: 0;
    width: 14%;
    height: auto;
  }
}

.footer-app__heading {
  font-size: 18px;
}
@media only screen and (max-device-width: 480px) {
  .footer-app__heading {
    font-size: 14px;
  }
}
@media only screen and (max-device-width: 480px) {  .footer-app__heading {
    font-size: 12px;
  }
}

.footer-block__contacts {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  flex: 1;
}
@media only screen and (max-device-width: 480px) {  .footer-block__contacts {
    flex-direction: row;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    width: 100%;
  }
}

.footer-block__img {
  width: 30%;
  margin-bottom: 48px;
}

@media only screen and (max-device-width: 480px) {  .footer-block__img {
    width: 130px;
    margin: 0 auto;
  }
}

.footer-social {
  display: flex;
  margin-top: 41px;
}
@media only screen and (max-device-width: 480px) { 
   .footer-social {
    margin: 0 auto;
  
  }
}

.footer-social__link {
  display: block;
  width: 36px;
  height: 36px;
  box-shadow: 2px 3px 4px rgba(6, 7, 7, 0.09);
  border-radius: 10px;
  background-color: #343f51;
  text-align: center;
  line-height: 36px;
}

.footer-social__link:not(:first-child) {
  margin-left: 18px;
}

.footer-social__facebook {
  padding-top: 7px;
}

.footer-line {
  border: 1px solid #344051;
  margin-top: 22px;
  margin-bottom: 27px;
}
@media only screen and (max-device-width: 480px) {  
  .footer-line {
    display: none;
  }
}

.footer-copyrights__link {
  display: block;
  color: #ffffff;
  font-size: 16px;
  font-weight: bold;
  text-decoration: none;
  height: 24px;
}
@media only screen and (max-device-width: 480px)  {
  .footer-copyrights__link {
    color: #000000;
  }
}
@media only screen and (max-device-width: 480px) {  .footer-copyrights__link {
    color: #ffffff;
  }
}

.footer-copyrights__link:first-child {
  border-right: 1px solid #ffffff;
  padding-right: 10px;
}
@media only screen and (max-device-width: 480px) {  .footer-copyrights__link:first-child {
    padding: 0;
    border: 0;
  }
}

.footer-copyrights__link:last-child {
  padding-left: 10px;
}

.footer-copyrights__item {
  display: flex;
}
@media only screen and (max-device-width: 480px) {  .footer-copyrights__item {
    flex-direction: column;
    align-items: center;
    color: #ffffff;
  }
}

.footer-copyrights__link:hover {
  color: #344051;
}

.footer-copyrights {
  display: flex;
  justify-content: space-between;
}
@media only screen and (max-device-width: 480px) {  
  .footer-copyrights {
    /* margin-top: 70px; */
    flex-direction: column;
    align-items: center;
  }
}

.footer-copyrights__text {
  color: #ffffff;
  font-size: 16px;
  font-weight: bold;
  text-decoration: none;
  margin: 0;
}


@media only screen and (max-device-width: 480px) {  
  .footer-copyrights__text {
    color: #ffffff;
    margin-top: 12%;
    margin-bottom: 44%;
    text-align: center;
  }
}

.footer__block {
  margin-top: 10%;
  display: flex;
  justify-content: space-between;
}
@media (min-width: 500px) and (max-width: 1024px) {
  .footer__block {
    margin-top: 30% !important;
  }
}

@media only screen and (max-device-width: 480px) {  
  .footer__block {
    flex-direction: column;
    align-items: center;
    margin-top: 152px;
  }
}

.footer-pay {
  display: flex;
}
@media (max-width: 810px) {
  .footer-pay {
    display: none;
  }
}
@media only screen and (max-device-width: 480px) {  .footer-pay {
    display: flex;
    order: 2;
    margin-top: 20px;
    justify-content: space-between;
    padding-bottom: 1%;
    margin-bottom: 20px;
  }
}

.footer-pay__img {
  margin-left: 27px;
  margin-right: 31px;
}
@media only screen and (max-device-width: 480px) {  .footer-pay__img {
    margin: 0;
    width: 18%;
  }
}

.footer-form__input {
  background-color: transparent;
  font-size: 18px;
  font-weight: 400;
  /* padding-left: 3%;
  padding-right: 3%; */
  width: 100%;
  /* height: 36px; */
  border-radius: 5px;
  border: 2px solid #576476;
  outline: none;
  color: #ffffff;
  padding: 4.5%;
}
@media only screen and (max-device-width: 480px) {  
  .footer-form__input {
    width: 100%;
    height: 30px;
    font-size: 16px;
    border: 2px solid #576476;
  }
}

.footer-form__input::placeholder {
  color: #ffffff;
}

.footer-button {
  display: block;
  width: 69%;
  /* height: 100%; */
  box-shadow: 2px 3px 7px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  background-color: #576476;
  color: #ffffff;
  font-size: 18px;
  font-weight: 400;
  text-decoration: none;
  text-align: center;
  line-height: 35px;
  transition: all 0.5s;
  margin-left: 10%;
  padding: 1.5px;

}
@media only screen and (max-device-width: 480px) {  .footer-button {
    width: 55%;
    font-size: 12px;
    height: 30px;
    line-height: 30px;
  }
}

.footer-button:hover {
  background-color: #116e77;
}

.footer-form {
  display: flex;
}

.footer-form-flex {
  width: 40%;
}


.img__width {
  width: 110px;
  height: 35px;
}

.footer-block__item {
  width: 30%;
  margin-right: 30px;
}

.footer-pay-img {
  width: 24%;
  height: 86%;
}

/* Шапка ЛК */
.private-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 60px;
  background-color: #333F50;
}

.private-content {
  margin-left: 5%;
}

.private-content img {
  width: 110px;
  height: 35px;
}

.private-users-img {
  display: flex;
  margin-right: 5%;
}

.private-users-img img {
  border: 2px solid #fff;
  border-radius: 5px;
  width: 40px;
  height: 40px;
}

.user-data {
  display: flex;
  flex-direction: column;
  margin-right: 10px;
  text-align: right;
}

.user-name {
  font-size: 18px;
  color: #fff;
}

.status {
  font-size: 18px;
  color: #E6C633;
}

.text-menu {
  color: #fff;
  padding: 2%;
  margin-bottom: 10px;
  cursor: pointer;
  text-decoration: none;
}

#block-menu {
  background-color: #344051;
  width: 125px;
  height: 100px;
  padding: 10px;
  position: absolute;
  margin-top: 17px;
  display: none;
}

.logo-mobile {
  width: 110px;
  height: 35px;
  margin: 20px 0 0 15%;
}

.logo-mobile2 {
  width: 110px;
  height: 35px;
  margin: 20px 0 0 5%;
}

.header-mobile {
  width: 100%;
  height: 68px;
  margin-bottom: 10px;
}

.new-color-burger {
  background-color: #344051 !important;
}

.new-overlay {
  margin-top: 10px !important;
  position: fixed !important;
}

.new-bm-button {
  margin-top: -5px !important;
}

.mobile-menu__item:nth-child(n+2) {
  margin-top: 20px !important;
}

.menu__account {
  display: block;
  margin-left: auto;
  margin-right: 5%;
  margin-top: 10% !important;
  margin-bottom: 40px;
  text-decoration: none;
  width: 180px;
  height: 30px;
  box-shadow: 2px 3px 4px rgba(6, 7, 7, 0.09);
  border-radius: 10px;
  background-color: #922723;
  color: #ffffff;
  font-size: 18px;
  font-weight: bold;
  position: relative;
  padding-left: 60px;
  line-height: 36px;
  transition: all 0.5s;
  text-decoration: none;
}

.menu__account span {
  position: absolute;
  top: -2px;
  left: 57px;
}

.menu__account:hover {
  color: #fff;
  background-color: #344051;
  border-radius: 1px solid #922723;
}
</style>