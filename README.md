<!doctype html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>大数据</title>
	<link rel="stylesheet" href="css/css.css">
	<script type="text/javascript" src="http://echarts.baidu.com/gallery/vendors/echarts/echarts-all-3.js"></script>
	<!--<script type="text/javascript" src="http://echarts.baidu.com/gallery/vendors/echarts/extension/dataTool.min.js"></script>
	<script type="text/javascript" src="http://echarts.baidu.com/gallery/vendors/echarts/map/js/china.js"></script> -->
	<!--<script type="text/javascript" src="http://echarts.baidu.com/gallery/vendors/echarts/map/js/world.js"></script>
	<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=ZUONbpqGBsYGXNIYHicvbAbM"></script> 
	<script type="text/javascript" src="http://echarts.baidu.com/gallery/vendors/echarts/extension/bmap.min.js"></script> -->
</head>
<body>
	<div class="content">
		<div class="top">大数据</div>
		<div class="banner">
			<div id="top-goods"></div>
			<div id="top-car"></div>
			<div id="top-cars"></div>
			<div id="car-trade"></div>
			<div id="provice"></div>
			<div id="haha"></div>
		</div>
		
	</div>
</body>
<?php
include("conn.php");
$query = sqlsrv_query($conn, "select * from ecs_cart where rec_id = '2'");  
while($row = sqlsrv_fetch_array($query))  
{  
	// $row=json_encode($row);
	// echo "<pre>";
	// print_r($row);
	// echo "</pre>";
 //    $lf = $row['user_id'];
 //    $ty = $row['session_id'];
 //    $gd = $row['goods_id'];
 //    $sj = $row['goods_name'];
 //    $qtsj = $row['market_price'];
 //    $lmsj = $row['is_gift'];
 //    $drfh = $row['parent_id'];
 //    $qtfh = $row['is_gift'];
 //    $lmfh = $row['goods_attr_id'];
} 	
$arr = array(
		"name"=>"100",
		"sex"=>"200",
		"app"=>"300"
	);
