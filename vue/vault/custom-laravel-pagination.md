# Custom Laravel Vue Pagination

```Vue```

```js

import { Bootstrap5Pagination } from 'laravel-vue-pagination';
app.component('pagination', Bootstrap5Pagination);

```

```js
<template>
  <div class="employee-other-info mt-4">
    <h5>Genform Information</h5>

    <div class="main-info">
      <table class="table table-bordered">
        <thead>
          <tr>
            <th>Gx No</th>
            <th>Date</th>
            <th>Unit</th>
            <th>Description</th>
          </tr>
        </thead>
        <tbody>
          <template v-for="(item, index) in laravelData.data" :key="index">
            <tr>
              <td :rowspan="rowspan(item.record_description.length)">
                {{ item.gx_no }}
              </td>
              <td :rowspan="rowspan(item.record_description.length)">
                {{ $filter.enFormat(item.gx_date) }}
              </td>
              <td :rowspan="rowspan(item.record_description.length)">
                {{ item?.unit.name }}
              </td>
            </tr>
            <template
              v-for="(item, index) in item.record_description"
              :key="index"
            >
              <tr v-if="item.description !== null">
                <td>
                  {{ item.description }}
                </td>
              </tr>
            </template>
          </template>
        </tbody>
      </table>
      <h1>Hi</h1>
      <pagination
        :data="laravelData"
        @pagination-change-page="getResults"
      ></pagination>
    </div>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      data: {},
      laravelData: {},
    };
  },
  methods: {
    getRecords() {
      axios
        .get("get/employee-records", {
          params: {
            id: this.id,
          },
        })
        .then((res) => {
          this.data = res.data;
        });
    },
    rowspan(size) {
      let length = size + 1;
      return length;
    },
    getResults(page) {
      if (typeof page === "undefined") {
        page = 1;
      }
      axios.get("/get/employee-records?page=" + page).then((res) => {
        this.laravelData = res.data;
      });
    },
  },
  created() {
    this.getResults();
  },
};
</script>
```

```Controller```

```php
function getRecords(Request $request){
  $records = EmployeeRecord::query()
  ->with('unit')
      //->where('employee_id',$request->id)
      ->latest()
      ->paginate(1);
  
  return $records;
}
```
