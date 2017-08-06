<template>
  <v-app light class="elevation-5">
    <main>
      <header class="elevation-3">
        <span><strong>trip</strong>tip</span>
      </header>
      <form class="query-input" @submit.prevent="findHotel">
        <v-text-field
          name="query-input"
          label="Place your query here"
          v-model="query"
        ></v-text-field>
      </form>
      <v-data-table
        v-bind:headers="headers"
        :items="hotels"
        hide-actions
        class="elevation-1"
      >
        <template slot="items" scope="props">
          <td>{{ props.item.name }}</td>
          <td class="text-xs-right">{{ props.item.address }}</td>
          <td class="text-xs-right">{{ props.item.lat }}</td>
          <td class="text-xs-right">{{ props.item.lng }}</td>
        </template>
      </v-data-table>
    </main>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      query: '',
      hotels: [],
      headers: [
        {
          text: 'Name',
          align: 'left',
          sortable: true,
          value: 'name'
        },
        {
          text: 'Address',
          align: 'left',
          sortable: true,
          value: 'address'
        },
        {
          text: 'Lattitude',
          align: 'left',
          sortable: true,
          value: 'lat'
        },
        {
          text: 'Longitude',
          align: 'left',
          sortable: true,
          value: 'lng'
        },
      ]
    };
  },
  methods: {
    findHotel() {
      axios.get(`http://localhost:3031?q=${this.query}`)
      .then((response) => {
        this.hotels.length = 0;
        response.data.forEach(hotel => this.hotels.push(hotel));
      });
    },
  },
};
</script>

<style lang="stylus">
  @import './stylus/main'
</style>
