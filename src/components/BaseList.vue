<template>
  <div class="list-main">
    <h2>{{listTitle}}</h2>
    <ul class="list-wrapper">
      <li v-for="lineItem in listData" class="list-line-item">
        <div class="wrap">
          <div class="line-info-item item0">
            <a href="#" :class="['car-image',lineItem.car.carTypeImage]"></a>
            <span class="car-type">{{lineItem.car.carHeight}}米</span>
            <span class="car-type">{{lineItem.car.loadingType.desc}}</span>
          </div>
          <div class="line-info-item item1">
            <p class="start-address detail-item">
              {{lineItem.startAddress.province.name
              +lineItem.startAddress.city.name
              +lineItem.startAddress.district.name}}
            </p>
            <p class="car-volume detail-item">
              <span>载货体积：</span>
              {{lineItem.car.carLong}}*{{ lineItem.car.carHeight}} * {{lineItem.car.carWidth }}m
            </p>
          </div>
          <div class="line-info-item item2">
            <span class="car-hours">{{lineItem.hoursLength}}h</span>
            <span class="car-distance">{{lineItem.distance}}km</span>
          </div>
          <div class="line-info-item item3">
            <p class="end-address detail-item">
              {{lineItem.endAddress.province.name
              +lineItem.endAddress.city.name
              +lineItem.endAddress.district.name}}
            </p>
            <p class="car-load detail-item">
              <span>载货重量：</span>
              <span class="car-load-number">{{lineItem.car.carLoad}}吨</span>
            </p>
          </div>
          <div class="line-info-item item4">
            <p class="line-price">
              <span>一口价：￥</span>
              <span>{{lineItem.price}}</span>
            </p>
            <p class="usage-count">
              <span>累计已发：</span>
              <span>{{lineItem.usageCount}}车</span>
            </p>
          </div>
          <div class="line-info-item item5">
            <button class="btn-use-car">立即用车</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "BaseList",
  data() {
    return {
      listTitle: "BaseList",
      listData: [],
      carImagePath: "../assets/"
      // startLine:'',
      // endLine:''
    };
  },
  created() {
    import(`../assets/mockData.js`).then(mod => {
      let data = JSON.parse(JSON.stringify(mod));
      this.$nextTick(() => {
        this.listData.push(data.listData);
        console.log(this.listData);
      });
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
h1 ~ h6,
ul,
li,
a,
p,
span,
div,
button {
  padding: 0;
  margin: 0;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
div {
  display: inline-block;
}
.list-line-item {
  display: block;
  height: 100%;
  width: 100%;
  padding: 15px 0;
  border: 2px solid rgba(236, 221, 221, 0.4);
  .wrap {
    display: flex;
    align-items: center;
  }
  .wrap .line-info-item {
    display: inline-block;
    width: 200px;
    height: 100px;
    // border: 1px solid red;
    &.item1 {
      text-align: right;
      padding-top: 24px;
      box-sizing: border-box;
    }
    &.item2 {
      padding-top: 24px;
      box-sizing: border-box;
      position: relative;
      span {
        display: block;
        line-height: 25px;
      }
      .car-hours {
        &:after {
          content: "";
          height: 3px;
          position: absolute;
          width: 40px;
          background: #000;
          left: 82px;
          top: 48px;
        }
        &::before {
          content: "";
          position: absolute;
          top: 45px;
          left: 120px;
          height: 0;
          width: 0;
          border-top: 5px solid transparent;
          border-left: 10px solid #000;
          border-bottom: 5px solid transparent;
        }
      }
    }
    &.item3 {
      text-align: left;
      padding-top: 24px;
      box-sizing: border-box;
    }

    &.item4 {
      padding-top: 24px;
      box-sizing: border-box;
      .line-price span {
        color: #f59463;
        font-size: 20px;
      }
      .usage-count {
        color: #9a9696;
        font-size: 12px;
      }
    }
    &.item5 {
      line-height: 100px;
    }
    .start-address,
    .end-address {
      font-weight: 700;
    }
  }
}

.btn-use-car {
  background: #fa8802;
  color: #fff;
  border-color: #fa8802;
  border-radius: 4px;
  padding: 10px;
  display: inline-block;
  line-height: 1;
  white-space: nowrap;
  cursor: pointer;
  -webkit-appearance: none;
  text-align: center;
  box-sizing: border-box;
  outline: none;
  transition: 0.1s;
  font-weight: 500;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  padding: 12px 20px;
  font-size: 16px;
}
.car-image {
  cursor: default;
  width: 100%;
  display: inline-block;
  height: 80px;
  background: url(../assets/car0.png) no-repeat center center;
}
</style>
