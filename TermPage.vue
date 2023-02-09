<template>
    <div class="header">Cách tính điểm</div>
    <div v-for="(item, key) in responesedata" :key="key" class="sieu-toc-box" id="content">
        <div><img class="sieu-img" :src="item.icon"></div>
        <div class="sieu-text">{{item.name}}</div>
        <div class="diem">{{item.point}} điểm</div>
    </div>
    <!-- <div v-for="(item, key) in dataser" :key="key">{{item}}</div> -->
    <!-- <div>{{responesedata}}</div> -->
</template>

<script>
// import { ServiceData } from '@/data/data.js'
import axios from 'axios'
const API = 'https://apistg.ahamove.com/opstech/loyalty/supplier/pt/api/v1/service/'
const token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhaGEiLCJ0eXAiOiJzdXBwbGllciIsImNpZCI6Ijg0Mzg3OTkwMDU1Iiwic3RhdHVzIjoiT0ZGTElORSIsImVvYyI6InZ1bGFAYWhhbW92ZS5jb20iLCJub2MiOiJMZSBBbmggVnUiLCJjdHkiOiJXQSIsImFjY291bnRfc3RhdHVzIjoiQUNUSVZBVEVEIiwicm9sZSI6ImFkbWluIiwicm9sZV9pZHMiOltdLCJleHAiOjE2MzQxMTYyMjQsInR5cGUiOiJ3ZWIiLCJpbWVpIjoid2ViIn0.CP7Bwq4f7CCTLLBvz0qnDPAG08jujq9PIoc5SLG_b_0'

export default {
  name: 'TermPage',
  data () {
    return {
      responesedata: []
      // dataser: ServiceData
    }
  },
  methods: {
    async fetchApi () {
      await axios.get(API, {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
        .then((response) => {
          this.responesedata = response.data.data
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

/* .sieu-toc-box {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background: #FFFFFF;
    border: 0.2px solid #dbe4f0;
} */

#content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    background: #FFFFFF;
    border: 0.2px solid #e4e9f0b6;
}

.sieu-text {
    flex-grow: 1;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;
    color: #121619;
    text-align: left;
    padding-left: 20px;

}

.sieu-img {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  height: 2rem;
  width: 2rem;
}

/* .truck-text {
    flex-grow: 1;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;
    color: #121619;
    text-align: left;
    padding-left: 20px;
}

.sieu-re-text {
    flex-grow: 1;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;
    color: #121619;
    text-align: left;
    padding-left: 20px;
} */

.diem {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */

    text-align: right;

    /* Gray/90 */

    color: #121619;
}

</style>
