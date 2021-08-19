<template>
  <div class="main" id="main">
    <a href="https://github.com/JimmyAnso" target="_blank">
      <img
        class="main__logo"
        alt="Github Octocat logo"
        src="./assets/Octocat.png"
      />
    </a>

    <div class="profile">
      <img class="profile__img" :src="profile.avatar_url" alt="" />
      <h1 class="profile__name">{{ profile.login }}</h1>
      <p class="profile__follow">
        <img src="./assets/group.png" alt="" />
        followers：{{ profile.followers }} ● following：{{ profile.following }}
      </p>
      <p>
        <img src="./assets/url.png" alt="" /><a
          href="https://github.com/JimmyAnso"
          target="_blank"
          >https://github.com/JimmyAnso</a
        >
      </p>
      <p>
        <img src="./assets/message.png" alt="" /><a
          href="jimmy123698745@yahoo.com.tw"
          target="_blank"
          >jimmy123698745@yahoo.com.tw</a
        >
      </p>
    </div>

    <ul class="list" v-for="repo in myRepos" :key="repo">
      <li>
        <div class="attachment"></div>
      </li>

      <li class="list__li">
        <span class="list__li--title">專案名稱：</span>
        <span class="list__li--data">{{ repo.name }}</span>
      </li>
      <li class="list__li">
        <span class="list__li--title">專案描述：</span>
        <span class="list__li--data">{{ repo.description }}</span>
      </li>
      <li class="list__li">
        <span class="list__li--title">專案網址：</span>
        <span class="list__li--data">
          <a :href="repo.html_url" target="_blank">{{ repo.html_url }}</a>
        </span>
      </li>
      <li class="list__li">
        <span class="list__li--title">Demo網址：</span>
        <span class="list__li--data">
          <a :href="repo.html_url" target="_blank">{{ repo.homepage }}</a>
        </span>
      </li>
      <li class="list__li">
        <span class="list__li--title">建立時間：</span>
        <span class="list__li--data">{{ repo.created_at }}</span>
      </li>
      <li class="list__li">
        <span class="list__li--title">最後更新時間：</span>
        <span class="list__li--data">{{ repo.updated_at }}</span>
      </li>
    </ul>
    <a href="#main" class="back-to-top"></a>

    <img class="flot flot__1" src="./assets/daftpunktocat-guy.gif" alt="" />
    <img class="flot flot__2" src="./assets/daftpunktocat-thomas.gif" alt="" />
    <img class="flot flot__3" src="./assets/Octocat-ironcat.png" alt="" />
    <img class="flot flot__4" src="./assets/Octocat-momtocat.png" alt="" />
    <img class="flot flot__5" src="./assets/Octocat-poptocat.png" alt="" />
    <img class="flot flot__6" src="./assets/Octocat-spidertocat.png" alt="" />
    <img class="flot flot__7" src="./assets/Octocat-starwar.png" alt="" />
    <img class="flot flot__8" src="./assets/Octocat-waldocat.png" alt="" />
    <img class="flot flot__9" src="./assets/Octocat-goretocat.png" alt="" />
    <img class="flot flot__10" src="./assets/Octocat-riddlocat.png" alt="" />

  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      myRepos: [],
      profile: {},
    };
  },
  created() {
    this.getAPI();
    this.getProfile();
  },
  mounted() {
    window.addEventListener("scroll", this.isRefresh, true);

    const flots = document.querySelectorAll(".flot");

    flots.forEach(flot=>{
      // 隨機水平位置
      flot.style.left = `${Math.random() * 80}% `;
      // 使用 dataset 給予隨機滾動速率
      flot.dataset.speed = 0 - Math.random()*5;
      });
  },
  methods: {
    getProfile() {
      const options = {
        method: "GET",
        url: "https://api.github.com/users/JimmyAnso",
      };
      // axios(options);
      axios(options)
        .then((response) => {
          // handle success
          this.profile = response.data;
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
    getAPI() {
      const options = {
        method: "GET",
        url: "https://api.github.com/users/JimmyAnso/repos",
      };
      // axios(options);
      axios(options)
        .then((response) => {
          // handle success
          response.data.forEach((element) => {
            this.myRepos.push(element);
          });
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
    //判斷捲軸位置，若到底則重 call this.getAPI() 將資料 push 到 myRepos
    isRefresh() {

      const flots = document.querySelectorAll(".flot");

      flots.forEach(flot => {
        flot.style.transform = 
          `translateY( 
              ${window.pageYOffset * Number(flot.dataset.speed)}px
          )`;
        }
      );

      // document.documentElement：回傳目前 document 的根元素

      //scrollTop：視窗頂端 到 頁面頂端 的距離
      var scrollTop =
        document.documentElement.scrollTop || document.body.scrollTop;

      //clientHeight：視窗的高度
      var clientHeight =
        document.documentElement.clientHeight || document.body.clientHeight;

      //scrollHeight：頁面的高度
      var scrollHeight =
        document.documentElement.scrollHeight || document.body.scrollHeight;

      // scrollTop、clientHeight、scrollHeight： https://img2018.cnblogs.com/blog/1504647/201812/1504647-20181221155602294-354909265.png

      //滾動條件檢視
      // console.log(scrollTop + clientHeight + "--" + scrollHeight);

      if (scrollHeight - 200 <= scrollTop + clientHeight) {
        // isRefreshBool= false; 防止多次觸發 非同步API
        // this.isRefreshBool = false;

        console.log("Call API ~~~");
        this.getAPI();
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #2c3e50;
  color: white;
  padding: 50px 0;
}
* {
  margin: 0;
  padding: 0;
  list-style: none;
  scroll-behavior: smooth;
}
.main {
  margin: auto;
  position: relative;
  &__logo {
    margin-bottom: 30px;
    width: 300px;
    position: relative;
    animation: name duration timing-function delay iteration-count direction
      fill-mode;
    animation: picFloat 2s ease-in-out 0s infinite alternate;
    @keyframes picFloat {
      0% {
        transform: translatey(-10px) rotate(5deg);
      }
      25% {
        transform: translatey(-5px) rotate(-5deg);
      }
      75% {
        transform: translatey(5px) rotate(5deg);
      }
      100% {
        transform: translatey(10px) rotate(-5deg);
      }
    }
    &:hover {
      animation: picShake 0.2s linear 0.3s infinite alternate;
      @keyframes picShake {
        0% {
          transform: rotate(5deg);
        }
        100% {
          transform: rotate(-5deg);
        }
      }
    }
  }
}
.profile {
  border: 5px solid black;
  border-radius: 20px;
  padding: 50px 0;
  box-shadow: 0px 0px 10px 0px black;
  margin: 0 10px;
  &__img {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    margin-bottom: 50px;
  }
  p {
    margin-top: 20px;
    img {
      width: 20px;
      height: 20px;
      margin: 0 10px;
      vertical-align: bottom;
    }
    a {
      color: white;
      text-decoration: none;
      &:hover {
        color: skyblue;
      }
    }
  }
}
.list {
  // width: 60%;
  margin: 50px auto;
  position: relative;
  z-index: 99;
  & ~ .list::before {
    content: "";
    width: 100%;
    height: 2px;
    display: block;
    background-color: black;
    transform: translateY(-25px);
  }
  &__li {
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-around;
    margin: 10px 0;
    &--title {
      width: 120px;
      text-align: right;
    }
    &--data {
      width: 340px;
      text-align: left;
      a {
        color: skyblue;
        &:hover {
          color: lightblue;
        }
      }
    }
  }
}
.attachment {
  background: url("./assets/github-octocat-fire.png");
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: auto;
  height: 600px;
  margin: 0px 20px;
  opacity: 0.1;
  filter: blur(2px);
  animation: bgFloat 2s ease-in-out 0s infinite alternate;
  @keyframes bgFloat {
    0% {
      transform: translatey(-20px);
    }
    100% {
      transform: translatey(20px);
    }
  }
}
.back-to-top {
  background: #233241;
  width: 50px;
  height: 50px;
  position: fixed;
  bottom: 50px;
  right: 100px;
  border-radius: 5px;
  box-shadow: 0px 0px 10px 1px #233241;
  // position: relative;
  &:hover {
    transform: translateY(-5px);
  }
  &::before {
    content: "";
    width: 15px;
    height: 15px;
    border-left: 5px solid black;
    border-top: 5px solid black;
    position: absolute;
    top: 50%;
    right: 50%;
    transform: translate(50%, -25%) rotate(45deg);
  }
}
.flot {
  position: absolute;
  // top: 100vh;
  bottom: 0;
  width: 100px;
}

// breakpoints
@media screen and (min-width: 576px) {
}
@media screen and (min-width: 768px) {
  .main {
    width: 60%;
  }
}
@media screen and (min-width: 992px) {
  .main {
    width: 50%;
  }
}
@media screen and (min-width: 1200px) {
  .main {
    width: 40%;
  }
}
@media screen and (min-width: 1400px) {
  .main {
    width: 35%;
  }
}
</style>
