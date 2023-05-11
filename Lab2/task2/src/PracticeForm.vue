<template>
    <div class="container my-2">
        <div class="row my-1">
            <HeaderComponent/>
        </div>
        <div class="row my-1">
            <div class="col-4">
                <!-- <h4>Links Component</h4> -->
                <LinksComponent/>
            </div>
            <div class="col-8">
                <BodyComponent/>    
            </div>
        </div>
        <div class="row my-1">
            <FooterComponent/>
        </div>
    </div>
</template>

<script>
import LinksComponent from '@/components/LinksComponent.vue'
import HeaderComponent from '@/components/HeaderComponent.vue'
import FooterComponent from '@/components/FooterComponent.vue'
import BodyComponent from '@/components/BodyComponent.vue'
export default {
  // data
  // methods
  components:{
    LinksComponent,
    HeaderComponent,
    FooterComponent,
    BodyComponent
  }
}
</script>

<style>

</style>