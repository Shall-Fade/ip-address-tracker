<template>
  <div class="result-container">
    <div class="wrapper">
      <div class="result-block">
        <div class="result-group">
          <h3 class="result-title">IP Address</h3>
          <p class="result-info">{{ ipInfo.ip }}</p>
        </div>
        <hr class="hr-line" />
        <div class="result-group">
          <h3 class="result-title">Location</h3>
          <p class="result-info">{{ ipInfo.region }}, {{ ipInfo.country }}</p>
        </div>
        <hr class="hr-line" />
        <div class="result-group">
          <h3 class="result-title">Timezone</h3>
          <p class="result-info">UTC {{ ipInfo.timezone }}</p>
        </div>
        <hr class="hr-line" />
        <div class="result-group">
          <h3 class="result-title">ISP</h3>
          <p class="result-info">{{ ipInfo.isp }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["ipInfo"],
};
</script>

<style scoped>
.result-container {
  position: absolute;
  top: 230px;
  right: 0;
  left: 0;
}
.result-block {
  text-align: left;
  min-height: 140px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: var(--c-white);
  padding: 35px;
  border-radius: 15px;
}
.result-group {
  max-width: 350px;
}
.result-title {
  font-size: 14px;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--c-dark-gray);
  padding-bottom: 10px;
}
.result-info {
  font-size: 26px;
  font-weight: 700;
  color: var(--c-very-dark-gray);
}
.hr-line {
  border: 1px solid var(--c-dark-gray);
  border-radius: 50px;
  height: 70px;
}

@media only screen and (max-width: 1440px) {
  .result-block {
    width: 1200px;
    margin: 0 auto;
  }
}
@media only screen and (max-width: 1024px) {
  .result-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  .result-group {
    padding: 10px 0;
  }
  .result-title {
    font-size: 12px;
    padding-bottom: 0;
  }
  .result-info {
    font-size: 18px;
  }
  .hr-line {
    display: none;
  }
}
@media only screen and (max-width: 768px) {
  .result-block {
    width: 500px;
    margin: 0 auto;
  }
  .result-group {
    padding: 5px 0;
  }
  .result-title {
    font-size: 14px;
    padding-bottom: 0;
  }
  .result-info {
    font-size: 16px;
  }
}
@media only screen and (max-width: 425px) {
  .result-title {
    font-size: 10px;
    padding-bottom: 0;
  }
  .result-block {
    width: 350px;
    margin: 0 auto;
  }
}
@media only screen and (max-width: 375px) {
  .result-info {
    font-size: 16px;
  }
}
</style>
