







<script setup>
    import axios from 'axios'
    import { ssrExportAllKey } from 'vite/runtime';
    // 发起 GET 请求
    function login() {
        axios({
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            },
            method: 'post',
            url: "https://192.168.1.153/api/Users/Login",
            data: { ModiePone: "13888881001", Password: "8888" }
        })
            .then(response => {
                // 请求成功处理
                console.log(response.data);
            })
            .catch(error => {
                // 请求失败处理
                console.error(error);
            });
    }

    function submit() {
        axios({
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            },
            method: 'post',
            url: "https://192.168.1.153/api/Users/Login",
            data: { ModiePone: "13888881001", Password: "8888" }
        })
            .then(response => {
                // 请求成功处理
                console.log(response.data);
            })
            .catch(error => {
                // 请求失败处理
                console.error(error);
            });
    }

    function getlist() {
        axios({
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            },
            method: 'get',
            url: "https://192.168.1.153/api/Users/GetUsersList",
            data: { ModiePone: "13888881001", Password: "8888" }
        })
            .then(response => {
                // 请求成功处理
                console.log(response.data);
            })
            .catch(error => {
                // 请求失败处理
                console.error(error);
            });
    }


    layui.use(function () {
        var table = layui.table;
        // 渲染，并获得实例对象
        var inst = table.render({
            elem: '#myuserslist', // 绑定元素选择器
            url: "https://192.168.1.153/api/Users/GetUsersList",
            cols: [[ // 重置表头
                { type: 'checkbox', fixed: 'left' },
                { field: 'id', title: 'ID', width: 80, fixed: 'left', unresize: true, sort: true, totalRowText: '合计：' },
                { field: 'sex', title: '性别', width: 80, edit: 'text', sort: true },
                { field: 'modiePone', title: 'shouji', width: 80, sort: true, totalRow: true },
                { field: 'userName', title: 'username', width: 100, sort: true, totalRow: true },
                { field: 'carteTime', title: '加入时间', width: 120 },
                { fixed: 'right', title: '操作', width: 134, minWidth: 125, toolbar: '#barDemo' }
            ]]
        });
        // 实例对象成员
        inst.config; // 当前表格配置属性
        //inst.reload(options, deep); // 对当前表格的完整重载。参数 deep 表示是否深度重载。
        //inst.reloadData(options, deep); // 对当前表格的数据重载。参数 deep 同上。
        inst.resize(); // 对当前表格重新适配尺寸
        inst.setColsWidth() // 对当前表格重新分配列宽


        // 触发单元格工具事件
        table.on('tool(test)', function (obj) { // 双击 toolDouble
            var data = obj.data; // 获得当前行数据
            // console.log(obj)
            if (obj.event === 'edit') {
                layer.open({
                    title: '编辑 -id:bvbnbn' + data.modiePone,
                    type: 1,
                    area: ['80%', '80%'],
                    content: '<div style="padding: 16px;">自定义表单元素</div>'
                });
            }
            else if (obj.event === 'more') {
                // 更多 - 下拉菜单
                dropdown.render({
                    elem: this, // 触发事件的 DOM 对象
                    show: true, // 外部事件触发即显示
                    data: [{
                        title: '查看',
                        id: 'detail'
                    }, {
                        title: '删除',
                        id: 'del'
                    }],
                    click: function (menudata) {
                        if (menudata.sex === 'detail') {
                            layer.msg('查看操作，当前行 ID:' + data.sex);
                        } else if (menudata.sex === 'del') {
                            layer.confirm('真的删除行 [id: ' + data.sex + '] 么', function (index) {
                                obj.del(); // 删除对应行（tr）的DOM结构
                                layer.close(index);
                                // 向服务端发送删除指令
                            });
                        }
                    },
                    align: 'right', // 右对齐弹出
                    style: 'box-shadow: 1px 1px 10px rgb(0 0 0 / 12%);' // 设置额外样式
                })
            }
        });

        //// 触发表格复选框选择
        //table.on('checkbox(test)', function (obj) {
        //    console.log(obj)
        //});

        //// 触发表格单选框选择
        //table.on('radio(test)', function (obj) {
        //    console.log(obj)
        //});

        //// 行单击事件
        //table.on('row(test)', function (obj) {
        //    //console.log(obj);
        //    //layer.closeAll('tips');
        //});
        //// 行双击事件
        //table.on('rowDouble(test)', function (obj) {
        //    console.log(obj);
        //});

        //// 单元格编辑事件
        //table.on('edit(test)', function (obj) {
        //    var field = obj.field; // 得到字段
        //    var value = obj.value; // 得到修改后的值
        //    var data = obj.data; // 得到所在行所有键值
        //    // 值的校验
        //    if (field === 'email') {
        //        if (!/^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/.test(obj.value)) {
        //            layer.tips('输入的邮箱格式不正确，请重新编辑', this, { tips: 1 });
        //            return obj.reedit(); // 重新编辑 -- v2.8.0 新增
        //        }
        //    }
        //    // 编辑后续操作，如提交更新请求，以完成真实的数据更新
        //    // …
        //    layer.msg('编辑成功', { icon: 1 });

        //    // 其他更新操作
        //    var update = {};
        //    update[field] = value;
        //    obj.update(update);
        //});




    });

</script>

<template>
    <main>
  
        <div class="wrapper">

            <input value="登录" type="button" @click="login" />
            <form action="https://192.168.1.153/api/Users/Login" method="post">

                <div class="phone">
                    <!-- 文本输入框 -->
                    <label for="name">手机号:</label>
                    <input type="text" id="name" name="ModiePone" required>
                    <br>
                </div>

                <div class="phone">
                    <!-- 密码输入框 -->
                    <label for="password">密&emsp;码:</label>
                    <input type="password" id="password" name="Password" required>
                    <br>
                </div>
                <!-- 提交按钮 -->
                <div class="haha">
                    <input type="submit" value="提交" class="erzi">  <input value="登录" type="button" @click="login" />
                </div>
            </form>

            <input value="getlist" type="button" @click="getlist" />

            <div id="myuserslist">

            </div>


        </div>
    </main>
</template>

<script>
    export default {

    }
</script>

<style scoped>
    .erzi {
        margin-right: 100px;
        background-color: red;
    }




    .haha {
        display: flex;
        justify-content: center;
        background-color: blue;
    }

    .phone {
        padding: 5px;
    }


    header {
        line-height: 1.5;
    }

    .logo {
        display: block;
        margin: 0 auto 2rem;
    }

    @media (min-width: 1024px) {
        header {
            display: flex;
            place-items: center;
        }

        .logo {
            margin: 0 2rem 0 0;
        }

        header .wrapper {
            display: flex;
            place-items: flex-start;
            flex-wrap: wrap;
        }
    }
</style>
