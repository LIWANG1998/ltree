<template>
  <div class="hello" id="hello"></div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from "vue-property-decorator";

interface Data {
  id: string;
  name: string;
  pid: string;
  level: number;
  open?: boolean;
}
@Component
export default class Ltree extends Vue {
  private data: Data[] = [];
  @Watch("data", { deep: true, immediate: true })
  private handler_data() {
    this.renders();
  }
  private setData() {
    this.data = [];
    this.data.push({
      id: "ltree0",
      name: "成都金遂",
      pid: "",
      level: 0,
      open: true,
    });
    this.data.push({
      id: "ltree1",
      name: "测试1",
      pid: "ltree0",
      level: 1,
      open: false,
    });
    for (let i = 0; i < 10; i++) {
      this.data.push({
        id: "ltree" + i + 2,
        name: "测试1-" + i,
        pid: "ltree1",
        level: 2,
      });
    }
    this.data.push({
      id: "ltree13",
      name: "测试2",
      pid: "ltree0",
      level: 1,
      open: false,
    });
    for (let i = 0; i < 500; i++) {
      this.data.push({
        id: "ltree" + i + 14,
        name: "测试2-" + i,
        pid: "ltree13",
        level: 2,
      });
    }
  }

  private renders() {
    const div = document.createElement("div");
    div.id = "ltree";
    for (let i = 0; i < this.data.length; i++) {
      div.appendChild(this.createVDom(this.data[i]));
    }
    console.log(div);
    const ltree = document.getElementById("ltree");
    if (ltree) {
      ltree.remove();
    }
    document.getElementById("hello")?.appendChild(div);
  }

  private createVDom(data: Data) {
    const div = document.createElement("div");
    div.className = "cell";
    div.addEventListener("click", () => {
      this.click(data);
    });
    div.style.transform = `translateX(${data.level * 30}px)`;
    div.style.display = this.isopen(data.pid, data.level) ? "block" : "none";
    const span = document.createElement("span");
    div.appendChild(span);
    span.innerHTML = data.name;
    return div;
  }

  private mounted() {
    this.setData();
    console.log(this.data);
    // this.renders();
  }

  private isopen(pid: string, level: number) {
    if (pid === "" || level === 0) {
      return true;
    }
    const _t = this.data.find((item) => item.id === pid);
    return _t ? _t.open : false;
  }
  private click(t: Data) {
    console.log(t);
    t.open = t.open ? !t.open : true;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
.hello {
  margin: 0 auto;
  width: 30%;
  text-align: left;
  #ltree {
    font-size: 16px;
    .cell {
      font-size: 14px;
      height: 30px;
      line-height: 30px;
      cursor: pointer;
      &:hover {
        color: tomato;
      }
    }
  }
}
</style>
