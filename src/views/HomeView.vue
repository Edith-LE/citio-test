<script >
  import ColorCard from "../components/ColorCard.vue"
  export default{
    components:{
      ColorCard
    },
    data(){
      return{
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
</style>
