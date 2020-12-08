<template>
  <v-container :fluid="true" class="px-0 py-0">
    <!-- Main Footer -->
    <footer class="main-footer">
      <div class="auto-container">
        <div class="logo"></div>
        <ul class="footer-nav d-md-flex ">
          <li><a href="#">Home</a></li>
          <li><a href="#">Recipes</a></li>
          <li><a href="#">About us</a></li>
          <li><a href="#">Events</a></li>
          <li><a href="#">Blog</a></li>
          <li><a href="#">Contacts</a></li>
        </ul>
       
        <div class="copyright">&copy; All Right Reserved 2020</div>
      </div>
    </footer>
  </v-container>
</template>

<script>
export default {
  name: "Footer",

  data: () => ({}),
};
</script>
<style  scoped>
.main-footer {
  background: url(../assets/background/5.png);

  position: relative;
  text-align: center;
  padding: 75px 0px 0px;
  background-position: center bottom;
  background-repeat: no-repeat;
}
.auto-container {
  position: static;
  max-width: 1200px;
  padding: 0px 15px;
  margin: 0 auto;
}
.main-footer .footer-nav {
  margin: 25px 0px 30px;
  justify-content: space-around;

}
ul,
li {
  padding: 0px;
  margin: 0px;
}
.main-footer .copyright {
  position: relative;
  margin-top: 60px;
  color: #1c1c1c;
  font-size: 15px;
  padding: 25px 0px;
  border-top: 1px solid #e6e3e2;
}

.main-footer .footer-nav li a {
  position: relative;
  color: #262626;
  font-size: 24px;
  font-family: "Grand Hotel", cursive;
  text-decoration: none;
}

</style>