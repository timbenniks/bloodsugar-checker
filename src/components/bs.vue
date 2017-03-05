<template>
  <main>
    <img src="../assets/logo.svg" width="100" class="logo" />
    <form>
      <input type="number" ref="bs" inputmode="numeric" pattern="[0-9]*" name="bloodsugar" v-model="mgdl" @keyup="calculateBloodsugar" placeholder="mg/dl" autofocus />
      <select name="when" v-model="when" @change="calculateBloodsugar">
        <option value="fasting">Fasting</option>
        <option value="before">Before meal</option>
        <option value="after">After meal</option>
      </select>
    </form>
    <figure class="results" v-bind:data-status="status">
      <div class="result mmll" v-if="mmll">
        {{ mmll }}
        <span>mml/l</span>
      </div>
      <div class="result mgdl" v-if="mgdl">
        {{ mgdl }}
        <span>mg/dl</span>
      </div>
    </figure>
  </main>
</template>

<script>
export default {
  name: 'bs',
  data () {
    return {
      mmll: '',
      mgdl: '',
      when: 'fasting',
      status: '',
      fasting: { low: 0, high: 95 },
      before: { low: 70, high: 100 },
      after: { low: 95, high: 140 }
    }
  },
  methods: {
    calculateBloodsugar () {
      this.mmll = ( this.mgdl / 18 ).toFixed( 1 );

      if( this.when === 'fasting' ){
        if( this.mgdl >= this.fasting.low && this.mgdl <= this.fasting.high ){
          this.status = 'good';
        }
        else {
          this.status = 'bad';
        }
      }

      if( this.when === 'before' ){
        if( this.mgdl >= this.before.low && this.mgdl <= this.before.high ){
          this.status = 'good';
        }
        else {
          this.status = 'bad';
        }
      }

      if( this.when === 'after' ){
        if( this.mgdl >= this.after.low && this.mgdl <= this.after.high ){
          this.status = 'good';
        }
        else {
          this.status = 'bad';
        }
      }
    }
  }
}
</script>

<style>
.logo {
  display: block;
  margin: 50px auto;
}

form {
  overflow: hidden;
  border: 2px solid #c63c22;
  width: 95%;
  margin: 0 auto;
}

input {
  width: calc( 50% - 30px );
  font-size: 15px;
  padding: 1em;
  background: #fff;
  border: none;
  border-radius: 0;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  float: left;
}

input:focus {
  outline: none;
}

select {
  width: 50%;
  font-size: 15px;
  padding: 1em;
  border: none;
  border-radius: 0;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  float: left;
  background: #f6f6f6 url( '../assets/dropdown.svg' );
  background-repeat: no-repeat;
  background-position: 92% 22px;
  background-size: 8%;
}

select:focus {
  background: #f6f6f6 url( '../assets/dropdown.svg' );
  background-repeat: no-repeat;
  background-position: 92% 22px;
  background-size: 8%;
  outline: 0;
}

figure.results {
  padding: 1em 0;
  display: flex;
  align-items: baseline;
  width: 95%;
  margin: 0 auto;
}

[data-status="good"]{
  background: #f0fff4;
  border: solid #cdefd6;
  border-width: 0 2px 2px 2px;
}

[data-status="bad"]{
  background: #fff0f0;
  border: solid rgba( 198, 60, 34, 0.23 );
  border-width: 0 2px 2px 2px;
}

.result {
  text-align: center;
  flex: 1;
}

.result.mmll,
.result.mgdl {
  font-size: 3.5em;
  line-height: 1.1;
}

.result.mmll span,
.result.mgdl span {
  font-size: 0.3em;
  display: block;
}
</style>