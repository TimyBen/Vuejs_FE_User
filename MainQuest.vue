<template>
    <div class="ctn_hd">
        <v-btn class="arrow_btn">
            <img class="arrow_heading" src="/arrow_heading.svg"/>
        </v-btn>
        <div class="hd_challenge">
            <div class="title">Challenges</div>
        </div>
    </div>
    <nav class="nav">
        <div class="mainquest">
            <router-link class="main" to="/mainquest">Main Quest</router-link>
        </div>
        <div class="weeklychallenge">
            <router-link class="weekly" to="/weeklychallenge">Thử thách tuần</router-link>
        </div>
    </nav>
    <div class="progress-bar">
        <div class="container-box">
            <div class="progress-box" v-for="(num, key) in mile_stone" v-bind:key="key" :class="[num.supplier_result.result_status === 2 ? 'blue_outta' : ',']">
                <div class="progress-number" :class="[num.supplier_result.result_status === 0 ? 'orng' : ',' ,
                                                        num.supplier_result.result_status === 1 ? 'green' : ',' ,
                                                        num.supplier_result.result_status === 2 ? 'blue' : ','  ,
                                                        num.supplier_result.result_status === 3 ? 'red' : ',',
                                                        num.supplier_result.result_status === 4 ? 'red' : ',',
                                                        num.supplier_result.result_status === 5 ? 'grey' : ','  , ]">
                    <span class="num" >{{ num.milestone }}</span>
                    <img class="lock" v-if="(num.supplier_result.result_status === 0)" src="/Time.svg"/>
                    <img class="lock" v-else-if="(num.supplier_result.result_status === 1)" src="/checked.svg"/>
                    <img class="lock" v-else-if="(num.supplier_result.result_status === 3)" src="/error.svg"/>
                    <img class="lock" v-else-if="(num.supplier_result.result_status === 4)" src="/error.svg"/>
                    <img class="lock" v-else-if="(num.supplier_result.result_status === 5)" src="/lock.svg"/>
                </div>
            </div>
        </div>
        <div class="info-page">
            <div class="info">
                <div class="container-name-amount">
                    <div class="name">Timothy Benedict</div>
                    <div class="amount">đ170,000</div>
                </div>
                <div class="gifts">
                    <div class="remaining-gifts">số lượng quà còn lại</div>
                    <div class="qty">100</div>
                </div>
            </div>
            <div class="accumulated-points">
                <div class="accumulated">Accumulated Points</div>
                <div v-for="(num, key) in mile_stone" v-bind:key="key">
                <!-- <div v-if="(num.supplier_result.result_status === 1)" class="points">{{ num.milestone + 20 }}</div> -->
                </div>
            </div>
            <div class="loading-milestone">
                <!-- <div class="circle"><img src="circle.svg"></div> -->
                <!-- <div class="process_img"><img src="../progress_loader/loader_bar.svg"/></div> -->
                <div class="progress_loader_bar">
                  <div class="ms_loader"></div>
                </div>
                <!-- <input type="number" v-model="value"/> -->
            </div>
            <div class="msg_points">You must complete Quality<img src="/image.png"/>standard to receive a reward</div>
        </div>
        <div class="terms">
            <v-btn btn @click="show('term')">
            <div class="terms-box">
                <div class="img" id="term"><img src="/note_terms.svg"/></div>
                <div class="terms-condition">Cách tính điểm</div>
                <div class="arrow" id="terms-arrow"><img src="/arrow.svg"/></div>
            </div>
            </v-btn>
        </div>
        <div class="reward">
            <router-link class="router-link" to="RewardHistory">
                <div class="reward-history" id="RewardHistory">
                    <div class="img" id="reward"><img src="/clock.svg"/></div>
                    <div class="history">Lịch sử điểm thưởng</div>
                    <div class="arrow" id="reward-arrow"><img src="/arrow.svg"/></div>
                </div>
            </router-link>
        </div>
        <div class="prerequisites-box">
            <v-btn @click="show('prerequisites')" id="Prerequisites">
                <div class="prerequisites-container">
                    <div class="img" id="prerequisites"><img src="/medal.svg"/></div>
                    <div class="prerequisites">Điều kiện tiên quyết</div>
                    <div class="arrow" id="prerequisites-arrow"><img src="/arrow.svg"/></div>
                </div>
            </v-btn>
        </div>
        <div class="prerequisites-box">
            <v-btn @click="show('addeditem')" id="Prerequisites">
                <div class="prerequisites-container">
                    <div class="img" id="prerequisites"><img src="/medal.svg"/></div>
                    <div class="prerequisites">Xem thêm</div>
                    <div class="arrow" id="prerequisites-arrow"><img src="/arrow.svg"/></div>
                </div>
            </v-btn>
        </div>
        <!-- <div style="white-space: pre-line">get status : {{mile_stone}}</div> -->
        </div>
        <Modal :open='isOpen' @close='isOpen = !isOpen'>
            <div class="content_container">
            <keep-alive>
                <component v-bind:is="modalC"></component>
            </keep-alive>
            </div>
        </Modal>
