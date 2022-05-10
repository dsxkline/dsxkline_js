# 大师兄K线图
纯JS(ES5)语言进行开发，几乎完美适配所有浏览器平台(ie678除外)，移动端电脑端混合开发媲美原生体验！
## 官方网站
http://www.dsxkline.com

## 开始
    <script src="http://www.dsxkline.com/dsx.kline.js></script>
#### 创建K线图
    <div id="kline"></div>
    var c=document.getElementById("kline"); 
    var kline = new dsxKline({
        element:c,
        onLoading:function(o){
            // 开始请求加载数据
        },
        nextPage:function(data,index){
            // 开始请求加载下一页数据
        },
        onCrossing:function(data,index){
            // 十字线移动数据
        },
        updateComplate:function(){
            // 完成K线一次更新
        }
    });
#### 更新K线图
    kline.update({
        chartType:dsxConfig.chartType.timeSharing,
        //theme:"dark",
        candleType:dsxConfig.candleType.hollow,
        zoomLockType:dsxConfig.zoomLockType.right,
        isShowKlineTipPannel:false,
        sides:kline.chartType<=1?["VOL"]:["VOL","MACD"],
        datas:data,
    });
    kline.finishLoading();
#### 刷新最新数据
    // 周期 cycle=t,d,w,m,y,m1,t5 分别代表 分时,日K,周K,年K,1分钟,五日
    // data为最后一根K线数据，数据结构 分时图=[日期,时间,价格,成交量,成交额] K线图=[日期,开,高,低,收,成交量,成交额] 分钟K线=[日期,时间,开,高,低,收,成交量,成交额]
    kline.refreshLastOneData(data,cycle);

## 属性
|属性|名称|类型|必需|默认值|备注|
|----|----|----|----|----|----|
|theme	|主题	|string|	否	|white|	white,dark|
|chartType	|图标类型|	int|	否	|0	|分时图=0，五日=1，k线图=2|
|market|	交易所	|string	|否	|sh|	sh,sz,bj,hk,us|
|candleType|	蜡烛图类型|	int	|否	|0	|空心=0 实心=1|
|dpr	|屏幕dpr	|float|否	|2	|自动适配|
|element|	画布对象|	dom|	是	|	|
|width|	宽度|	float	|否	|画布宽度|	默认跟element适配|
|height|	高度	|float	|否	|画布高度|	默认跟element适配|
|paddingTop	|顶部间距	|float|	否|	20	||
|paddingMiddle|	主副图间距	|float	|否	|20	||
|paddingBottom	|底部间距	|float	|否	|1	||
|autoSize	|自动大小	|boolean	|否	|false	|为true根据element自动适应|
|datas	|数据	|int	|否|	null	|查看数据规范|
|lastClose|	昨收	|int|	否	|null	|当前股票昨日收盘价|
|mobileCross	|十字线移动端接管	|boolean|	否	|false|	需要移动端实现十字线时启用|
|onCrossing	|滑动十字线回调	|function	|否	|0	|返回十字线当前数据|
|zoomstep	|缩放步长|	float|否	|0.5	|每次缩放多少像素|
|zoomMin	|缩小最小值	|float	|否	|3	||
|zoomMax|	放大最大值	|float|	否	|50	||
|zoomLockType	|缩放类型|	int	|否|	2	|1=左，2=中，3=右，4=跟随鼠标|
|mobileZoom	|缩放手势移动端接管	|boolean|	否	|false	|移动端实现缩放时启用|
|sides|	副图指标	|array|	否	|["MA"]	|支持指标 MA,BOLL|
|main	|主图指标	|array|	否|	["VOL"]	|支持指标 VOL,MACD,KDJ,RSI|
|sideHeight	|副图高度	|float	|否	|height*20%	|默认为高度的20%|
|mainHeight|	主图高度	|float	|否		||
|debug	|debug模式	|boolean|	否	|false	||
|nextPage	|加载下一页|	function|	否	|0	|滚动到最左边的时候加载下一页数据|
|rightEmptyKlineAmount	|右边空数据	|int|	否	|0	|默认图表右边空出多少根K线|
|onLoading	|开始加载回调	|function	|否	|0	|初始化加载数据，首次请求数据需要定义在此|
|updateComplate	|更新完成回调	|function|	否	|0	|图表完成一次更新结束|
|timePeriod	|交易时间段|	string	|否	|9:30-11:30,13:00-15:00	|为空启用系统内置|
|isShowKlineTipPannel	|显示内置K线提示面板	|boolean	|否	|true	|自主实现K线数据提示请关闭|
|page	|页码	|int	|否	|1	|加载下一页数据时需要传入页码|
|theend	|滚动到尽头	|boolean	|否	|false	|下一页没有数据需要标志为true|

## 配置 dsxConfig
#### k线图表类型
    // k线图表类型
    dsxConfig.chartType = {
        timeSharing:0,  // 分时图
        timeSharing5:1, // 五日分时图
        candle:2,       // K线图
    }
