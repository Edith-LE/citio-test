<template>
  <div class="color-card">
    <div 
      :style="{'background-color': data.color}"
      class="color-card__bg"
    >
      <div class="color-card__text">
        {{ data.text }}
      </div>
    </div>

  </div>
</template>
<script>
export default{
  name: "ColorCard",
  props: {
    data:{
      type: Object,
      default: () => {}
    }
  },
  data(){
    return{

    }
  }
}
</script>
<style lang="scss">
.color-card{
  width: 100%;
  display: flex;
  justify-content: center;
  @media screen and (max-width: 768px){
    padding: 16px;
  }
  &__bg{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 300px;
    height: 300px;
    border-radius: 8px;
    @media screen and (max-width: 768px){
    margin-bottom: 20px;
  }

  }
  &__text{
    font-size: 24px;
    line-height: 32px;
    color: black;
    font-weight: bold;
  }
  
}
</style>