# Custom Laravel Vue Pagination

``` Documentation ```
[Laravel Vue Pagination](https://laravel-vue-pagination.org/)

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


``` Custom Component ```
```js
<gpagination
  :data="laravelData"
  @pagination-change-page="getResults"
></gpagination>
```
```js
<template>
  <RenderlessPagination
    :data="data"
    :limit="limit"
    :keep-length="keepLength"
    @pagination-change-page="onPaginationChangePage"
    v-slot="slotProps"
  >
    <!-- <div
      class="pagination mt-4 d-flex justify-content-start justify-content-md-end"
      v-bind="$attrs"
      aria-label="Pagination"
      v-if="slotProps.computed.total > slotProps.computed.perPage"
    >
      <ul>
        <li class="arrow">
          <a
            href="#"
            :disabled="!slotProps.computed.prevPageUrl"
            v-on="slotProps.prevButtonEvents"
            ><i class="bi bi-arrow-left"></i
          ></a>
        </li>
        <li class="mid-pagi">
          <a
            href="#"
            :aria-current="slotProps.computed.currentPage ? 'page' : null"
            v-for="(page, key) in slotProps.computed.pageRange"
            :key="key"
            v-on="slotProps.pageButtonEvents(page)"
          >
            <a class="active" href="#"
              ><span>{{ page }}</span></a
            >
          </a>
        </li>
        <li class="arrow">
          <a href="#"
            ><i
              class="bi bi-arrow-right"
              :disabled="!slotProps.computed.nextPageUrl"
              v-on="slotProps.nextButtonEvents"
            ></i
          ></a>
        </li>
      </ul>
    </div> -->

    <div
      class="pagination mt-4 d-flex justify-content-start justify-content-md-end"
      v-bind="$attrs"
      aria-label="Pagination"
      v-if="slotProps.computed.total > slotProps.computed.perPage"
    >
      <ul>
        <li class="arrow">
          <a
            href="#"
            :disabled="!slotProps.computed.prevPageUrl"
            v-on="slotProps.prevButtonEvents"
            ><i class="bi bi-arrow-left"></i
          ></a>
        </li>

        <li class="mid-pagi">
          <a
            href="#"
            :class="`${
              slotProps.computed.currentPage == page ? 'active' : null
            } `"
            :aria-current="slotProps.computed.currentPage ? 'page' : null"
            v-for="(page, key) in slotProps.computed.pageRange"
            :key="key"
            v-on="slotProps.pageButtonEvents(page)"
          >
            <span>
              {{ page }}
            </span>
          </a>
        </li>
        <li class="arrow">
          <a href="#"><i class="bi bi-arrow-right"></i></a>
        </li>
      </ul>
    </div>
  </RenderlessPagination>
</template>

<script>
import RenderlessPagination from "laravel-vue-pagination/src/RenderlessPagination.vue";

export default {
  inheritAttrs: false,

  emits: ["pagination-change-page"],

  components: {
    RenderlessPagination,
  },

  props: {
    data: {
      type: Object,
      default: () => {},
    },
    limit: {
      type: Number,
      default: 0,
    },
    keepLength: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      activeClass: null,
    };
  },
  methods: {
    onPaginationChangePage(page) {
      this.$emit("pagination-change-page", page);
    },
  },
};
</script>

```
