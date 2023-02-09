<template>
    <div class="header">Thông tin trả thưởng</div>
    <div class="amount_box" id="cnt">
        <div class="amount-text">Số tiền được nhận</div>
        <div class="amount">+{{reward_detail.reward}}VND</div>
    </div>
    <!-- </div> -->
    <div class="achievement-box" id="cnt">
        <div class="acht_text">Thành tích</div>
        <div class="points_box">
            <div class="point_reward">90 điểm</div>
            <div class="pnt_txt">Mục tiêu 30 điểm</div>
        </div>
    </div>
    <div class="content_contain">
    <div class="order_accept">
        <div class="ctn">
            <div class="accepted">
                <div class="txt">Tỷ lệ chấp nhận đơn hàng</div>
                <v-btn class="more_info"><img src="../condition/info.svg"/></v-btn>
            </div>
            <div class="load_bar">
                <img src="../condition/load_bar.svg"/>
                <!-- <img class="load_bar_sp" src="../condition/red_load.svg"/> -->
                </div>
        </div>
        <div class="rate_percentage">
            <div class="odds">100%</div>
            <div class="check"><img src="../condition/checked.svg"/></div>
        </div>
    </div>
    </div>
</template>

<script>
// import { Data } from '../data/data.js'
// import { clicked } from '@/views/RewardFund.vue'
// import axios from 'axios'
// const API = 'https://apistg.ahamove.com/opstech/loyalty/supplier/pt/api/v1/supplier/reward?from=1660875937&to=1661394337&offset=0&limit=10'
// const token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhaGEiLCJ0eXAiOiJzdXBwbGllciIsImNpZCI6Ijg0Mzg3OTkwMDU1Iiwic3RhdHVzIjoiT0ZGTElORSIsImVvYyI6InZ1bGFAYWhhbW92ZS5jb20iLCJub2MiOiJMZSBBbmggVnUiLCJjdHkiOiJXQSIsImFjY291bnRfc3RhdHVzIjoiQUNUSVZBVEVEIiwicm9sZSI6ImFkbWluIiwicm9sZV9pZHMiOltdLCJleHAiOjE2MzQxMTYyMjQsInR5cGUiOiJ3ZWIiLCJpbWVpIjoid2ViIn0.CP7Bwq4f7CCTLLBvz0qnDPAG08jujq9PIoc5SLG_b_0'
export default {
  name: 'RewardInfo',
  data () {
    return {
      // item: clicked
    }
  },
  props: ['reward_detail']
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

.amount-box {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background: #FFFFFF;
    border: 0.2px solid #dbe4f0;
}

#cnt {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    background: #FFFFFF;
    border: 0.2px solid #e4e9f072;
}

.amount-text {
    flex-grow: 1;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;
    color: #121619;
    text-align: left;

}
.amount {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 24px;
    color: #38A169;
}

.achievement_box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: #FFFFFF;
}

.acht_text {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 20px;
    color: #121619;
    padding-bottom: 15px;
}

.point_box {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end;
}

.point_reward {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 14px;
    line-height: 20px;
    text-align: right;
    color: #121619;
}

.pnt_txt {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 16px;
    color: #697077;
}
.content_contain {
    background: #FFFFFF;
    width: 100%;
    padding-top: 2px;
    padding-bottom: 2px;
    padding-right: 5px;
    padding-left: 12px;
}
.order_accept {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 0.2px solid #bec6d141;
    background: #F7F9FC;
}

.accepted {
    display: flex;
    align-items: center;
}

.rate_percentage {
    width: 55px;
    height: 56px;
    background: #EEF0F3;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
</style>
