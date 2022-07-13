<template>
  <div id="app">
    <b-card title="Card Title" no-body>
      <b-row>
        <b-col cols="2">
          <b-card-header header-tag="nav">
            <b-nav fill vertical>
              <!-- <img class="logo"  src="./assets/logo.png"> -->
              <b-img src="./assets/logo.png" fluid logo alt="Logo"></b-img>
              <b-nav-item to="/" exact exact-active-class="active"
                >Painel</b-nav-item
              >
              <b-nav-item to="/sobre" exact exact-active-class="active"
                >Sobre</b-nav-item
              >
            </b-nav>
          </b-card-header>
        </b-col>
        <b-col cols="10">
          <b-card-body>
            <router-view></router-view>
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Sora&display=swap");
.nav-link {
  padding: 10px;
  background-color: white;
  margin-top: 20px;
  border-radius: 10px;
  color: black;
  font-weight: bold;
  text-align: center;
  transition: 0.5s;
}

.nav-item .active {
  transition: 0.5s;
  background-color: purple;
  color:white;
}
#app {
  font-family: "Sora";
}
.card {
    background-color: #000;
}
</style>
