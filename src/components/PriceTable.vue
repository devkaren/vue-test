<template>
    <div>
        <el-row>
            <el-button type="success" @click="handleAdd()" :disabled="!addButton">Add price</el-button>
        </el-row>
        <el-table
                :data="tableData"
                :default-sort="{prop: 'price', order: 'ascending'}"
                style="width: 100%">
            <el-table-column
                    label="Price"
                    sortable
                    prop="price">
                <template slot-scope="scope">
                    <div v-if="scope.row.type === 'text'">
                        <span>{{ scope.row.price }}</span>
                    </div>
                    <div v-else>
                        <el-input placeholder="Please type price" v-model="scope.row.price"></el-input>
                    </div>
                </template>
            </el-table-column>
            <el-table-column
                    align="right">
                <template slot-scope="scope">
                    <el-button
                            size="mini"
                            v-if="scope.row.type === 'text'"
                            :disabled="!isEdit"
                            @click="handleEdit(scope.row)">Edit
                    </el-button>
                    <el-button
                            size="mini"
                            v-else
                            type="success"
                            @click="handleSave(scope.row)">Save
                    </el-button>
                    <el-button
                            size="mini"
                            type="danger"
                            @click="handleDelete(scope.row)">Delete
                    </el-button>
                </template>
            </el-table-column>
        </el-table>
    </div>
</template>

<script>
    export default {
        name: 'PriceTable',
        data() {
            return {
                tableData: [{
                    price: 20,
                    oldPrice: 20,
                    type: 'text',
                    new: false
                }, {
                    price: 30,
                    oldPrice: 30,
                    type: 'text',
                    new: false
                }],
                addButton: true,
                isEdit: true,
                activeRow: null
            }
        },
        created() {
            this.handleEscape();
        },
        methods: {
            handleAdd() {
                this.addButton = false;
                this.tableData.push({price: null, oldPrice: null, type: 'input', new: true});
            },
            handleEdit(row) {
                this.activeRow = row;
                this.isEdit    = false;
                this.addButton = false;
                row.type       = 'input';
            },
            handleSave(row) {
                row.oldPrice   = row.price;
                row.type       = 'text';
                this.addButton = true;
                this.isEdit    = true;
            },
            handleDelete(row) {
                this.$confirm('This will permanently delete the selected price. Continue?', 'Warning', {
                    confirmButtonText: 'OK',
                    cancelButtonText: 'Cancel',
                    type: 'warning'
                }).then(() => {
                    this.addButton = true;
                    this.isEdit    = true;

                    this.tableData.splice(this.tableData.indexOf(row), 1);
                    this.$message({
                        type: 'success',
                        message: 'Successfully deleted'
                    });
                });
            },
            handleEscape() {
                document.onkeydown = evt => {
                    evt = evt || window.event;

                    if (evt.keyCode === 27) {
                        this.activeRow.price = this.activeRow.oldPrice;
                        this.activeRow.type  = 'text';
                        this.isEdit          = true;
                        this.addButton       = true;
                    }
                }
            }
        }
    }
</script>
