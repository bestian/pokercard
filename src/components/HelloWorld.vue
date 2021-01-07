<template>
  <div class="hello">
    <a id = "doPrint" class="noPrint" onclick="window.print()">列印樸克牌。&spades;&hearts;&diams;&clubs;
    </a>
    <div class ="suit" v-for = "suitID in [0,1,2,3]" :key="suitID">
      <div v-for = "card in root.cards" class="card" :class="root.suits[suitID]" :style="{left:card.left * 64 - 2 +'mm', top:(card.top * 83 + suitID*79.5*4*magic) + 'mm'}" :key="card.n">
          <div class="front" :class="root.suits[suitID] + card.n">
            <div class="index" v-show = "['J','Q','K','天','水'].indexOf(card.n) == -1 ">{{card.n}}<br /> 
                <span v-show = "root.suits[suitID] == 'Spade'">&spades;</span>
                <span v-show = "root.suits[suitID] == 'Heart'">&hearts;</span>
                <span v-show = "root.suits[suitID] == 'Dimond'">&diams;</span>
                <span v-show = "root.suits[suitID] == 'Club'">&clubs;</span>
            </div>
            <div class="title">
              <span class="black">{{card[root.suits[suitID]].t}}</span>
            </div>

            <div v-for = "tail in card.css"    
            :class="makeCss(tail)" :key="tail">
              <a :href = "makeQR(('https://'+card[root.suits[suitID]].u) || 'https://poker.bestian.tw')" target="_blank">

              <img class = "icon" :src="'https://chart.apis.google.com/chart?chs=200x200&amp;cht=qr&amp;chld=|1&amp;chl=http%3A%2F%2F' + (card[root.suits[suitID]].u || 'pokercard.bestian.tw')" :alt="card[root.suits[suitID]].t" >

              </a>
            </div>

            <div class="flipTitle" 
            :style = "{top: 75 + 'mm' }">
               <span class="black">{{card[root.suits[suitID]].t || '資訊待補充'}}</span>
            </div> 
            <div class="flipIndex" v-show = "['J','Q','K','天','水'].indexOf(card.n) == -1">{{card.n}}<br />

                <span v-show = "root.suits[suitID] == 'Spade'">&spades;</span>
                <span v-show = "root.suits[suitID] == 'Heart'">&hearts;</span>
                <span v-show = "root.suits[suitID] == 'Dimond'">&diams;</span>
                <span v-show = "root.suits[suitID] == 'Club'">&clubs;</span>
            </div>
          </div>    
          <div class="print" :class="root.suits[suitID]+card.n">
          </div>
      </div>
      <div class="page-break"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    root: Object,
    keys: Array
  },
  methods: {
    makeCss (str) {
      var ans = "spot "+str.substr(0,1)+" r"+str.substr(1,2);
    //  console.log(ans);
      return ans
    },
    makeQR (str) {
      return str.replace('https://','').replace('http://','');
    }
  },
  data () {
    return {
      magic: 1.022
    }
  },
  mounted () {
    if (navigator.userAgent.indexOf('Firefox') > -1) {
        this.magic = 1.2;
    }

    if (navigator.userAgent.indexOf('Chrome') > -1) {
        this.magic = 1.067;      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

/******************************************************************************
* Styles for playing cards.                                                   *
******************************************************************************/

.suit {
  position: relative;
  margin: 0;
  padding: 0;
}

#frm {
  z-index: 999;
  top: 0;
  right: 0;
  background: rgba(200, 200, 200, 0.98);
  border-radius: 5px;
  padding: 5px 15px;
  position: absolute;
}

#whiteback {
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  width: 260mm;
  height: 1450mm;
  background-color: #ffffff;
  z-index: -1;
}

.card {
  border: #000 3px solid;
  font-size: 25pt;
  position: absolute;
  height: 82mm;
  width: 63mm;
  border-radius: 15px;
  page-break-inside: avoid;
}

.front {
  display: block;
  border-radius: 10px;
  background-color: #ffffff;
  color: #000000;
  position: absolute;
  height: 100%;
  width: 100%;
  background-size: contain;
/*  background-size: cover; */

}

.print {
  display: block;
  border-radius: 10px;
  position: absolute;
  height: 100%;
  width: 100%;  
}


/* .print.SpadeK {   content: url("/img/cards/Spade_king.png"); } */


.print.SpadeK {   content: url("/img/cards/Spade_king.png"); }
.print.SpadeK:before  {   content: url("/img/cards/Spade_king.png"); }

.print.SpadeQ {   content: url("/img/cards/Spade_Queen.png"); }
.print.SpadeJ {   content: url("/img/cards/Spade_Jack.jpg"); }
.print.Spade天 {   content: url("/img/cards/Jocker1.jpg"); }
.print.Spade水 {   content: url("/img/cards/Jocker2.jpg"); }


