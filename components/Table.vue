<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left" v-for="item in dataHeaders" :key="item">
            {{ item }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in dataArray" :key="item.CountryCode">
          <td>{{ item.Country }}</td>
          <td>{{ format(item.TotalDeaths) }}</td>
          <td>{{ format(item.TotalConfirmed) }}</td>
          <td>{{ format(item.NewDeaths) }}</td>
          <td>{{ format(item.NewConfirmed) }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
export default {
  props: {
    dataArray: {
      type: Array,
      required: true,
    },
    dataHeaders: {
      type: Array,
      required: true,
    },
  },
  methods: {
    format(number) {
      return new Intl.NumberFormat().format(number)
    },
  },
}
</script>
