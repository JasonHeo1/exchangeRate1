<template>
  <v-app>
  <v-card class="vCard" height="80px">
    <v-img
      :src="require('@/assets/img/yyIcon.jpg')"
      height="80px" width="200px"
    ></v-img>
  </v-card>
    <v-card class="vCardTwo" height="40px" style="background-color: rgb(49, 86, 233)">
      <span class="titleText" style="color:white">송금계의 트리바고, 호텔컴바인</span>
      <!-- <v-card-title class="vCard">{{time}}</v-card-title> -->
    <!-- <AdsenseVue v-bind:slot="7644074545"></AdsenseVue> -->
    </v-card>
    <!-- <v-tabs v-model="activeTab" @change="switchTab"> -->
    <v-tabs v-model="activeTab">
      <v-tab key="tab-a">KRW->CNY</v-tab>
      <!-- <v-tab key="tab-b">人民币->韩币</v-tab> -->

    <v-tab-item key="tab-a">
      <v-data-table
        :headers="headersTabOne"
        :items="remittanceListTabA"
        :mobile-breakpoint="0"
        :disable-items-per-page="true"
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <tr style="height: 50px;">
          <td class="text-xs-left">
            <v-avatar size="50">
              <img :src="props.item.icon" alt="avatar" />
            </v-avatar>
          </td>
          <td class="text-sm-left">{{ props.item.companyNmEng }}</td>
          <td class="text-xs-left">10,000</td>
          <td class="text-xs-left">
            <v-avatar size="20">
              <img :src="require('@/assets/img/arrowRight.png')" alt="avatar" />
            </v-avatar>
          </td>
          <td class="text-xs-left">
            {{ (props.item.exchangeRate * 10000) | toFixed(2) }}
          </td>
          <!-- <td class="text-xs-left">{{ props.item.exchangeRate | toFixed(4) }}</td> -->
          <!-- <td class="text-xs-left">{{ props.item.company.name }}</td> -->
          <!-- <td class="text-xs-left">{{ props.item.website }}</td> -->
          <!-- <td class="text-xs-left">{{ props.item.address.city }}</td> -->
          </tr>
        </template>
      </v-data-table>
    </v-tab-item>

    <v-tab-item key="tab-b">
      <v-data-table
        :headers="headersTabTwo"
        :items="remittanceListTabB"
        :mobile-breakpoint="0"
        disable-pagination
        hide-default-footer
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td class="text-xs-left">
            <v-avatar size="50">
              <img :src="props.item.icon" alt="avatar" />
            </v-avatar>
          </td>
          <td class="text-sm-left">{{ props.item.companyNmEng }}</td>
          <td class="text-xs-left">1</td>
          <td class="text-xs-left">
            <v-avatar size="20">
              <img :src="require('@/assets/img/arrowRight.png')"  alt="avatar" />
            </v-avatar>
          </td>
          <td class="text-xs-left">
            {{ (props.item.exchangeRate) | toFixed(2) }}
          </td>
          <!-- <td class="text-xs-left">{{ props.item.exchangeRate | toFixed(4) }}</td> -->
          <!-- <td class="text-xs-left">{{ props.item.company.name }}</td> -->
          <!-- <td class="text-xs-left">{{ props.item.website }}</td> -->
          <!-- <td class="text-xs-left">{{ props.item.address.city }}</td> -->
        </template>
      </v-data-table>
    </v-tab-item>
    </v-tabs>
    <span></span>
    <v-card class="vCard" height="55px">
      <span class="spanText">
      **환율 app 정보 확장 중. 
      환율은 실시간 환율과 다소 차이가 있을 수 있습니다.
      <br>上述汇率与实时汇率间可能存在误差。</span>
    </v-card>
  </v-app>

</template>

<script>
import AdsenseVue from './Adsense.vue';

