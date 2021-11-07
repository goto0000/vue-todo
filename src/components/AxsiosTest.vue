<template>
      <main>
    <div>
      <h2>都道府県</h2>
      <div class="input_area">
        <input type="radio" id="hokkaido" value="北海道" v-model="value" @change="getPrefectures()" />
        <label for="hokkaido">北海道</label>
        <input type="radio" id="touhoku" value="東北" v-model="value" @change="getPrefectures()" />
        <label for="touhoku">東北</label>
        <input type="radio" id="kantou" value="関東" v-model="value" @change="getPrefectures()" />
        <label for="kantou">関東</label>
        <input type="radio" id="chubu" value="中部" v-model="value" @change="getPrefectures()" />
        <label for="chubu">中部</label>
        <input type="radio" id="kinki" value="近畿" v-model="value" @change="getPrefectures()" />
        <label for="kinki">近畿</label>
        <input type="radio" id="chugoku" value="中国" v-model="value" @change="getPrefectures()" />
        <label for="chugoku">中国</label>
        <input type="radio" id="shikoku" value="四国" v-model="value" @change="getPrefectures()" />
        <label for="shikoku">四国</label>
        <input
          type="radio"
          id="kyushu_okinawa"
          value="九州"
          v-model="value"
          @change="getPrefectures()"
        />
        <label for="kyushu_okinawa">九州沖縄</label>
      </div>
      <div class="result_area">
        <ul>
          <li v-for="item in result.response.prefecture" :key="item">{{ item }}</li>
        </ul>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import VueAxios from "vue-axios";
export default ({
    data() {
        return {
            value: "",
            result: {
                "response": {
                    "prefecture": []
                }
            },
            changed: false
        }
    },
  created () {
    axios.get("http://geoapi.heartrails.com/api/json", {
      params: {
        method: "getPrefectures",
        area: "北海道"
      }
    })
      .then(response => {
        this.result = response.data
      })
      .catch(err => {
        console.error(err)
      })
  },
    methods: {
        getprefectures: function() {
            this.axios.get("http://geoapi.heartrails.com/api/json", {
                params: {
                method: "getPrefectures",
                area: this.value
                }
            }).then(response => {
                this.result = response.data
            }).catch (err => {
                console.error(err)
            })
        }
    },
    plugins: {

    }
})
</script>

<style scoped>
main {
  height: calc(100vh - 152px);
  padding: 3% 0;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
}
h2 {
  margin-bottom: 1.5em;
}
.input_area {
  margin-bottom: 15%;
}
.result_area {
  min-height: 300px;
}
ul {
  padding-left: 0;
}
ul li {
  list-style: none;
}
</style>

