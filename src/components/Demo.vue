<template>
    <div>
        <div class="img-total">
            请输入图片数：<input v-model="imgTotal" type="number" />
        </div>
        <div class="img-col-size">
            每列显示数量：<input v-model="imgRowSize" type="number" />
            <button @click="controlCol()">确认</button>
        </div>

        <div
            v-for="(items, index) in colList"
            :key="index"
            class="img-wrap"
            :class="index % 2 == 0 ? 'fdrr' : 'fdr'"
        >
            <i
                v-for="(item, index1) in items && items"
                :key="index1"
                class="img-box"
            >
                <img :src="item && item.img" alt="" />
                <span class="current-img">{{ item && item.id }}</span>
            </i>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            imgTotal: null,
            imgRowSize: null,
            imgWidth: null,
            colList: []
        };
    },
    mounted() {},

    methods: {
        controlTotal() {},

        controlCol() {
            this.colList = [];
            let counter = 1;

            if (!this.imgRowSize) {
                /** 图片总数 */
                const arr = [];
                for (let i = 0; i < this.imgTotal; i++) {
                    arr.push({
                        id: counter++,
                        img: require("../assets/img/cat.png")
                    });
                }

                this.$set(this.colList, [0], arr);

            } else {

                /** 设置行数 */
                let rowNum = Math.ceil(
                    parseInt(this.imgTotal) / parseInt(this.imgRowSize)
                );

                console.log("rowNum:", rowNum);

                for (let i = 0; i < this.imgRowSize; i++) {

                    /** 设置列数 */
                    this.colList.push([]);

                    /** 每列加上行数 */
                    for (let j = 0; j < rowNum; j++) {
                        this.$set(this.colList[i], [j], {
                            id: counter++,
                            img: require("../assets/img/cat.png")
                        });
                    }
                }
            }

            console.log("this.colList:", this.colList);
        }
    }
};
</script>

<style>
.fdr {
    flex-direction: row;
}

.fdrr {
    flex-direction: row-reverse;
}

.img-wrap {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
}

.img-wrap .img-box {
    flex: 1;
    position: relative;
    height: 145px;
    padding: 5px;
}

.current-img {
    position: absolute;
    top: 10px;
    left:10px;
    color: #fff;
}
</style>
