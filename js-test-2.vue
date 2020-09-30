<template>
  <div class="row">
    <div class="col-6"><span class="text-center">Active {{ totalActiveCount }}</span></div>
    <div class="col-6"><span class="text-center">Inactive {{ totalInactiveCount }}</span></div>
    <table class="table">
      <thead>
      <tr>
        <th>#</th>
        <th>Mark</th>
        <th>Model</th>
        <th>Color</th>
        <th>Price</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(car, i) in cars">
        <td v-if="car.is_active">{{ car.id }}</td>
        <td v-if="car.is_active" @click="moreInfo(1)">{{ car.mark }}</td>
        <td v-if="car.is_active" @click="moreInfo(2)"> {{ car.model }}</td>

        <td v-if="car.is_active" @click="moreInfo(3)"> {{ car.color }}</td>
        <td v-if="car.is_active" @click="moreInfo(4)"> {{ car.price }}</td>
        <td v-if="car.is_active" @click="toggle(car, i)"> {{ car.is_active ? 'active' : 'inactive' }}</td>
      </tr>
      </tbody>
    </table>
    <hr>
    <table class="table">
      <tr v-for="(value, key) in moreInfoGroup">
        <td>{{ key }}</td>
        <td>{{ value.length }}</td>
      </tr>
    </table>

  </div>
</template>

<script>

export default {
  data() {
    return {
      cars: [
        {
          id: 12,
          mark: 'BMW',
          model: 'm3',
          color: 'red',
          price: 2500,
          is_active: true
        },
        {
          id: 88,
          mark: 'Ford',
          model: 'm3',
          color: 'blue',
          price: 785,
          is_active: false
        },
        {
          id: 789,
          mark: 'Dodge',
          model: 'mustang',
          color: 'black',
          price: 32485,
          is_active: true
        },
        {
          id: 24,
          mark: 'BMW',
          model: 'm7',
          color: 'red',
          price: 896,
          is_active: true
        },
        {
          id: 15,
          mark: 'Ford',
          model: 'Transit',
          color: 'green',
          price: 2500,
          is_active: false
        }

      ],
      moreInfoGroup: {},
      totalActiveCount: 0,
      totalInactiveCount: 0,
    };
  },
  created() {
    this.calcTotalActiveCount();
    this.calcTotalInactiveCount();
  },
  methods: {
    calcTotalActiveCount() {
      this.totalActiveCount = 0;
      this.cars.map((car) => {
        if (car.is_active) {
          this.totalActiveCount++;
        }
      })
    },
    calcTotalInactiveCount() {
      this.totalInactiveCount = 0;
      this.cars.map((car) => {
        if (car.is_active) {
          this.totalInactiveCount++;
        }
      })
    },
    toggle(car, i) {
      this.cars = this.cars.map((c) => {
        if (c.id === car.id) {
          if (c.is_active === true) {
            c.is_active = false;
          } else if (c.is_active === false) {
            c.is_active = true
          }
        }
        return c;
      })
    },
    moreInfo(k) {
      if (k === 1) {
        this.moreInfoGroup = this.cars.reduce((rv, x) => {
          (rv[x['mark']] = rv[x['mark']] || []).push(x);
          return rv;
        }, {});
      } else if (k === 2) {
        this.moreInfoGroup = this.cars.reduce((rv, x) => {
          (rv[x['model']] = rv[x['model']] || []).push(x);
          return rv;
        }, {});
      } else if (k === 3) {
        this.moreInfoGroup = this.cars.reduce((rv, x) => {
          (rv[x['color']] = rv[x['color']] || []).push(x);
          return rv;
        }, {});
      } else if (k === 4) {
        this.moreInfoGroup = this.cars.reduce((rv, x) => {
          (rv[x['price']] = rv[x['price']] || []).push(x);
          return rv;
        }, {});
      }
    }
  },
  watch: {
    cars() {
      this.calcTotalActiveCount();
      this.calcTotalInactiveCount();
    }
  }
};
</script>