.print.HeartK {  content: url("/img/cards/Heart_king.jpeg"); }
.print.HeartQ {  content: url("/img/cards/Heart_Queen.png"); }
.print.HeartJ {  content: url("/img/cards/Heart_Jack.png"); }
.print.Heart天 {   content: url("/img/cards/Jocker1.jpg"); }
.print.Heart水 {   content: url("/img/cards/Jocker2.jpg"); }

.print.DimondK {  content: url("/img/cards/Dimond_King.png"); }
.print.DimondQ {  content: url("/img/cards/Dimond_Queen.png"); }
.print.DimondJ {  content: url("/img/cards/Dimond_Jack.png"); }
.print.Dimond天 {   content: url("/img/cards/Jocker1.jpg"); }
.print.Dimond水 {   content: url("/img/cards/Jocker2.jpg"); }

.print.ClubK {  content: url("/img/cards/Club_king.png"); }
.print.ClubQ {  content: url("/img/cards/Club_Queen.png"); }
.print.ClubJ {  content: url("/img/cards/Club_Jack.jpg"); }
.print.Club天 {   content: url("/img/cards/Jocker1.jpg"); }
.print.Club水 {   content: url("/img/cards/Jocker2.jpg"); }

.index, .flipIndex, .title, .flipTitle {
  font-size: 60%;
  font-weight: bold;
  text-align: center;
  position: absolute;
  z-index: 2;
}

.index, .flipIndex {
  font-size: 100%;
  line-height: 90%;
}

.index {
  left: 2mm;
  top:  2mm;
}
.flipIndex {
  left: 54mm;
  top:  64mm;
    -moz-transform: rotate(180deg); 
    -webkit-transform: rotate(180deg);
    filter: progid:DXImageTransform.Microsoft.Matrix(sizingMethod='auto expand', 
    M11=-1, M12=0, 
    M21=0, M22=-1);
}

.face {
  border: 1px solid #000000;
  border-radius: 15px;
  position: absolute;
  left: 0.50em;
  top:  0.45em;
  width:  2.6em;
  height: 4.0em;
}

.spot { position: absolute }

.A { left: 8mm }
.B { left: 27mm }
.C { left: 45mm }

.r1 { top: 17mm }   /* 10,5,5,10 */
.r2 { top: 33mm }   /* 12,6,6,12 */
.r3 { top: 41mm }   /* 16,8,8,16 */
.r4 { top: 49mm }
.r5 { top: 65mm }

.E.r3 { left: 21mm; top: 33mm }

.A.r1 { left: 4mm ; top: 17mm;}
.A.r2 { top: 35mm;}
.A.r3 { top: 43mm;}
.A.r4 { top: 51mm;}
.A.r5 { top: 67mm;}
.A.r1 .icon, .E.r3 .icon  {  width: 20mm; z-index: 5;}
.Heart .A.r1 .icon, .Heart .E.r3 .icon  {
    padding: 7px; 
    border: red 5px solid;}
.Heart .A.r1 {top: 15mm;}

.Dimond .A.r1 .icon, .Dimond .E.r3 .icon, .Club .A.r1 .icon, .Club .E.r3 .icon  {  
  padding: 0px;
}

.Club .A.r1 .icon, .Club .E.r3 .icon  {  
  border: #999 3px solid;
}

.Dimond .A.r1, .Club .A.r1 { left: 7mm; }

.B .icon {  z-index: 4; }

.icon {
  position: relative;
  width: 6mm;
  z-index: 3;
}


.Heart *, .Dimond *{
  color:red;
}

.Spade .icon {
  display: block;
  border: 2px black solid;
  border-radius: 10px;
}
.Heart .icon {
    display: block; 
    border-radius: 30px;
  /*  background-color: red; */
    border: red 2px solid;
    padding: 5px; 
}

.Dimond .icon {
    display: block;
  /*  background-color: red; */
    border: red 2px solid;
    -moz-transform: rotate(45deg); 
    -webkit-transform: rotate(45deg);
    filter: progid:DXImageTransform.Microsoft.Matrix(sizingMethod='auto expand', 
    M11=0.7071067811, M12=-0.7071067811, 
    M21=0.7071067811, M22=0.7071067811);
}

.Club .icon {
    display: block;
  /*  background-color: grey; */
    border: grey 5px solid;
    border-radius: 15px;

    -moz-transform: rotate(45deg); 
    -webkit-transform: rotate(45deg);
    filter: progid:DXImageTransform.Microsoft.Matrix(sizingMethod='auto expand', 
    M11=0.7071067811, M12=-0.7071067811, 
    M21=0.7071067811, M22=0.7071067811);}


