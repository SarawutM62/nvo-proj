<template>
  <div>
<b-container class="bv-example-row">

  <div class="" >
    <b-row class="text-left">
         <b-col></b-col>

         <b-col cols="10" class="bg1">


    <h1>เลือกสินค้า</h1>
  <!--   <p><button v-on:click="logout">Logout</button></p> -->
    <h5>จำนวนการสั่งซื้อ {{ blogs.length }} </h5>

    <p><b-button pill variant="success" v-on:click="navigateTo('/blog/create')"> เลือกสินค้า </b-button></p>

<br>
    <div class="box1" v-for="blog in blogs" v-bind:key="blog.id">
      <p>ลำดับ: {{ blog.id }}</p>
      <p>ชื่อ: {{ blog.firstname }}</p>
      <p>นามสกุล: {{ blog.lastname }}</p>
      <p>รายการสินค้า: {{ blog.nroom }}</p>
      <p>จำนวนการสั่งซื้อ: {{ blog.pnum }}</p>
      <p>เบอร์โทรศัพท์: {{ blog.tel }}</p>
      <p>ที่อยู่ : {{ blog.other }}</p>
      <!-- <p>วันที่เริ่มต้น: {{ blog.dates }}</p>
      <p>เวลาที่เริ่มต้น: {{ blog.times }}</p>
      <p>วันที่สิ้นสุด: {{ blog.datee }}</p>
      <p>เวลาที่สิ้นสุด: {{ blog.timee }}</p>
      <p>อื่นๆ : {{ blog.other }}</p> -->
      <p>
        <b-button pill variant="warning" v-on:click="navigateTo('blog/'+blog.id)"> ตรวจสอบการสั่งซื้อ </b-button>
        <!-- <b-button pill variant="warning" v-on:click="navigateTo('/blog/edit/' + blog.id)"> แก้ไขการจอง </b-button> -->
        <b-button pill variant="danger" v-on:click="deleteBlog(blog)"> ยกเลิกการสั่งซื้อ</b-button>
      </p>
      
    </div>
    
</b-col>
      <b-col> </b-col>
     </b-row>

     </div>
</b-container>

  </div>
</template>
<script>
import BlogService from "@/services/BlogsService";
export default {
  data() {
    return {
      blogs: [],
    };
  },
  async created() {
    this.blogs = (await BlogService.index()).data;
  },
  methods: {

  /*   logout() {
      this.$store.dispatch("setToken", null);
      this.$store.dispatch("setUser", null);
      this.$router.push({
        name: "login",
      });
    },
    */
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteBlog(blog) {
      let result = confirm("คุณแน่ใจนะ ที่จะยกเลิกการจองห้องประชุม?");
      if (result) {
        try {
          await BlogService.delete(blog);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this.blogs = (await BlogService.index()).data;
    },
  },
};
</script>
<style scoped>

</style>