<template>
    <div>
        <div class="main" v-if="list.length > 0">
            <div class="goods" v-for="(item, index) in list" :key="index">
                <span class="check">
                    <input type="checkbox" @click="selectGoods(index)" :checked="item.isSelect">
                </span>
                <span class="name">
                    <img :src="item.imgUrl">{{ item.itemName }}
                </span>
                <span class="unitPrize">{{ item.unitPrice }}元</span>
                <span class="num">
                    <span @click="reduce(index)" :class="{ off: item.number == 1 }">-</span>
                    {{ item.number }}
                    <span @click="increase(index)">+</span>
                </span>
                <span class="unitTotalPrize">{{ item.unitPrice * item.number }}元</span>
                <span class="operation"><a @click="remove(index)">删除</a></span>
            </div>
        </div>
        <div v-else>购物车为空</div>
        <div class="info">
            <span><input type="checkbox" @click="selectAll" :checked="isSelectAll">全选</span>
            <span>已选商品<span class="totalNUmber">{{ totalNumber }}</span>件</span>
            <span>合计:<span class="totalPrize">{{ totalPrize }}</span>元</span>
            <span>去结算</span>
        </div>
    </div>
</template>

<script>


export default {
    data: function () {
        return {
            isSelectAll: false, // 默认全未选
            list: [{
                imgUrl: require("@/assets/images/boqi.png"),
                itemName: "波奇酱",
                number: 3,
                unitPrice: 12,
                isSelect: false
            },
            {
                imgUrl: require("@/assets/images/summer.png"),
                itemName: "夏天",
                number: 1,
                unitPrice: 2699,
                isSelect: false
            },
            {
                imgUrl: require("@/assets/images/fj.jpg"),
                itemName: "风景",
                number: 2,
                unitPrice: 276,
                isSelect: false
            }
            ]
        }
    },
    computed: {
        totalNumber: function () { // 计算商品1件数
            var totalNumber = 0;
            this.list.forEach(function (item) {
                if (item.isSelect) {
                    totalNumber += 1;
                }
            });
            return totalNumber;
        },

        totalPrize: function () { // 计算商品总价
            var totalPrize = 0;
            this.list.forEach(function (item) {
                if (item.isSelect) {
                    totalPrize += item.number * item.unitPrice;
                }
            });
            return totalPrize;
        }
    },

    methods: {
        reduce: function (index) { // 减少商品件数
            var goods = this.list[index];
            if (goods.number >= 2) {
                goods.number--;
            }
        },

        increase: function (index) { // 增加商品件数
            var goods = this.list[index];
            goods.number++;
        },

        remove: function (index) { // 移除商品
            this.list.splice(index, 1);
        },

        selectGoods: function (index) { // 选择商品
            const goods = this.list[index];
            goods.isSelect = !goods.isSelect;
            this.isSelectAll = true;
            for (var i = 0; i < this.list.length; i++) {
                if (this.list[i].isSelect == false) {
                    this.isSelectAll = false;
                }
            }
        },

        selectAll: function () { // 全选或者全不选
            this.isSelectAll = !this.isSelectAll;
            for (var i = 0; i < this.list.length; i++) {
                this.list[i].isSelect = this.isSelectAll;
            }
        }

    }
}
</script>