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
            <tr v-for="car in cars" v-bind:key="car.id">
                <td>{{ car.id }}</td>
                <td @click="moreInfo('mark')">{{ car.mark }}</td>
                <td @click="moreInfo('model')"> {{ car.model }}</td>
                <td @click="moreInfo('color')"> {{ car.color }}</td>
                <td @click="moreInfo('price')"> {{ car.price }}</td>
                <td @click="toggle(car)"> {{ car.is_active ? 'active' : 'inactive' }}</td>
            </tr>
            </tbody>
        </table>
        <hr>
        <table class="table">
            <tr v-for="(value, key) in moreInfoGroup" v-bind:key="key">
                <td>{{ key }}</td>
                <td>{{ value.length }}</td>
            </tr>
        </table>

    </div>
</template>

<script>

    export default {
        name: 'CarTable',
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
                moreInfoGroup: {}
            };
        },
        methods: {
            toggle(car) {
                car.is_active = !car.is_active;
            },
            moreInfo(type) {
                this.moreInfoGroup = this.cars.reduce((rv, x) => {
                    (rv[x[type]] = rv[x[type]] || []).push(x);
                    return rv;
                }, {});
            }
        },
        computed: {
            totalActiveCount: function () {
                let total = [];
                Object.entries(this.cars).forEach(([key, val]) => {
                    if (val.is_active)
                        total.push(val.is_active)
                });

                return total.length;

            },
            totalInactiveCount: function () {
                return this.cars.length - this.totalActiveCount;
            }
        }
    }
</script>
