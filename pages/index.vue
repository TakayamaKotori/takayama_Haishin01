<template>
  <div class="container">
    <div style="width:100%;">
      <div style="margin-left: 15px;margin-top:30px;">
        <svg viewBox="0 0 200 100">
          <text
            class="layer-4"
            x="0"
            y="50%"
            v-bind:style="{fontSize: fontsizeint + 'px','stroke-width':strokewidth4,stroke:strokeColor4}"
          >{{outtext}}</text>
          <text
            class="layer-3"
            x="0"
            y="50%"
            v-bind:style="{fontSize: fontsizeint + 'px','stroke-width':strokewidth3,stroke:strokeColor3}"
          >{{outtext}}</text>
          <text
            class="layer-2"
            x="0"
            y="50%"
            v-bind:style="{fontSize: fontsizeint + 'px','stroke-width':strokewidth2,stroke:strokeColor2}"
          >{{outtext}}</text>
          <text
            class="layer-1"
            x="0"
            y="50%"
            v-bind:style="{fontSize: fontsizeint + 'px',fill:foreColer}"
          >{{outtext}}</text>
        </svg>
      </div>
    </div>
    <div style="width:70%;background-color: #FFA0A0;">
      <div>
        <div>
          Font-size:
          <el-input-number
            v-model="fontsizeint"
            @change="handleChange"
            :min="1"
            :max="300"
            size="mini"
          ></el-input-number>
        </div>
        <div>
          <div>
            out-line-size-4:
            <el-input-number
              v-model="strokewidth4"
              @change="handleChange"
              :min="strokewidth3"
              :max="300"
              size="mini"
            ></el-input-number>
          </div>
          <div>
            out-line-size-3:
            <el-input-number
              v-model="strokewidth3"
              @change="handleChange"
              :min="strokewidth2"
              :max="strokewidth4"
              size="mini"
            ></el-input-number>
          </div>
          <div>
            out-line-size-2:
            <el-input-number
              v-model="strokewidth2"
              @change="handleChange"
              :min="1"
              :max="strokewidth3"
              size="mini"
            ></el-input-number>
          </div>
        </div>
        <div>
          out-line-color-4:
          <el-color-picker v-model="strokeColor4" size="mini"></el-color-picker>out-line-color-3:
          <el-color-picker v-model="strokeColor3" size="mini"></el-color-picker>out-line-color-2:
          <el-color-picker v-model="strokeColor2" size="mini"></el-color-picker>font-color:
          <el-color-picker v-model="foreColer" size="mini"></el-color-picker>
        </div>
        <div>
          <el-checkbox v-model="boldchecked" @change="handleChange" size="mini">bold</el-checkbox>
        </div>
        <div>
          <el-button size="mini" @click="presetChange(1)">preset1</el-button>
          <el-button size="mini" @click="presetChange(2)">preset2</el-button>
          <el-button size="mini" @click="presetChange(3)">preset3</el-button>
          <el-button size="mini" @click="presetChange(4)">preset4</el-button>
          <el-button size="mini" @click="presetChange(5)">preset5</el-button>
        </div>
      </div>
      <div style="margin-top:25px;">
        display-text:
        <el-input placeholder="Please input" @change="handleChange" v-model="inputtext"></el-input>
        <el-input-number v-model="num1" @change="handleChange" :min="1" :max="99" size="mini"></el-input-number>
        <el-input-number v-model="num2" @change="handleChange" :min="1" :max="99" size="mini"></el-input-number>
        <el-input-number v-model="num3" @change="handleChange" :min="1" :max="99" size="mini"></el-input-number>
        <el-input-number v-model="num4" @change="handleChange" :min="1" :max="99" size="mini"></el-input-number>
        <el-input-number v-model="num5" @change="handleChange" :min="1" :max="99" size="mini"></el-input-number>
        <el-input-number v-model="num6" @change="handleChange" :min="1" :max="99" size="mini"></el-input-number>
        <el-input-number v-model="num7" @change="handleChange" :min="1" :max="99" size="mini"></el-input-number>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

// 存在チェック
if (String.prototype.format == undefined) {
  /**
   * フォーマット関数
   */
  String.prototype.format = function(arg) {
    // 置換ファンク
    var rep_fn = undefined;

    // オブジェクトの場合
    if (typeof arg == "object") {
      rep_fn = function(m, k) {
        return arg[k];
      };
    }
    // 複数引数だった場合
    else {
      var args = arguments;
      rep_fn = function(m, k) {
        return args[parseInt(k)];
      };
    }

    return this.replace(/\{(\w+)\}/g, rep_fn);
  };
}

export default {
  components: {},
  data() {
    return {
      inputtext: "最高順位：{0}位",
      num1: 1,
      num2: 1,
      num3: 1,
      num4: 1,
      num5: 1,
      num6: 1,
      num7: 1,
      outtext: "",
      fontsizeint: 12,
      boldchecked: true,
      fontwight: "400",
      strokewidth2: 4,
      strokewidth3: 8,
      strokewidth4: 4,
      foreColer: "#fff",
      strokeColor2: "#000",
      strokeColor3: "#0048FF",
      strokeColor4: "#000000",
      preset1: { out4: "#000", out3: "#fff", out2: "#000", fontcolor: "#fff" }
    };
  },
  methods: {
    presetChange(num) {
      console.debug(num);
      if (num == 1) {
        this.presetChangeInner(this.preset1);
      }
    },
    presetChangeInner(preset) {
      this.foreColer = preset.fontcolor;
      this.strokeColor2 = preset.out2;
      this.strokeColor3 = preset.out3;
      this.strokeColor4 = preset.out4;
    },
    handleChange() {
      console.log("handoleChange");
      this.outtext = this.inputtext.format(
        this.num1,
        this.num2,
        this.num3,
        this.num4,
        this.num5,
        this.num6,
        this.num7
      );

      if (this.boldchecked) {
        this.fontwight = "700";
      } else {
        this.fontwight = "400";
      }
    }
  },
  created: function() {
    this.handleChange();
  }
};
</script>

<style>
svg {
  display: inline-block;
  width: 250px;
  height: auto;
  overflow: visible;
}

.layer-4,
.layer-3,
.layer-2 {
  stroke-linejoin: round;
}
</style>
