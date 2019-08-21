<template>
  <div id="app">
    <b-container>
      <b-table :fields="fields" :items="items" foot-clone>
        <!-- THIS IS BROKEN -->
        <template v-slot:[name]="data">
          {{ data.value.first }} {{ data.value.last }}
        </template>
        <!-- THIS WORKS NICELY -->
        <!-- <template slot="[name]" slot-scope="data">
          {{ data.value.first }} {{ data.value.last }}
        </template> -->

        <!-- A custom formatted header cell for field 'name' -->
        <template v-slot:HEAD[name]="data">
          <span class="text-info"
            ><b>{{ data.label }}</b></span
          >
        </template>

        <!-- A custom formatted footer cell for field 'name' -->
        <template slot="FOOT[name]" slot-scope="data">
          <span class="text-danger">{{ data.label }}</span>
        </template>

        <!-- Default fall-back custom formatted footer cell -->
        <template slot="FOOT[]" slot-scope="data">
          <i>{{ data.label }}</i>
        </template>
 
       <!-- WORKS-->
        <!-- <template slot="[]">
          Override everything
        </template>  -->

        <!-- NOT WORKING with v-slot directive -->
        <!-- <template v-slot:[]>
          Override everything
        </template> -->
      </b-table>
    </b-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // name: 'name',
      fields: [
        // A column that needs custom formatting
        { key: "name", label: "Full Name" },
        // A regular column
        "age",
        // A regular column
        "sex"
      ],
      items: [
        { name: { first: "John", last: "Doe" }, sex: "Male", age: 42 },
        { name: { first: "Jane", last: "Doe" }, sex: "Female", age: 36 },
        { name: { first: "Rubin", last: "Kincade" }, sex: "Male", age: 73 },
        {
          name: { first: "Shirley", last: "Partridge" },
          sex: "Female",
          age: 62
        }
      ]
    };
  }
};
</script>

<style>
</style>