export default {
  components:{
      AdsenseVue,
    },
  filters: {
    dateFormat: function(val, format) {
      return moment(val).format(format);
    },
    toFixed: function(val, num) {
      return parseFloat(val).toFixed(num);
    },
    comma: function(val) {
      return String(Math.round(val)).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  },
  data() {
    return {
      activeTab: 'tab-a', // 초기 선택 탭
      time:'',
      currencyCodeFromValue:'KRW',
      currencyCodeToValue:'CNY',

      // users: [],

      remittanceListTabA:[],
      remittanceListTabB:[],
      arrowRightPath:"/static/img/arrowRight.png",
      yyIconPath:"/static/img/yyIcon.jpg",
      headersTabOne: [
        {
          value: "icon",
          align: "left",
          sortable: false
        },
        {
          text: "App",
          value: "companyNmEng",
          align: "left",
          sortable: false,
          align: "left"
        },
        {
          text: "KRW",
          value: "10,000",
          align: "left",
          sortable: false,
          align: "left"
        },
        {
          text: "",
          value: "10,000",
          align: "left",
          sortable: false,
          align: "left"
        },
        {
          text: "CNY",
          value: "currencyCodeTo",
          align: "left",
          sortable: false,
          align: "left"
        },
        // {
        //   text: "Rate",
        //   value: "exchangeRate",
        //   align: "left",
        //   sortable: false,
        //   align: "left"
        // }
      ],
      headersTabTwo: [
        {
          value: "icon",
          align: "left",
          sortable: false
        },
        {
          text: "App Name",
          value: "companyNmEng",
          align: "left",
          sortable: false,
          align: "left"
        },
        {
          text: "CNY",
          value: "100",
          align: "left",
          sortable: false,
          align: "left"
        },
        {
          text: "",
          value: "10,000",
          align: "left",
          sortable: false,
          align: "left"
        },
        {
          text: "KRW",
          value: "currencyCodeTo",
          align: "left",
          sortable: false,
          align: "left"
        },
        // {
        //   text: "Rate",
        //   value: "exchangeRate",
        //   align: "left",
        //   sortable: false,
        //   align: "left"
        // }
      ]
    };
  },

  methods: {
    // randomAvatar() {
    //   return avatars[Math.floor(Math.random() * avatars.length)];
    // },

    getRemittanceList: function() {
      this.axios.post('http://admin.yyhq.kr:8888/rate/exchangeRateInfo/latestExchangeRateInfoRequest',{
      // this.axios.post('http://babohama.synology.me:8888/rate/exchangeRateInfo/latestExchangeRateInfoRequest',{
      // "currencyCodeFrom": this.currencyCodeFromValue,
      // "currencyCodeTo": this.currencyCodeToValue
      "currencyCodeFrom": 'KRW',
      "currencyCodeTo": 'CNY'
    }).then(response => {
      var result = response && response.data;
      console.log(JSON.stringify(result.data));

      this.remittanceListTabA = result.data;
    });
    },

    getRemittanceListSecond: function() {
      this.axios.post('http://admin.yyhq.kr:8888/rate/exchangeRateInfo/latestExchangeRateInfoRequest',{
      // this.axios.post('http://babohama.synology.me:8888/rate/exchangeRateInfo/latestExchangeRateInfoRequest',{
      // "currencyCodeFrom": this.currencyCodeFromValue,
      // "currencyCodeTo": this.currencyCodeToValue
      "currencyCodeFrom": 'CNY',
      "currencyCodeTo": 'KRW'
    }).then(response => {
      var result = response && response.data;
      console.log(JSON.stringify(result.data));

      this.remittanceListTabB = result.data;
    });
    },
    getCurrentTime: function(){
        const now = new Date();
        const year = now.getFullYear();
        const month = String(now.getMonth() + 1).padStart(2, '0');
        const day = String(now.getDate()).padStart(2, '0');
        const hours = String(now.getHours()).padStart(2, '0');
        const minutes = String(now.getMinutes()).padStart(2, '0');
        const seconds = String(now.getSeconds()).padStart(2, '0');

        this.time = `${year}-${month}-${day} ${hours}:${minutes}:${seconds}`;
    },

    // switchTab(tab){
    //   if(tab === 0){
    //     this.currencyCodeFromValue = 'KRW',
    //     this.currencyCodeToValue = 'CNY'
    //   }else{
    //     this.currencyCodeFromValue = 'CNY',
    //     this.currencyCodeToValue = 'KRW'
    //   }
    //   console.log('currencyCodeFromValue: '+this.currencyCodeFromValue);
    //   console.log('currencyCodeToValue: '+this.currencyCodeToValue);

    //   this.getRemittanceList();
    //   console.log(JSON.stringify(this.remittanceList));
    // }
  },

  created() {
    const vm = this;
    vm.getCurrentTime();
    vm.getRemittanceList();
    // vm.getRemittanceListSecond();
  }
};
</script>

<style>
.table {
  border-radius: 1px;
  background-clip: content-box;
  border: 1px solid rgba(0, 0, 0, 0.125);
  box-shadow: 1px 1px 1px 1px rgba(0, 0, 0, 0.21);
  background-color: cadetblue;
  /* width: 390px; */


/* 아이패드 에어 (가로 모드) */
@media (min-width: 768px) and (max-width: 1023px) {

    width: 768px; /* 화면 너비가 768px에서 1023px 사이일 때의 높이 설정 */
}
}
.vCard {
  border-radius: 10px;
  background-color: aliceblue;
  font-weight: bold;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 18px;
  margin-top: 5px;
}
.vCardTwo {
  border-radius: 10px;
  background-color: rgb(49, 86, 233);
  font-weight: 900;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  margin-top: 5px;
  margin-bottom: 1px;
  padding-left: 60px;
  padding-top: 10px;
}
.spanText {
  margin-block: inherit;
  font-size: 5px;
  font-style: italic;
  color: coral;
}
.titleText {
  font-size: 15px;
  font-style: italic;
  color: blue;
  position: center;
}
</style>