.title, .flipTitle {  color: #ccc;  width: 50mm;}

.title {
  left: 7mm;
  top:  2mm;
  height: 50mm;
}

.flipTitle {
  left: 3mm;
  transform: rotate(180deg); 
  -moz-transform: rotate(180deg); 
  -webkit-transform: rotate(180deg);
  filter: progid:DXImageTransform.Microsoft.Matrix(sizingMethod='auto expand', 
  M11=-1, M12=0, 
  M21=0, M22=-1);
}


#custom {
  display: block;
  float: right;
  cursor: help;
  position: fixed;
  top: 40px;
  right: 3%;
  z-index: 11;
}
#custom:hover {
  z-index: 101;
}

.tool {
  display: block;
  position: relative;
  overflow-y: scroll;
  padding-left: 3px;
  height: 12ex; 
  -webkit-transition: all 1s ease;
  -moz-transition: all 1s ease;
  -ms-transition: all 1s ease;
  -o-transition: all 1s ease;
  transition: all 1s ease;

}
.tool:hover {
  height: 60vh;
  top: 0;
  right: 0;
  background-color: #fff;
  z-index: 12;
}


.tool.Club:hover{
  margin-top: -1ex;
}
.tool.Dimond:hover{
  margin-top: -5ex;
}
.tool.Spade:hover{
  margin-top: -15ex;
}
.tool.Heart:hover{
  margin-top: -25ex;
}

#bull {
  display: block;
  overflow: auto; 
  height: 60ex; 
}

#bull p {
  overflow-y: scroll;
}

.right {
  text-align: right;
  margin-right: 50px;
}

.right:hover {
  font-size: 200%;
}


a#doPrint {
    position: fixed;
    top: 30px;
    left: 40%;
    z-index: 31;
    top: 50%;
    left: 25%;
    margin-top: -15%;
    margin-left: -5%;
    width: 50%;
    height: 10%;
    text-decoration: none;
    color: rgba(255,255,255,0.5);
    background-color: rgba(219,87,5,0.5);
    font-family: 'Yanone Kaffeesatz';
    font-weight: 700;
    font-size: 200%;
    line-height: 200%;
    cursor: pointer;
    display: block; 
    padding: 5px;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    border-radius: 8px;
    -webkit-box-shadow: 0px 9px 0px rgba(219,31,5,.5), 0px 9px 25px rgba(0,0,0,.4);
    -moz-box-shadow: 0px 9px 0px rgba(219,31,5,.5), 0px 9px 25px rgba(0,0,0,.4);
    box-shadow: 0px 9px 0px rgba(219,31,5,.5), 0px 9px 25px rgba(0,0,0,.4);

    text-align: center;
  
  -webkit-transition: all 1s ease;
  -moz-transition: all 1s ease;
  -ms-transition: all 1s ease;
  -o-transition: all 1s ease;
  transition: all 1s ease;
}

a#doPrint:hover {
    color: rgba(255,255,255,1);
    background-color: rgba(219,87,5,1);
    -webkit-box-shadow: 0px 9px 0px rgba(219,31,5,1), 0px 9px 25px rgba(0,0,0,.7);
    -moz-box-shadow: 0px 9px 0px rgba(219,31,5,1), 0px 9px 25px rgba(0,0,0,.7);
    box-shadow: 0px 9px 0px rgba(219,31,5,1), 0px 9px 25px rgba(0,0,0,.7);

}

a#doPrint:active {
    -webkit-box-shadow: 0px 3px 0px rgba(219,31,5,1), 0px 3px 6px rgba(0,0,0,.9);
    -moz-box-shadow: 0px 3px 0px rgba(219,31,5,1), 0px 3px 6px rgba(0,0,0,.9);
    box-shadow: 0px 3px 0px rgba(219,31,5,1), 0px 3px 6px rgba(0,0,0,.9);
}


@media print {
  .page-break { 
    page-break-inside: always;
  }

  body {
    background-color: #ffffff;
  }

  .noPrint, .noPrint *{
    display: none;
    visibility: hidden;
  }

  a#doPrint {
    color: rgba(255,255,255,0);
    background-color: rgba(219,87,5,0);
    -webkit-box-shadow: 0px 9px 0px rgba(219,31,5,0), 0px 9px 25px rgba(0,0,0,0);
    -moz-box-shadow: 0px 9px 0px rgba(219,31,5,0), 0px 9px 25px rgba(0,0,0,0);
    box-shadow: 0px 9px 0px rgba(219,31,5,0), 0px 9px 25px rgba(0,0,0,0);
  }
}

.moe {
  position: relative;
  display: inline-block;
  float: none;
  z-index: 501;
}

.black {
  color: black;
}
</style>