foreach ($arr as $key => $value) {
	@$data_name .= "'".$key."',";
	// echo $key."=>".$value."\n";
	@ $data_num .= "{value:".$value.", name:'".$key."'},";
}
// echo "<pre>";
// print_r($data_type);
// echo "</pre>";
?>
<script type="text/javascript">
	var dom = document.getElementById("top-goods");
	var myChart = echarts.init(dom);
	var app = {};
	option = null;
	option = {
	    title : {
	        text: '司机总人数',
	        x: 'center'
	    },
	    tooltip: {
	        trigger: 'item',
	        formatter: "{a} <br/>{b} : {c} ({d}%)"
	    },
	    legend: {
	        orient: 'vertical',
	        left: 'left',
	        data: ['本部司机人数','联盟司机人数','其他司机人数']
	    },
	    series : [
	        {
	            name: '访问来源',
	            type: 'pie',
	            radius : '55%',
	            center: ['50%', '60%'],
	            data:[
	                {value:20, name:'本部司机人数'},
	                {value:30, name:'联盟司机人数'},
	                {value:40, name:'其他司机人数'}
	                
	            ],
	            itemStyle: {
	                emphasis: {
	                    shadowBlur: 10,
	                    shadowOffsetX: 0,
	                    shadowColor: 'rgba(0, 0, 0, 0.5)'
	                }
	            }
	        }
	    ]
	};

	app.currentIndex = -1;

	app.timeTicket = setInterval(function () {
	    var dataLen = option.series[0].data.length;
	    // 取消之前高亮的图形
	    myChart.dispatchAction({
	        type: 'downplay',
	        seriesIndex: 0,
	        dataIndex: app.currentIndex
	    });
	    app.currentIndex = (app.currentIndex + 1) % dataLen;
	    // 高亮当前图形
	    myChart.dispatchAction({
	        type: 'highlight',
	        seriesIndex: 0,
	        dataIndex: app.currentIndex
	    });
	    // 显示 tooltip
	    myChart.dispatchAction({
	        type: 'showTip',
	        seriesIndex: 0,
	        dataIndex: app.currentIndex
	    });
	}, 1000);
	;
	if (option && typeof option === "object") {
	    myChart.setOption(option, true);
	}
	//货物图
	var dom1 = document.getElementById("top-car");
	var myChart1 = echarts.init(dom1);
	var app1 = {};
	option = null;
	option = {
	    title : {
	        text: '发货总数',
	        x: 'center'
	    },
	    tooltip: {
	        trigger: 'item',
	        formatter: "{a} <br/>{b} : {c} ({d}%)"
	    },
	    legend: {
	        orient: 'vertical',
	        left: 'left',
	        data: ['单日发货数','联盟单日发货数','其他发货数']
	    },
	    series : [
	        {
	            name: '访问来源',
	            type: 'pie',
	            radius : '55%',
	            center: ['50%', '60%'],
	            data:[
	                {value:60, name:'单日发货数'},
	                {value:80, name:'联盟单日发货数'},
	                {value:90, name:'其他发货数'}
	                
	            ],
	            itemStyle: {
	                emphasis: {
	                    shadowBlur: 10,
	                    shadowOffsetX: 0,
	                    shadowColor: 'rgba(0, 0, 0, 0.5)'
	                }
	            }
	        }
	    ]
	};

	app1.currentIndex = -1;

	app1.timeTicket = setInterval(function () {
	    var dataLen = option.series[0].data.length;
	    // 取消之前高亮的图形
	    myChart1.dispatchAction({
	        type: 'downplay',
	        seriesIndex: 0,
	        dataIndex: app1.currentIndex
	    });
	    app1.currentIndex = (app1.currentIndex + 1) % dataLen;
	    // 高亮当前图形
	    myChart1.dispatchAction({
	        type: 'highlight',
	        seriesIndex: 0,
	        dataIndex: app1.currentIndex
	    });
	    // 显示 tooltip
	    myChart1.dispatchAction({
	        type: 'showTip',
	        seriesIndex: 0,
	        dataIndex: app1.currentIndex
	    });
	}, 1000);
	;
	if (option && typeof option === "object") {
	    myChart1.setOption(option, true);
	}
	//车辆数
	var dom2 = document.getElementById("top-cars");
	var myChart2 = echarts.init(dom2);
	var app2 = {};
	option = null;
	option = {
	    title : {
	        text: '车辆总数',
	        x: 'center'
	    },
	    tooltip: {
	        trigger: 'item',
	        formatter: "{a} <br/>{b} : {c} ({d}%)"
	    },
	    legend: {
	        orient: 'vertical',
	        left: 'left',
	        data: ['本部车辆数','联盟车辆数','其他车辆数']
	    },
	    series : [
	        {
	            name: '访问来源',
	            type: 'pie',
	            radius : '55%',
	            center: ['50%', '60%'],
	            data:[
	                {value:200, name:'本部车辆数'},
	                {value:310, name:'联盟车辆数'},
	                {value:234, name:'其他车辆数'}
	                
	            ],
	            itemStyle: {
	                emphasis: {
	                    shadowBlur: 10,
	                    shadowOffsetX: 0,
	                    shadowColor: 'rgba(0, 0, 0, 0.5)'
	                }
	            }
	        }
	    ]
	};

	app2.currentIndex = -1;

	app2.timeTicket = setInterval(function () {
	    var dataLen = option.series[0].data.length;
	    // 取消之前高亮的图形
	    myChart2.dispatchAction({
	        type: 'downplay',
	        seriesIndex: 0,
	        dataIndex: app2.currentIndex
	    });
	    app2.currentIndex = (app2.currentIndex + 1) % dataLen;
	    // 高亮当前图形
	    myChart2.dispatchAction({
	        type: 'highlight',
	        seriesIndex: 0,
	        dataIndex: app2.currentIndex
	    });
	    // 显示 tooltip
	    myChart2.dispatchAction({
	        type: 'showTip',
	        seriesIndex: 0,
	        dataIndex: app2.currentIndex
	    });
	}, 1000);
	;
	if (option && typeof option === "object") {
	    myChart2.setOption(option, true);
	}
	//车辆成交量
	var dom3 = document.getElementById("car-trade");
	var myChart3 = echarts.init(dom3);
	var app3 = {};
	option = null;
	option = {
	    title : {
	        text: '车辆成交量',
	        x: 'center'
	    },
	    tooltip: {
	        trigger: 'item',
	        formatter: "{a} <br/>{b} : {c} ({d}%)"
	    },
	    legend: {
	        orient: 'vertical',
	        left: 'left',
	        data: ['本部车辆成交量','联盟车辆成交量','其他车辆成交量']
	    },
	    series : [
	        {
	            name: '访问来源',
	            type: 'pie',
	            radius : '55%',
	            center: ['50%', '60%'],
	            data:[
	                {value:200, name:'本部车辆成交量'},
	                {value:310, name:'联盟车辆成交量'},
	                {value:234, name:'其他车辆成交量'}
	                
	            ],
	            itemStyle: {
	                emphasis: {
	                    shadowBlur: 10,
	                    shadowOffsetX: 0,
	                    shadowColor: 'rgba(0, 0, 0, 0.5)'
	                }
	            }
	        }
	    ]
	};

	app3.currentIndex = -1;

	app3.timeTicket = setInterval(function () {
	    var dataLen = option.series[0].data.length;
	    // 取消之前高亮的图形
	    myChart3.dispatchAction({
	        type: 'downplay',
	        seriesIndex: 0,
	        dataIndex: app3.currentIndex
	    });
	    app3.currentIndex = (app3.currentIndex + 1) % dataLen;
	    // 高亮当前图形
	    myChart3.dispatchAction({
	        type: 'highlight',
	        seriesIndex: 0,
	        dataIndex: app3.currentIndex
	    });
	    // 显示 tooltip
	    myChart3.dispatchAction({
	        type: 'showTip',
	        seriesIndex: 0,
	        dataIndex: app3.currentIndex
	    });
	}, 1000);
	;
	if (option && typeof option === "object") {
	    myChart3.setOption(option, true);
	}

	//省份
	var dom4 = document.getElementById("provice");
	var myChart4 = echarts.init(dom4);
	var app4 = {};
	option = null;

	function fetchData(cb) {
	    // 通过 setTimeout 模拟异步加载
	    setTimeout(function () {
	        cb({
	            categories: [<?php echo $data_name;?>],
	            data: [<?php echo $data_num;?>]
	        });
	    }, 3000);
	}



	option = {
	    title: {
	        text: '各地发货量'
	    },
	    tooltip: {},
	    legend: {
	        data:['发货量']
	    },
	    xAxis: {
	        data: []
	    },
	    yAxis: {},
	    series: [{
	        name: '发货量',
	        type: 'bar',
	        data: []
	    }]
	};;
	

	myChart4.showLoading();

	fetchData(function (data) {
	    myChart4.hideLoading();
	    myChart4.setOption({
	        xAxis: {
	            data: data.categories
	        },
	        series: [{
	            // 根据名字对应到相应的系列
	            name: '销量',
	            data: data.data
	        }]
	    });
	});;



	if (option && typeof option === "object") {
	    myChart4.setOption(option, true);
	}
	//折线图
	var dom5 = document.getElementById("haha");
	var myChart5 = echarts.init(dom5);
	var app5 = {};
	option = null;
	option = {
    title: {
        text: '折线图堆叠'
    },
    tooltip: {
        trigger: 'axis'
    },
    legend: {
        data:['邮件营销','联盟广告','视频广告','直接访问','搜索引擎']
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    toolbox: {
        feature: {
            saveAsImage: {}
        }
    },
    xAxis: {
        type: 'category',
        boundaryGap: false,
        data: ['周一','周二','周三','周四','周五','周六','周日']
    },
    yAxis: {
        type: 'value'
    },
    series: [
        {
            name:'邮件营销',
            type:'line',
            stack: '总量',
            data:[120, 132, 101, 134, 90, 230, 210]
        },
        {
            name:'联盟广告',
            type:'line',
            stack: '总量',
            data:[220, 182, 191, 234, 290, 330, 310]
        },
        {
            name:'视频广告',
            type:'line',
            stack: '总量',
            data:[150, 232, 201, 154, 190, 330, 410]
        },
        {
            name:'直接访问',
            type:'line',
            stack: '总量',
            data:[320, 332, 301, 334, 390, 330, 320]
        },
        {
            name:'搜索引擎',
            type:'line',
            stack: '总量',
            data:[820, 932, 901, 934, 1290, 1330, 1320]
        }
    ]
};
if (option && typeof option === "object") {
	    myChart5.setOption(option, true);
	}
</script>
</html>
