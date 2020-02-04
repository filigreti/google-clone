<template>
  <main>
    <main class="home">
      <img class="logo" src="@/assets/google.png" alt />
      <div class="input-cont">
        <img class="icon" src="@/assets/search.svg" alt />
        <input
          @keydown.enter="send"
          :class="[check ? 'input-new' :'input-box']"
          type="text"
          v-model.trim="search"
          name
          id
        />
      </div>

      <div class="search-button" :class="{'new':check}">
        <div :class="{line:check}"></div>
        <div class="auto-area">
          <autocomplete
            :search="search"
            class="box"
            :searched="getSearch"
            @checkValue="check = $event"
          />
        </div>
        <div :class="{'center-area':check}">
          <button @click="send" class="search">Google Search</button>
          <button class="feeling">
            <a href="https://www.google.com/doodle" target="_blank">I'm Feeling Lucky</a>
          </button>
        </div>
      </div>
    </main>
    <main class="footer">
      <div class="center">Nigeria</div>
      <div class="justify-center">
        <div>Created By Charles</div>
        <div>SeamlessHR Test</div>
      </div>
    </main>
  </main>
</template>

<script>
import autocomplete from "../components/AutoComplete";
import mock from "../utils/mock.json";

export default {
  name: "home",
  data() {
    return {
      search: "",
      check: false
    };
  },

  components: {
    autocomplete
  },
  computed: {
    getSearch() {
      if (this.search !== "") {
        this.check = true;
        return mock.filter(searched => {
          return searched.name.toLowerCase().match(this.search.toLowerCase());
        });
      } else {
        this.check = false;
        return [];
      }
    }
  },
  methods: {
    clear() {
      (this.search = ""), (this.check = false);
    },
    send() {
      if (this.search !== "") {
        let newSearch;
        newSearch = this.getSearch;
        this.$router.push({
          name: "view",
          params: {
            data: newSearch,
            searched: this.search,
            clicked: false
          }
        });
      }
    }
  }
};
</script>


<style >
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  height: 88vh;
  overflow: hidden;
  box-sizing: border-box;
  padding-bottom: 140px;
}
.home .logo {
  height: 92px;
  width: 272px;
}
.input-cont {
  width: 45%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 25px;
  position: relative;
}
.icon {
  fill: #9aa0a6;
  height: 20px;
  width: 20px;
  position: absolute;
  left: 20px;
}
.input-box {
  height: 44px;
  width: 100%;
  border-radius: 24px;
  border: 1px solid #dfe1e5;
  outline: none;
  font-size: 16px;
  padding-left: 50px;
}
.input-new {
  height: 44px;
  width: 100%;
  border-top-left-radius: 24px;
  border-top-right-radius: 24px;
  border: 0;
  box-shadow: 0 1px 6px 0 rgba(32, 33, 36, 0.28);
  border-color: rgba(223, 225, 229, 0);
  outline: none;
  font-size: 16px;
  padding-left: 50px;
}

.input-box:hover,
.input-box:focus {
  box-shadow: 0 1px 6px 0 rgba(32, 33, 36, 0.28);
  border-color: rgba(223, 225, 229, 0);
}
.search-button button {
  background-color: #f2f2f2;
  border: 1px solid #f2f2f2;
  border-radius: 4px;
  height: 36px;
  outline: none;
  color: #5f6368;
  font-size: 14px;
  padding: 0 20px;
  margin-top: 33px;
  font-weight: 400;
}
.line {
  border: 0.5px solid #e8eaed !important;
  padding: 0 10px;
  margin: 0 15px;
}
.search-button {
  position: fixed;
  margin-top: 120px;
}
.search-button button:hover {
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  background-image: -webkit-linear-gradient(top, #f8f8f8, #f1f1f1);
  background-color: #f8f8f8;
  border: 1px solid #c6c6c6;
  color: #222;
}
.footer {
  background: #f2f2f2;
  width: 100%;
  height: 11.8vh;
  color: #5f6368;
  border-top: 1px solid #e4e4e4;

  box-sizing: border-box;
}
.search {
  margin-right: 5px;
}
.center {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #e4e4e4;
  padding: 0 30px;
  font-size: 14px;
  height: 45%;
}
.feeling {
  margin-left: 5px;
}
.feeling a {
  color: #5f6368;
  text-decoration: none;
}
.justify-center {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
  padding: 0 30px;
  height: 45%;
}
.new {
  width: 45%;
  height: auto;
  overflow: hidden;
  box-shadow: 0 4px 6px 0 rgba(32, 33, 36, 0.28);
  top: 29%;
  z-index: 2;
  background: white;
  border: 0px;
  position: fixed;
  border-bottom-left-radius: 24px;
  border-bottom-right-radius: 24px;
}
.center-area {
  width: 100%;
  display: flex;
  align-items: center;
  height: 80px;
  justify-content: center;
  margin-bottom: 20px;
}

/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {
  .input-cont {
    width: 90%;
  }
  .new {
    width: 90%;
  }
  .content {
    display: flex !important;
  }
  .content-cont {
    margin-left: 30px !important;
    display: flex;
    align-items: center;
    position: relative;
    width: 63px;
    padding-bottom: 15px;
  }
  .content-cont:after {
    position: absolute;
    content: "";
    height: 3px;
    width: 100%;
    background: #1a73e8;
    bottom: 0;
    left: -10px;
  }
  .main-body {
    margin-left: 30px !important;
  }
  .w-55 {
    width: 90% !important;
  }
}
</style>