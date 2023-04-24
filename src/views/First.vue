<template>
    <el-container style="border: 1px solid #eee">
        <el-container>
            <el-main>
                <div ref="charts" style="width: 100%; height: 100vh"></div>
            </el-main>
        </el-container>

        <el-dialog title="数据来源" :visible.sync="dialogVisible" width="60%" :before-close="handleClose">
            <div v-for="(item, inds) in linksData.links" :key="inds">{{ `${item.date} - ` }} <el-link type="primary"
                    :href="item.link">{{ item.name }}</el-link> </div>
            <span slot="footer" class="dialog-footer">
                <el-button size="small" type="primary" @click="dialogVisible = false">确 定</el-button>
            </span>
        </el-dialog>
    </el-container>
</template>
<style scoped lang="scss">
$main-color: #f1f5fb;

* {
    font-size: 1.6rem;
}

body>.el-container {
    margin-bottom: 40px;
}

.el-main,
.el-container {
    background-color: $main-color;
}

.el-container {
    overflow-x: auto;
    min-width: 1200px;
    height: 100vh;
}

.el-main {
    background-color: #FFF;
    color: #333;
    text-align: center;
    overflow: visible;
}
</style>
<script>
import usaJson from "@/assets/USA.json"

export default {
    data() {
        return {
            dataSet: {
                resultdata1: [
                    { name: 'Alabama', value: 4822023 },
                    { name: 'Alaska', value: 731449 },
                    { name: 'Arizona', value: 6553255 },
                    { name: 'Arkansas', value: 2949131 },
                    { name: 'California', value: 38041430 },
                    { name: 'Colorado', value: 5187582 },
                    { name: 'Connecticut', value: 3590347 },
                    { name: 'Delaware', value: 917092 },
                    { name: 'District of Columbia', value: 632323 },
                    { name: 'Florida', value: 19317568 },
                    { name: 'Georgia', value: 9919945 },
                    { name: 'Hawaii', value: 1392313 },
                    { name: 'Idaho', value: 1595728 },
                    { name: 'Illinois', value: 12875255 },
                    { name: 'Indiana', value: 6537334 },
                    { name: 'Iowa', value: 3074186 },
                    { name: 'Kansas', value: 2885905 },
                    { name: 'Kentucky', value: 4380415 },
                    { name: 'Louisiana', value: 4601893 },
                    { name: 'Maine', value: 1329192 },
                    { name: 'Maryland', value: 5884563 },
                    { name: 'Massachusetts', value: 6646144 },
                    { name: 'Michigan', value: 9883360 },
                    { name: 'Minnesota', value: 5379139 },
                    { name: 'Mississippi', value: 2984926 },
                    { name: 'Missouri', value: 6021988 },
                    { name: 'Montana', value: 1005141 },
                    { name: 'Nebraska', value: 1855525 },
                    { name: 'Nevada', value: 2758931 },
                    { name: 'New Hampshire', value: 1320718 },
                    { name: 'New Jersey', value: 8864590 },
                    { name: 'New Mexico', value: 2085538 },
                    { name: 'New York', value: 19570261 },
                    { name: 'North Carolina', value: 9752073 },
                    { name: 'North Dakota', value: 699628 },
                    { name: 'Ohio', value: 11544225 },
                    { name: 'Oklahoma', value: 3814820 },
                    { name: 'Oregon', value: 3899353 },
                    { name: 'Pennsylvania', value: 12763536 },
                    { name: 'Rhode Island', value: 1050292 },
                    { name: 'South Carolina', value: 4723723 },
                    { name: 'South Dakota', value: 833354 },
                    { name: 'Tennessee', value: 6456243 },
                    { name: 'Texas', value: 29059203 },
                    { name: 'Utah', value: 2855287 },
                    { name: 'Vermont', value: 626011 },
                    { name: 'Virginia', value: 8185867 },
                    { name: 'Washington', value: 6897012 },
                    { name: 'West Virginia', value: 1855413 },
                    { name: 'Wisconsin', value: 5726398 },
                    { name: 'Wyoming', value: 576412 },
                    { name: 'Puerto Rico', value: 3667084 }
                ],
                resultdata2: [
                    { name: 'Alabama', value: 4822023 },
                    { name: 'Alaska', value: 731449 },
                    { name: 'Arizona', value: 6553255 },
                    { name: 'Arkansas', value: 2949131 },
                    { name: 'California', value: 38041430 },
                    { name: 'Colorado', value: 5187582 },
                    { name: 'Connecticut', value: 3590347 },
                    { name: 'Delaware', value: 917092 },
                    { name: 'District of Columbia', value: 632323 },
                    { name: 'Florida', value: 19317568 },
                    { name: 'Georgia', value: 9919945 },
                    { name: 'Hawaii', value: 1392313 },
                    { name: 'Idaho', value: 1595728 },
                    { name: 'Illinois', value: 12875255 },
                    { name: 'Indiana', value: 6537334 },
                    { name: 'Iowa', value: 3074186 },
                    { name: 'Kansas', value: 2885905 },
                    { name: 'Kentucky', value: 4380415 },
                    { name: 'Louisiana', value: 4601893 },
                    { name: 'Maine', value: 1329192 },
                    { name: 'Maryland', value: 5884563 },
                    { name: 'Massachusetts', value: 6646144 },
                    { name: 'Michigan', value: 9883360 },
                    { name: 'Minnesota', value: 5379139 },
                    { name: 'Mississippi', value: 2984926 },
                    { name: 'Missouri', value: 6021988 },
                    { name: 'Montana', value: 1005141 },
                    { name: 'Nebraska', value: 1855525 },
                    { name: 'Nevada', value: 2758931 },
                    { name: 'New Hampshire', value: 1320718 },
                    { name: 'New Jersey', value: 8864590 },
                    { name: 'New Mexico', value: 2085538 },
                    { name: 'New York', value: 19570261 },
                    { name: 'North Carolina', value: 9752073 },
                    { name: 'North Dakota', value: 699628 },
                    { name: 'Ohio', value: 11544225 },
                    { name: 'Oklahoma', value: 3814820 },
                    { name: 'Oregon', value: 3899353 },
                    { name: 'Pennsylvania', value: 12763536 },
                    { name: 'Rhode Island', value: 1050292 },
                    { name: 'South Carolina', value: 4723723 },
                    { name: 'South Dakota', value: 833354 },
                    { name: 'Tennessee', value: 6456243 },
                    { name: 'Texas', value: 26059203 },
                    { name: 'Utah', value: 2855287 },
                    { name: 'Vermont', value: 626011 },
                    { name: 'Virginia', value: 8185867 },
                    { name: 'Washington', value: 6897012 },
                    { name: 'West Virginia', value: 1855413 },
                    { name: 'Wisconsin', value: 5726398 },
                    { name: 'Wyoming', value: 576412 },
                    { name: 'Puerto Rico', value: 3667084 }
                ]
            },
            linksData: {},
            dialogVisible: false
        }
    },
    methods: {
        initCharts() {
            const myCharts = this.$echarts.init(this.$refs["charts"]);
            const { resultdata1, resultdata2 } = this.dataSet
            resultdata1.forEach(item => {
                item.links = [{
                    date: '16 四月 2023',
                    name: '沙门氏菌爆发',
                    link: 'http://www.baidu.com'
                }, {
                    date: '16 五月 2023',
                    name: '加拿大人结核病最新数据',
                    link: 'http://www.baidu.com'
                }]
            })
            resultdata2.forEach(item => {
                item.links = [{
                    date: '6 四月 2023',
                    name: '北哦额俄方人反而分个额',
                    link: 'http://www.google.com'
                }, {
                    date: '10 五月 2023',
                    name: '人发工人过开放日荣光科技发热过诶肌肤诶分额佛额佛俄方饿哦分佛俄方',
                    link: 'http://www.google.com'
                },]
            })
            const option = {
                title: [{
                    text: '美国社交媒体/新闻疫情统计数据',
                    sublink: 'http://www.census.gov/popest/data/datasets.html',
                    left: 'left',
                    textStyle:{
                        fontSize: 30
                    }
                }
                    // ,{
                    //     text: '美国新闻疫情统计数据',
                    //     sublink: 'http://www.census.gov/popest/data/datasets.html',
                    //     left: 'right'
                    // }
                ],
                legend: {
                    data: ['美国社交媒体疫情统计数据', '美国新闻疫情统计数据'],
                    top: '5%',
                    left: '40%',
                    selectedMode: 'single',
                    selected: {
                        // 选中'系列1'
                        '美国社交媒体疫情统计数据': true,
                        // 不选中'系列2'
                        '美国新闻疫情统计数据': false
                    },
                    textStyle: {
                        fontSize: '22'
                    }
                },
                tooltip: {
                    trigger: 'item',
                    showDelay: 0,
                    transitionDuration: 0.2
                },
                visualMap: {
                    right: '8%',
                    bottom: '10%',
                    min: 500000,
                    max: 38000000,
                    inRange: {
                        color: [
                            '#313695',
                            '#4575b4',
                            '#74add1',
                            '#abd9e9',
                            '#e0f3f8',
                            '#ffffbf',
                            '#fee090',
                            '#fdae61',
                            '#f46d43',
                            '#d73027',
                            '#a50026'
                        ]
                    },
                    text: ['High', 'Low'],
                    calculable: true
                },
                series: [
                    {
                        name: '美国社交媒体疫情统计数据',
                        type: 'map',
                        roam: true,
                        top: 'middle',
                        scaleLimit: {
                            min: 1,
                            max: 2.6
                        },
                        map: 'USA',
                        label: {
                            normal: {
                                show: true,
                            },
                            emphasis: {
                                show: true,
                            },
                        },
                        emphasis: {
                            label: {
                                show: true
                            }
                        },
                        data: resultdata1
                    },
                    {
                        name: '美国新闻疫情统计数据',
                        type: 'map',
                        roam: true,
                        top: 'middle',
                        scaleLimit: {
                            min: 1,
                            max: 2.6
                        },
                        map: 'USA',
                        label: {
                            normal: {
                                show: true,
                            },
                            emphasis: {
                                show: true,
                            },
                        },
                        emphasis: {
                            label: {
                                show: true
                            }
                        },
                        data: resultdata2
                    }
                ]
            };

            console.log('ass', typeof usaJson)
            usaJson.features.forEach(item => {
                item.properties.name = item.properties.name_full
            })
            // 地图注册，第一个参数的名字必须和option.geo.map一致
            this.$echarts.registerMap('USA', usaJson, {
                Alaska: {
                    left: -131,
                    top: 25,
                    width: 15
                },
                Hawaii: {
                    left: -110,
                    top: 28,
                    width: 5
                },
                'Puerto Rico': {
                    left: -76,
                    top: 26,
                    width: 2
                }
            });

            myCharts.setOption(option);
            myCharts.on("click", params => { //点击事件
                console.log('我被点击了', params)
                this.clickItem(params)
            });
        },
        //点击每个州的事件
        clickItem(params) {
            this.linksData = params.data
            this.dialogVisible = true
        },
        handleClose() {
            this.dialogVisible = false
        }
    },
    mounted() {
        this.initCharts();
    }
}
</script>
  