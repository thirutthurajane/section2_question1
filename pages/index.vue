<template>

    <table class="myTable">
      <tr>
        <td class="firstCol"></td>
        <td class="secondCol"></td>
        <td class="lastCol"></td>
      </tr>
      <tr>
        <td>
          <input type="text" placeholder="please input number" @change="calculate(curType)" v-model="number">
        </td>
        <td class="text-center">
          <b-dropdown style="max-width: 400px;" class="secondCol" v-bind:text="this.selectText">
            <b-dropdown-item @click="calculate(0)">isPrime</b-dropdown-item>
            <b-dropdown-item @click="calculate(1)">isFibonacci</b-dropdown-item>
          </b-dropdown>
        </td>
        <td>
          <span>{{ result }}</span>
        </td>
      </tr>
    </table>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      result: 'Not Calculate yet',
      number: 0,
      selectText: 'isPrime',
      curType: 0
    }
  },
  methods: {
    calculate(type) {
      this.curType = type;
      if(this.curType === null)
        return;
      this.selectText = type === 0 ? "isPrime" : "isFibonacci";
      let result = type === 0 ? this.isPrimeNumber(this.number) : this.isFibonacci(this.number);
      this.result = result;
    },
    isSquare(n) {
        return n > 0 && Math.sqrt(n) % 1 === 0;
    },
    isFibonacci(num) {
      if (this.isSquare(5*(num*num)-4) || this.isSquare(5*(num*num)+4)) {
        return true;
      } else { return false; }
    },
    isPrimeNumber(number) {
      let isPrime = true;

      if (number === 1) {
        return false;
      }

      else if (number > 1) {

        for (let i = 2; i < number; i++) {
          if (number % i == 0) {
            isPrime = false;
            break;
          }
        }

        return isPrime;
      } else {
        return false;
      }
    }
  }
}
</script>
<style scoped>
  .firstCol {
    width: 200px
  }
  .secondCol {
    width: 100%;
    align-content: center;
  }
  .lastCol {
    width: 300px
  }

  @media screen and (max-width: 600px){
    .secondCol {
      width: 100%;
      align-content: center;
      min-width: 100px;
    }
  }
</style>
