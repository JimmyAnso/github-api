<template>
  <div class="main">
    <a href="https://github.com/JimmyAnso" target="_blank">
      <img
        class="main__logo"
        alt="Github Octocat logo"
        src="./assets/Octocat.png"
      />
    </a>
    <ul class="list" v-for="repo in myRepos" :key="repo">
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
        <span class="list__li--title">建立時間：</span>
        <span class="list__li--data">{{ repo.created_at }}</span>
      </li>
      <li class="list__li">
        <span class="list__li--title">最後更新時間：</span>
        <span class="list__li--data">{{ repo.updated_at }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      myRepos: {},
    };
  },
  created() {
    this.getAPI();
    console.log("create:");
  },
  methods: {
    getAPI() {
      const options = {
        method: "GET",
        url: "https://api.github.com/users/JimmyAnso/repos",
      };
      // axios(options);
      axios(options)
        .then((response) => {
          // handle success
          console.log(response);
          this.myRepos = response.data;
          console.log(this.myRepos);
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
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
}
.main {
  margin: auto;
  &__logo {
    width: 300px;
    position: relative;
    animation: picFloat 1s linear 0s infinite alternate;
    @keyframes picFloat {
      0% {
        transform: translatey(-10px);
      }
      100% {
        transform: translatey(10px);
      }
    }
    &:hover{
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
.list {
  // width: 60%;
  margin: 50px auto;
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
