<template>
  <div class="score">
    <div class="title-red">Maladie de Waldenstrom</div>
    <div class="sous-title">
      International Prognostic Scoring System for Waldenstrom Macroglobulinemia
    </div>
    <hr style="background-color: #000" />
    <div class="title-purple">Estimate prognosis with the IPPSWM</div>

    <div>
      <div class="question">
        <div class="question-title">Age</div>
        <div class="response">
          <div id="years-0" class="button years" @click="select(0, 'years')">
            ≤65 years
          </div>
          <div id="years-1" class="button years" @click="select(1, 'years')">
            >65 years
          </div>
        </div>
      </div>

      <div class="question">
        <div class="question-title">Hemoglobin</div>
        <div class="response">
          <div
            id="hemoglobin-0"
            class="button hemoglobin"
            @click="select(0, 'hemoglobin')"
          >
            <span>>115 g/L</span><br />
            <span class="button-info">>11.5 g/dL</span>
          </div>
          <div
            id="hemoglobin-1"
            class="button hemoglobin"
            @click="select(1, 'hemoglobin')"
          >
            <span>≤115 g/L</span> <br />
            <span class="button-info">≤11.5 g/dL</span>
          </div>
        </div>
      </div>
      <div class="question">
        <div class="question-title">Platelets</div>
        <div class="response">
          <div
            id="platelets-0"
            class="button platelets"
            @click="select(0, 'platelets')"
          >
            >100 x10⁹/L
          </div>
          <div
            id="platelets-1"
            class="button platelets"
            @click="select(1, 'platelets')"
          >
            ≤100 x10⁹/L
          </div>
        </div>
      </div>
      <div class="question">
        <div class="question-title">Beta-2-microglobulin</div>
        <div class="response">
          <div
            id="microglobulin-0"
            class="button microglobulin"
            @click="select(0, 'microglobulin')"
          >
            ≤3 mg/L
          </div>
          <div
            id="microglobulin-1"
            class="button microglobulin"
            @click="select(1, 'microglobulin')"
          >
            >3 mg/L
          </div>
        </div>
      </div>
      <div class="question">
        <div class="question-title">IgM</div>
        <div class="response">
          <div id="igm-0" class="button igm" @click="select(0, 'igm')">
            ≤7 g/dL
          </div>
          <div id="igm-1" class="button igm" @click="select(1, 'igm')">
            >7 g/dL
          </div>
        </div>
      </div>
    </div>
    <div
      v-if="
        years != null &&
        igm != null &&
        microglobulin != null &&
        platelets != null &&
        hemoglobin != null
      "
    >
      <div class="consequence">
        Prognosis
        <br /><br />
        {{ mounth[result - 1] }}
      </div>
    </div>
    <div class="about">
      <div class="title-about">EVIDENCE APPRAISAL</div>
      <div class="about-text">
        The IPSSWM was derived after merging a cohort of patients with WM from 7
        international co-operative groups. The IPSSWM speicifcially focuse on
        symptomatic patinets requiring therapy, and the majority were treated
        with standard therapies including alkylating agents, purine analogs, and
        rituximab.
      </div>
    </div>
    <div class="link">
            <div class="link-title">
                References
            </div>
            <div class="link-subTitle">
                Morel P, Duhamel A, Gobbi P, Dimopoulos MA, Dhodapkar MV, McCoy J, Crowley J, Ocio EM, Garcia-Sanz R, Treon SP, Leblond V, Kyle RA, Barlogie B, Merlini G.
            </div>
            <div class="linkUrl">
                <a href="https://read.qxmd.com/read/19196866/international-prognostic-scoring-system-for-waldenstrom-macroglobulinemia" target="_blank">International prognostic scoring system for Waldenstrom macroglobulinemia. Blood. 2009 Apr 30;113(18):4163-70. doi: 10.1182/blood-2008-08-174961. Epub 2009 Feb 5.</a>
            </div>
            <div class="linkUrl">
                <a href="https://qxmd.com/calculate/calculator_610/international-prognostic-scoring-system-for-waldenstrom-macroglobulinemia" target="_blank">The International Prognostic Scoring System for Waldenstrom Macroglobulinemia calculator is created by QxMD.</a>
            </div>
        </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "Maladie de Waldenstrom",
  data() {
    return {
      mounth: [
        "Risque faible: OS à 5 ans 87%, survie médiane 142,5 mois",
        "Risque intermédiaire: OS à 5 ans 68%, survie médiane 98,6 mois",
        "Risque élevé: OS à 5 ans 36%, survie médiane 43,5 mois",
      ],
      result: null,
      years: null,
      igm: null,
      microglobulin: null,
      platelets: null,
      hemoglobin: null,
    };
  },

  mounted() {},

  methods: {
    select: function (value, input) {
      let holdSelec = document.getElementsByClassName(
        input + " button-selected"
      );
      let newSelec = document.getElementById(input + "-" + value);

      if (holdSelec[0]) {
        if (holdSelec[0] != newSelec) {
          holdSelec[0].classList.remove("button-selected");
          newSelec.classList.add("button-selected");
        }
      } else {
        newSelec.classList.add("button-selected");
      }

      switch (input) {
        case "years":
          this.years = value;
          break;

        case "igm":
          this.igm = value;
          break;

        case "microglobulin":
          this.microglobulin = value;
          break;

        case "platelets":
          this.platelets = value;
          break;

        case "hemoglobin":
          this.hemoglobin = value;
          break;
      }
      this.calcul();
    },

    calcul: function () {
      this.result =
        this.hemoglobin +
        this.platelets +
        this.microglobulin +
        this.igm +
        this.years;
      if (this.years == 0 && this.result <= 1) {
        this.result = 1;
      } else if (this.years == 1 || this.result == 2) {
        this.result = 2;
      } else {
        this.result = 3;
      }
    },
  },
});
</script>

<style>
</style>