</template>

<script>

import Modal from '@/components/Modal.vue'
import TermPage from '@/components/TermPage.vue'
import RewardHistory from '@/views/RewardHistory.vue'
import Prerequisites from '@/components/Prerequisites.vue'
import { Data2 } from '@/data/data.js'
import Slider from '@vueform/slider'
import infoDialog from '@/components/Info_dialog.vue'
// import axios from 'axios'
// const API1 = 'https://apistg.ahamove.com/opstech/loyalty/supplier/pt/api/v1/supplier/scheme/1'
// const API2 = 'https://apistg.ahamove.com/opstech/loyalty/supplier/pt/api/v1/supplier/point?scheme_id=1'
// const token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhaGEiLCJ0eXAiOiJzdXBwbGllciIsImNpZCI6Ijg0Mzg3OTkwMDU1Iiwic3RhdHVzIjoiT0ZGTElORSIsImVvYyI6InZ1bGFAYWhhbW92ZS5jb20iLCJub2MiOiJMZSBBbmggVnUiLCJjdHkiOiJXQSIsImFjY291bnRfc3RhdHVzIjoiQUNUSVZBVEVEIiwicm9sZSI6ImFkbWluIiwicm9sZV9pZHMiOltdLCJleHAiOjE2MzQxMTYyMjQsInR5cGUiOiJ3ZWIiLCJpbWVpIjoid2ViIn0.CP7Bwq4f7CCTLLBvz0qnDPAG08jujq9PIoc5SLG_b_0'

export default {
  name: 'MainQuest',
  data () {
    return {
      value: '',
      mile_stone: Data2,
      responsedata1: {},
      responsedata2: {},
      isActive: false,
      active_milestone: '',
      isOpen: false,
      modalC: {
        type: String
      },
      grey: false,
      blue: false,
      blue_outta: false,
      green: false,
      orng: false

    }
  },
  components: { Modal, TermPage, RewardHistory, Prerequisites, Slider, infoDialog },

  methods: {
    show: function (page) {
      this.isOpen = true
      switch (page) {
        case 'term':
          this.modalC = 'TermPage'
          break
        case 'prerequisites':
          this.modalC = 'Prerequisites'
          break
        case 'addeditem':
          this.modalC = 'infoDialog'
          break
      }
    }
  }
}
</script>

<style>
.ctn_hd {
    background: #142246;
    height: 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    /* flex-direction: row; */
    padding-left: 15px;
    padding-right: 15px;
}

.hd_challenge {
    display: flex;
    align-self: center;
    justify-content: center;
    width: 100%;
}

.title {
    font-style: normal;
    font-weight: 600;
    font-size: 3vh;
    text-align: center;
    display: flex;
    color: #FFFFFF;
}

.arrow_heading {
    display: flex;
    align-self: center;
    justify-content: center;
}

.arrow_btn {
    height: 18px;
}

.nav {
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 14px !important;
    background: #FFFFFF;
}

.main {
   color: #7A8189;
   text-decoration: none;
}

.mainquest {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 2vh;
    display: flex;
    color: #7A8189;
}

.weeklychallenge {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 2vh;
    display: flex;
}

.weekly {
    color: #FE5F00;
    text-decoration: none;
}
.progress-bar {
    padding-top: 1rem;
    display: flex;
    flex-direction: column;
    background: #FFFFFF;
}

.container-box {
    display: flex;
    width: 100%;
    gap: 20px;
    justify-content: space-between;
    background-color: #FFFFFF;
    padding-left: 10px;
    padding-right: 10px;

}

