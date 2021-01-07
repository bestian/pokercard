<template>
  <div class="hello">
    <div class="noPrint"> 
      <div v-for = "suitC in root.suits" class="noPrint" :class="suitC" :key="suitC">
          <p class = "noPrint" v-show = "suitC == 'Spade'">&spades;</p>
          <p class = "noPrint" v-show = "suitC == 'Heart'">&hearts;</p>
          <p class = "noPrint" v-show = "suitC == 'Dimond'">&diams;</p>
          <p class = "noPrint" v-show = "suitC == 'Club'">&clubs;</p>

          <div>
            <p v-for = "index in keys" class="noPrint" :key="index">
              {{ root.cards[index].n }}
              <input v-model = "root.cards[index][suitC].t" @input="updateCards()">
              <input v-model = "root.cards[index][suitC].u" @input="updateCards()">
            </p>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    makeCss (str) {
      var ans = "spot "+str.substr(0,1)+" r"+str.substr(1,2);
    //  console.log(ans);
      return ans
    },
    makeQR (str) {
      return str.replace('https://','').replace('http://','');
    },
    updateCards () {
      this.$localStorage.set('cards', JSON.stringify(this.root.cards))
      // console.log(JSON.parse(this.$localStorage.get('cards')))
      this.$emit('updateCards')
    }
  },
  data () {
    return {
      keys: [],
      magic: 1.022,
      root: {
        myName: '為您的套牌命名',
        size: 44,
  //    $scope.root.alpha = 100;
        font: '?font=wt021',
        public: 2,  /// TOOL ///
        suits: ['Club','Dimond','Spade','Heart'],
        cards: {
          ace: {n: 'A', css: ['E3'], top:0, left:0,
            Spade: {t: "g0v零時政府", u: "g0v.tw"},
            Heart: {t: "自主學習促進會", u: "www.alearn.org.tw"},
            Dimond: {t: "主婦聯盟環保基金會", u: "www.huf.org.tw/"},
            Club: {t:"一小時學會寫程式", u:"code.org"}
          },

          two: {n: '2', css:['A1','C5'], top:0, left:1,
                Spade: {t: "中央政府總預算", u: "budget.g0v.tw/"},
                Heart: {t: "自學2.0", u: "we.alearn.org.tw"},
                Dimond: {t: "上下游新聞市集", u: "www.newsmarket.com.tw/"},
                Club: {t:"Scratch", u:"scratch.mit.edu/"}
          },
              
          three: {n: '3', css:['A1','B3','C5'], top:0, left:2,
                Spade: {t: "萌典", u: "www.moedict.tw/"},
                Heart: {t: "保障教育選擇權聯盟", u: "www.homeschool.tw/"},
                Dimond: {t: "厚生市集", u: "www.farm-direct.com.tw/"},
                Club: {t:"d3資訊繪圖", u:"d3js.org"},     
          },
          four: {n: '4', css:['A1','A5','C1','C5'], top:0, left:3,
                Spade: {t: "立院影城", u: "ivod.ly.g0v.tw/onair"},
                Heart: {t: "自學地圖", u: "map.alearn.org.tw"},
                Dimond: {t: "直接跟農夫買", u: "www.buydirectlyfromfarmers.tw/"},
                Club: {t:"Geogebra數理動畫", u:"www.geogebra.org"},    

          },
          five: {n: '5', css:['A1','A5','B3','C1','C5'], top:1, left:0,
                Spade: {t: "民代地圖", u: "g0v.github.io/mapView/ly.html"},
                Heart: {t: "台灣自學法律網", u: "law.chen-wernik.net/"},
                Dimond: {t: "主婦聯盟合作社", u: "www.hucc-coop.tw"},
                Club: {t:"網路開發者技能樹", u:"www.dungeonsanddevelopers.com/"},   
          },
          six: {n: '6', css:['A1','A3','A5','C1','C3','C5'], top:1, left:1,
                Spade: {t: "新聞小幫手", u: "newshelper.g0v.tw"},
                Heart: {t: "學習風格自我測試", u: "map.alearn.org.tw/#/style"},
                Dimond: {t: "林口台地農夫市集", u: "market.glife.org.tw/"},
                Club: {t:"Codecademy", u:"www.codecademy.com/"}, 
          },

          seven: {n: '7', css:['A1','A3','A5','B2','C1','C3','C5'], top:1, left:2,
                Spade: {t: "求職小幫手", u: "jobhelper.g0v.ronny.tw"},
                Heart: {t: "自學計畫諮詢", u: "sites.google.com/site/alearn13994229/a-03"},
                Dimond: {t: "台中合樸農學市集", u: "www.hopemarket.net"},
                Club: {t:"W3schools", u:"www.w3schools.com"},
          },

          eight: {n: '8', css:['A1','A3','A5','B2','B4','C1','C3','C5'], top:1, left:3,
                Spade: {t: "g0v新手村小遊戲", u: "8bit.g0v.tw"},
                Heart: {t: "自由數學", u: "math.alearn.org.tw"},
                Dimond: {t: "248農學市集", u: "www.248.com.tw/"},
                Club: {t:"Jsbin協作練習區", u:"jsbin.com"},
          },

          nine: {n: '9', css:['A1','A2','A4','A5','B3','C1','C2','C4','C5'], top:2, left:0, 
                Spade: {t: "福利請聽", u: "listening.g0v.tw/"},
                Heart: {t: "1know翻轉學習", u: "1know.net/"},
                Dimond: {t: "好食機", u: "www.howsfood.com"},
                Club: {t:"Github協力開發社群", u:"github.com"},  
          },
          ten: {n: '10', css:['A1','A2','A4','A5','B2','B4','C1','C2','C4','C5'], top:2, left:1,
                Spade: {t: "懸浮微粒", u: "g0v.github.io/twgeojson/air"},
                Heart: {t: "Khan可汗學院", u: "http://www.khanacademy.org"},
                Dimond: {t: "彎腰農夫市集", u: "bowtoland.blogspot.tw"},
                Club: {t:"Firebase", u:"www.firebase.com"},  
          },

          jack: {n: 'J', css:['E3'], top:2, left:2,
                Spade: {t: "如何使用IRC", u: "github.com/g0v/dev/wiki/如何使用-IRC"},
                Heart: {t: "如何成為自由人才", u: "www.youtube.com/watch?v=ZPzqw3x05-g"},
                Dimond: {t: "台灣農夫市集地圖", u: "http://farmersmarket.ushahidi.tw/"},
                Club: {t:"jQuery函式庫", u:"jquery.com"},        
          },
          queen: {n: 'Q', css:['E3'], top:2, left:3, 
                Spade: {t: "動民主", u: "g0v.github.io/don-republic/"},
                Heart: {t: "如何訂學習計畫", u: "www.youtube.com/watch?v=SUoT5P8_UOI"},
                Dimond: {t: "台東羅傑農場", u: "www.339.com.tw/rogerfarm.html"},
                Club: {t:"StackOverflow", u:"stackoverflow.com"}, 
          },

          king: {n: 'K', css:['E3'], top:3, left:0, 
                  Spade: {t: "政誌", u: "fact.g0v.tw"},
                  Heart: {t: "全球化與自主學習", u: "www.youtube.com/watch?v=Mi7qkTyqimE"},
                  Dimond: {t: "綠農的家", u: "www.greenff.com.tw"},
                  Club: {t:"AngularJs",u:"www.angularjs.org"}, 
            
          },

          Ad1: {n: '天', css:['E3'], top:3, left:1, 
                  Spade: {t: "開源之道", u: "www.slideshare.net/autang/open-source-enlightenment"},
                  Heart: {t: "維基百科", u: "zh.wikipedia.org/"},
                  Dimond: {t: "友善大地", u: "shui-ling.organic.org.tw/supergood/front/bin/ptlist.phtml?Category=106460"},
                  Club: {t:"何謂開放源碼",u:"www.youtube.com/watch?v=a8fHgx9mE5U"}, 
            
          },

          Ad2: {n: '水', css:['E3'], top:3, left:2, 
                  Spade: {t: "樸克牌", u: "http://bestian.github.io/pokercard/index.html"},
                  Heart: {t: "不該給學生打分數", u: "www.slideshare.net/Bestian_Tang/ss-16354270"},
                  Dimond: {t: "農民學院", u: "academy.coa.gov.tw"},
                  Club: {t:"小巴作品",u:"github.com/bestian"}, 
            
          }
        }
      }
    }
  },
  mounted () {
    if (navigator.userAgent.indexOf('Firefox') > -1) {
        this.magic = 1.2;
    }

    if (navigator.userAgent.indexOf('Chrome') > -1) {
        this.magic = 1.067;      
    }
    this.keys = Object.keys(this.root.cards)
    if (this.$localStorage.get('cards')) {
      this.root.cards = JSON.parse(this.$localStorage.get('cards'))
    }
  },
  watch: {
    root (newRoot) {
      this.$localStorage.set('cards', newRoot.cards)
      this.$emit('updateCards')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

input {
  font-size: 26px;
  width: 40vw;

}
</style>
