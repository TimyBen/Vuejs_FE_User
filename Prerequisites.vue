<template>
    <div class="header">Điều kiện tiên quyết</div>
    <div class="note">
        <div id="note">You must complete the Quality Standard indicators to be able to unlock rewards</div>
    </div>
    <div class="condition_content" v-for="(items, key) in responesedata" :key="key">
        <div class="ctn">
            <div class="acceptance">
                <div class="txt">{{items.name}}</div>
                <v-btn @click="isOpen = true" class="more_info"><img src="../condition/info.svg"/></v-btn>
            </div>
            <!-- <div class="load_bar"><img src="../condition/load_bar.svg"/></div> -->
            <input class="load_bar" type="range" min="1" max="205" step="1" v-model="value">
        </div>
        <div class="estimate">
            <div class="odds">100%</div>
            <div class="checked">
                <img v-if="(items.status === 0)" src="../condition/not_checked.svg"/>
                <img v-else-if="(items.status === 1)" src="../condition/checked.svg"/>

            </div>
        </div>
    </div>
    <!-- <div>{{responesedata}}</div> -->
    <InfoModal :open='isOpen' @close='isOpen = !isOpen'>
        <div class="content">
        <keep-alive>
            <component v-bind:is="infoM"></component>
        </keep-alive>
        </div>
    </InfoModal>
</template>

<script>
import InfoModal from '@/components/InfoModal.vue'
import InfoM from '@/components/InfoM.vue'
import axios from 'axios'
const StandardStatAPI = 'https://apistg.ahamove.com/opstech/loyalty/supplier/pt/api/v1/supplier/stats?standard_group_id=1'
const token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhaGEiLCJ0eXAiOiJzdXBwbGllciIsImNpZCI6Ijg0Mzg3OTkwMDU1Iiwic3RhdHVzIjoiT0ZGTElORSIsImVvYyI6InZ1bGFAYWhhbW92ZS5jb20iLCJub2MiOiJMZSBBbmggVnUiLCJjdHkiOiJXQSIsImFjY291bnRfc3RhdHVzIjoiQUNUSVZBVEVEIiwicm9sZSI6ImFkbWluIiwicm9sZV9pZHMiOltdLCJleHAiOjE2MzQxMTYyMjQsInR5cGUiOiJ3ZWIiLCJpbWVpIjoid2ViIn0.CP7Bwq4f7CCTLLBvz0qnDPAG08jujq9PIoc5SLG_b_0'

export default {
  name: 'PreRequisites',
  data () {
    return {
      isOpen: false,
      infoM: 'InfoM',
      responesedata: {}
    }
  },
  components: { InfoModal, InfoM },
  methods: {
    async fetchApi () {
      await axios.get(StandardStatAPI, {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
        .then((response) => {
          this.responesedata = response.data.data.standard
        })
        .catch((error) => {
          console.log(error)
        })
    }
  },
  mounted () {
    this.fetchApi()
  }

}

</script>

<style>
.header {
    padding: 18px;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
    text-align: center;
    color: #1A1A1A;
}

.note {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 16px;
    /* width: 100%; */
    text-align: left;
    color: #1A1A1A;
    padding: 5px;
    /* align-content: stretch; */
}

#note {
    white-space: pre-line;
    display: flex;
    padding-left: 8px;
}

.condition_content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 5px;
    padding-bottom: 5px;
    padding-right: 5px;
    padding-left: 12px;
    background: #FFFFFF;
    border: 0.2px solid #e4e9f0b6;
}

.content {
    /* position: relative; */
}
.acceptance {
    display: flex;
    align-items: center;
}

.txt {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 20px;
    color: #121619;
}

.more_info {
    padding-left: 5px;
}

.estimate {
    width: 55px;
    height: 56px;
    background: #EEF0F3;
    display:flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.odds {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 14px;
    align-items: center;
    text-align: center;
    color: #121619;
    padding-top: 5px;
}

.load_bar {
    position: relative;
}
.load_bar_sp {
    position: absolute;
    left: 0;
    top: 10px;
}

.checked{

}
</style>