.progress-box {
    display: flex;
    width: 60px;
    height: 60px;
    justify-content: center;
    align-items: center;
}

.progress-number {
    height: 44px;
    width: 44px;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
}

.num {
    /* display: flex; */
    justify-content: center;
    align-self: center;
}

.lock {
    position: absolute;
    padding: 2px;
    /* gap: 10px; */
    width: 16px;
    height: 16px;
    background: #f2f4f837;
    border-radius: 50px;
    bottom: -5px;
    right: 0;
}

.info-page {
    display: flex;
    justify-content: center;
    background: linear-gradient(175.71deg, #ECF4FF 3.49%, #FFFFFF 151.98%);
    padding: 16px;
    flex-direction: column;
}
.info {
    /* Neutral/White */
    display: flex;
    width: 100%;
    justify-content: space-between;
    background: #FFFFFF;
    border-radius: 8px;
    gap: 10px;
    padding: 16px;
    box-shadow: 1px 2px 2px #dcdcdc;
}

.name {
    top: 10%;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 10px;
    /* identical to box height, or 160% */

    display: flex;
    letter-spacing: 0.5px;
    text-transform: uppercase;

    /* Neutral/Dark Grey */

    color: #7A8189;
}
.amount {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 20px;
    display: flex;
    color: #072553;
}
.remaining-gifts {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 10px;
    line-height: 16px;
    display: flex;
    align-items: center;
    letter-spacing: 0.5px;
    text-transform: uppercase;
    color: #7A8189;
}
.qty {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 20px;
    display: flex;
    color: #1A1A1A;
    justify-content: flex-end;
}

.progress_loader_bar {
  display: flex;
  width: 100%;
  height: 1ch;
  background-color: #C1C7CD;
}

.ms_loader {
  display: flex;
  width: 50%;
  height: 100%;
  background-color: #FA8C16;
}

.accumulated-points {
    display: flex;
    gap: 10px;
    padding-top:10px;
    padding-bottom:10px;
}

.accumulated {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 10px;
    line-height: 16px;
    display: flex;
    align-items: center;
    letter-spacing: 0.5px;
    text-transform: uppercase;
    color: #072553;
}

.points {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 20px;
    line-height: 32px;
    display: flex;
    align-items: center;
    color: #FE5F00;
}

#progress_load {
    width: 100%;
    height: 1.6rem;
    accent-color: #FE5F00;
    /* background-color: #A2A9B0; */
}

.circle {
    position: absolute;
    /* background: #FE5F00; */
    border-radius: 8px;
    /* left: 20%; */
    justify-content: center;
    align-items: center;
    display: flex;
}

.msg_points {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 500;
    font-size: 12px;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: #1A1A1A;
    padding-top: 10px;
}

.terms {
    padding-top: 5%;
}

.terms-box {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background: #FFFFFF;
}

.img * {
    height: 22px;
    width: 20px;
    display: flex;
}

.terms-condition {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
    color: #121619;
    flex-grow: 1;
    text-align: left;
    padding-left: 10px;
}

.reward {
    padding-top: 5%;
}
.reward-history {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background: #FFFFFF;
}

.router-link {
    text-decoration: none !important;
}

.history {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
    color: #121619;
    flex-grow: 1;
    text-align: left;
    padding-left: 10px;
}

.prerequisites-box {
    padding-top: 5%;
}
.prerequisites-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background: #FFFFFF;
}

.prerequisites {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
    color: #121619;
    flex-grow: 1;
    text-align: left;
    padding-left: 10px;
}

.arrow * {
    display: flex;
    height: 12px;
    width: 8.4px;
    justify-items: end;
}

.content_container {
    max-height: 500px;
    overflow-y: scroll;
}

.orng {
    border: 2px solid #FA8C16;
    background-color: #FFF7E6;
    border-radius: 100px
}
.green {
    border: 2px solid #2F855A;
    background-color: #F0FFF4;
    border-radius: 100px
}
.blue {
    border: 2px solid #0E4174;
    background-color: #F1F8FF;
    border-radius: 100px
}
.blue_outta {
    background: #ECF4FF;
}
.red {
    background-color:  #FFF1F0;
    border: 2px solid  #CF1322;
    border-radius: 100px
}
.grey {
    border: 2px solid #A2A9B0;
    background-color: #E6E9EC;
    border-radius: 100px
}
</style>
