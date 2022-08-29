<template>
  <section id="app">
    <BeeHive>
      <BeeHiveRow
        v-for="(career, index) in sampleData.levels"
        :index="index + 1"
        :children="career.roles.length"
        :key="index"
        :rowBefore="getRowBeforeChildren(index)"
        :label="career.id"
      >
        <BeeHiveItem
          v-for="role in career.roles"
          :key="role.id"
          :color="role.color"
          :item="{...role, level: career.id}"
          :active="role.id === selectedItem?.id"
          @select="selectHandler"
        >
          <p class="hexagon__title">
            {{role.name}}
          </p>
        </BeeHiveItem>
      </BeeHiveRow>
    </BeeHive>
  </section>
</template>

<script>
import Vue from 'vue';
// Uncomment import and local "components" registration if library is not registered globally.
import { BeeHive, BeeHiveRow, BeeHiveItem } from '@/entry.esm';

export default Vue.extend({
  name: 'ServeDev',
  components: {
   BeeHive,
   BeeHiveRow,
   BeeHiveItem
  },
  data: function () {
    return {
      selectedItem: {},
      sampleData: {
        id: "cfo",
        levels: [
          {
            id: "A",
            roles: [
              {
                id: "bu-exec",
                name: "Business Executive",
                track: "Domain & Industry",
                skills: [
                  "Manage Communication in Crisis",
                  "Implement Communications Program",
                  "Manage Client Experience",
                ],
              },
            ],
          },

          {
            id: "B",
            roles: [
              {
                id: "ppl-mgr",
                name: "People Manager",
                track: "Domain & Industry",
                skills: [
                  "Lead Change",
                  "Apply Project Management",
                  "Perform Conflict Resolution",
                ],
              },
              {
                id: "del-mgr",
                name: "Delivery Manager",
                track: "Domain & Industry",
                skills: [
                  "Lead Change",
                  "Apply Project Management",
                  "Apply Knowledge of Contracts",
                  "Perform Conflict Resolution",
                ],
              },
            ],
          },
          {
            id: "C",
            roles: [
              {
                id: "acc-analyst",
                name: "Accounting Analyst",
                track: "Technical",
                skills: [
                  "Apply Business Knowledge",
                  "Problem Solving",
                  "Apply Audit Standards",
                  "Implement Change For Automation",
                  "Perform Contract Review",
                ],
              },
              {
                id: "admin",
                name: "Administrator",
                track: "Technical",
                skills: [
                  "Apply Business Knowledge",
                  "Problem Solving",
                  "Apply Knowledge of Contracts",
                ],
              },
              {
                id: "tc",
                name: "Technical Consultant",
                track: "Technical",
                skills: [
                  "Design Process Integration",
                  "Understanding of IBM Garage Services",
                  "Perform Cloud Advisor Role",
                  "Advise on IT Process Models",
                  "Apply Knowledge of Lean/Agile Principles",
                  "Perform Workshop Facilitation",
                ],
              },
              {
                id: "data_sci",
                name: "Data Scientist",
                track: "Technical",
                skills: [
                  "Apply Problem Solving Techniques",
                  "Analyze Large Data Sets",
                  "Use Statistical & Analytical Techniques",
                  "Apply Project Management",
                ],
              },
            ],
          },
          {
            id: "D",
            roles: [
              {
                id: "intern",
                name: "Student/Intern",
                track: "Technical",
                skills: ["Use Communication Skills", "Maintain Product Knowledge"],
              },
            ],
          },
        ],
      }
    }
  },
  methods: {
    getRowBeforeChildren(index) {
      if(index > 0) {
        return this.sampleData.levels[index-1].roles.length;
      }  
	  },
    selectHandler(item) {
      if (item.id === this.selectedItem?.id) {
        this.selectedItem = {};
        return;
      }

      this.selectedItem = item;
    }
  }
}
);
</script>

<style>
  #app {
    width: 50vw;
    height: 50vh;
  }
</style>