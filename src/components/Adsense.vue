<template>
  <div>
    <ins class="adsbygoogle"
     style="display:inline-block;width:320px;height:70px"
     data-ad-client="ca-pub-4718925124330949"
     :data-ad-slot="this.slot">
     </ins>
  </div>
</template>
<script>
export default{
  props:{
    slot : String
  },
  mounted(){
    (adsbygoogle = window.adsbygoogle || []).push({});
  }
}
</script>