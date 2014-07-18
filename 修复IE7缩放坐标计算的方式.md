IE7实际坐标 = 获取坐标 / 缩放比例

获取缩放级别代码

    function GetZoomFactor() {
        var factor = 1;
        if (document.body.getBoundingClientRect) {
            var rect = document.body.getBoundingClientRect();
            var physicalW = rect.right - rect.left;
            var logicalW = document.body.offsetWidth;
            factor = Math.round((physicalW / logicalW) * 100) / 100;
        }
        return factor;
    }