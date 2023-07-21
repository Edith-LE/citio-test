<script >
  // import CardItem from "../components/CardItem.vue"
  import ColorCard from "../components/ColorCard.vue"
  export default{
    components:{
      // CardItem,
      ColorCard
    },
    data(){
      return{
        dataInfo: null,
        cardsData:[
          {
            color:"#6EEC2B",
            text: "Div 1"
          },
          {
            color: "#3B84D7",
            text: "Div 2"
          }
        ]
      }
    },
    mounted(){
      this.getCallInfo()
    },
    methods:{
      getCallInfo(){
        return fetch("/helpers/callHistory.json")
        .then(res => res.json())
        .then(data => {
          const reduced = data.reduce((acc, cur) => {
            const existing = acc.find((el) => el.firstName == cur.firstName)
            if(existing){
              existing.qty ++
            }else{
              acc.push({
                ...cur,
                qty: 1 
              })
              
            }
            return acc
          }, [])
          const sorted = reduced.sort((a,b) => {
            return b.qty - a.qty
          })
          
          const maped = sorted.map((item) => (
            {
              name: item.firstName, 
              lastname: item.lastName,
              qty: item.qty,
              date: this.getRelativeDate(item.called * 1000)
            }
          ))
          this.dataInfo = maped
          return this.dataInfo
        })
      },
      getRelativeDate(date) {
        const now = new Date();
        const diffInMilliseconds = date - now;

        const seconds = Math.floor(diffInMilliseconds / 1000);
        const minutes = Math.floor(seconds / 60);
        const hours = Math.floor(minutes / 60);
        const days = Math.floor(hours / 24);
        const months = Math.floor(days / 30);
        const years = Math.floor(months / 12);

        const rtf = new Intl.RelativeTimeFormat('en', { numeric: 'auto' });
        console.log(rtf.format(years, 'year'));
        if (years !== 0) {
          return rtf.format(years, 'year');
        } else if (months !== 0) {
          return rtf.format(months, 'month');
        } else if (days !== 0) {
          return rtf.format(days, 'day');
        } else if (hours !== 0) {
          return rtf.format(hours, 'hour');
        } else if (minutes !== 0) {
          return rtf.format(minutes, 'minute');
        } else {
          return 'just now';
        }
        
      }
    }  
  }
</script>

<template>
  <div 
    class="container-card"
  >
    <color-card
      v-for="(i, idx) in cardsData"
      :key="idx" 
      :data="i"
    />
  </div>
  <!-- <main class="contacts">
    <div class="contacts__header">
      <p>
        My favorite contacts
      </p>

    </div>
    <div
    class="contacts__card-list" 
    v-for="(item, idx) in dataInfo">
    
    <card-item 
        :data="item"
      />

    </div>
  </main> -->
</template>

<style lang="scss">
.container-card{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 500px;
  border: 1px solid red;
  @media screen and (max-width: 768px){
    flex-wrap: wrap;
    height: auto;
    
    
  }
}
// .contacts{
//   width: 500px;
//   &__header{
//     background-color: violet;
//     color: white;
//     font-size: 18px;
//     font-weight: bold;
//     text-align: center;
//   }
// }

</style>
