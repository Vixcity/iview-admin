<template>
  <div class="treated">
    <div class="flex">
      <div class="filterCtn flex aic">
        <div class="label">患者</div>
        <div class="searchCtn">
          <Select v-model="hz">
            <Option v-for="item in hzList" :value="item.value" :key="item.value">
              {{ item.label }}
            </Option>
          </Select>
        </div>
      </div>
      <div class="filterCtn flex aic">
        <div class="label">就诊类型</div>
        <div class="searchCtn">
          <Select v-model="jzlx" placeholder="请选择就诊类型">
            <Option v-for="item in jzlxList" :value="item.value" :key="item.value">
              {{ item.label }}
            </Option>
          </Select>
        </div>
      </div>
      <div class="filterCtn flex aic">
        <div class="label">就诊时间</div>
        <div class="searchCtn" style="width: 190px">
          <DatePicker
            type="daterange"
            v-model="chooseDate"
            :options="dateList"
            placement="bottom-end"
            placeholder="请选择就诊时间"
          ></DatePicker>
        </div>
      </div>
      <div class="filterCtn flex aic">
        <div class="label">搜索</div>
        <div class="searchCtn" style="width: 230px">
          <Input v-model="searchText" placeholder="请输入患者姓名/手机" icon="ios-search"></Input>
        </div>
      </div>
      <Button type="primary">查 询</Button>
    </div>
    <Table :columns="columns" :data="data" style="margin-top: 16px">
      <template #action="{ row, index }">
        <Button type="primary" size="small" style="margin-right: 5px" @click="show(index)">
          {{row.name}}
        </Button>
        <Button type="error" size="small" @click="remove(index)">Delete</Button>
      </template>
    </Table>
  </div>
</template>

<script>
export default {
  name: 'treated',
  data () {
    return {
      hzList: [
        {
          value: '全部患者',
          label: '全部患者'
        },
        {
          value: '待接诊患者',
          label: '待接诊患者'
        },
        {
          value: '接诊中患者',
          label: '接诊中患者'
        },
        {
          value: '已完成患者',
          label: '已完成患者'
        },
        {
          value: '已取消患者',
          label: '已取消患者'
        }
      ],
      hz: '全部患者',
      jzlxList: [
        {
          value: '全部',
          label: '全部'
        },
        {
          value: '复诊',
          label: '复诊'
        },
        {
          value: '出诊',
          label: '出诊'
        }
      ],
      jzlx: '全部',
      dateList: {
        shortcuts: [
          {
            text: '今天',
            value: () => {
              const start = this.$moment().startOf('day')._d
              return [start, start]
            }
          },
          {
            text: '本周',
            value: () => {
              const start = this.$moment().startOf('week').add(1, 'day')._d
              const end = this.$moment().endOf('week').add(1, 'day')._d
              return [start, end]
            }
          },
          {
            text: '本月',
            value: () => {
              const start = this.$moment().startOf('month')._d
              const end = this.$moment().endOf('month')._d
              return [start, end]
            }
          },
          {
            text: '今年',
            value () {
              const start = new Date().getFullYear() + '01-01'
              const end = new Date().getFullYear() + '12-31'
              return [start, end]
            }
          }
        ]
      },
      chooseDate: [
        this.$moment().startOf('day').format('YYYY-MM-DD'),
        this.$moment().startOf('day').format('YYYY-MM-DD')
      ],
      searchText: '',
      columns: [
        {
          title: '病案号',
          key: 'bah'
        },
        {
          title: '姓名',
          key: 'name'
        },
        {
          title: '年龄',
          key: 'age'
        },
        {
          title: '性别',
          key: 'sex'
        },
        {
          title: '就诊类型',
          key: 'type'
        },
        {
          title: '就诊时间',
          key: 'jzsj'
        },
        {
          title: '预约时间',
          key: 'yysj'
        },
        {
          title: '就诊医生',
          key: 'jzys'
        },
        {
          title: '状态',
          key: 'status'
        },
        {
          title: '操作',
          key: 'do',
          slot: 'action',
          width: 180
        }
      ],
      data: [
        {
          bah: '1',
          name: 'John Brown',
          age: 18,
          address: 'New York No. 1 Lake Park',
          date: '2016-10-03',
          sex: '男',
          type: '类型1',
          jzsj: '2022-04-04',
          yysj: '2022-04-05',
          jzys: '张医生',
          status: '良好'
        },
        {
          bah: '2',
          name: 'Jim Green',
          age: 24,
          address: 'London No. 1 Lake Park',
          date: '2016-10-01',
          sex: '男',
          type: '类型2',
          jzsj: '2022-04-04',
          yysj: '2022-04-05',
          jzys: '张医生',
          status: '良好'
        },
        {
          bah: '3',
          name: 'Joe Black',
          age: 30,
          address: 'Sydney No. 1 Lake Park',
          date: '2016-10-02',
          sex: '女',
          type: '类型3',
          jzsj: '2022-04-04',
          yysj: '2022-04-05',
          jzys: '张医生',
          status: '良好'
        },
        {
          bah: '4',
          name: 'Jon Snow',
          age: 26,
          address: 'Ottawa No. 2 Lake Park',
          date: '2016-10-04',
          sex: '男',
          type: '类型4',
          jzsj: '2022-04-04',
          yysj: '2022-04-05',
          jzys: '张医生',
          status: '良好'
        }
      ]
    }
  },
  methods: {},
  mounted () {}
}
</script>

<style lang="less">
@import './treated.less';
</style>
<style scoped>
.treated >>> .ivu-table th {
  color: #282d3c;
  font-size: 14px;
  font-weight: normal;
  background: rgba(49, 113, 255, 0.2);
}

.treated >>> .ivu-table-row {
  color: #282d3c;
  font-size: 14px;
  font-weight: normal;
}

.treated >>> .ivu-table-wrapper {
  border: 0;
}

.treated >>> .ivu-table:after {
  width: 0;
}
</style>
