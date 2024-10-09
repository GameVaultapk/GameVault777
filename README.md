
<html>

<head id="Head1">
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
    <meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
    <title>Game Vault</title>
    <link rel="shortcut icon" href="#" />
    <script src="https://juwadownload.oss-us-west-1.aliyuncs.com/js/js/jquery-1.11.3.js"></script>
    <script type="text/javascript" src="https://download.gamevault999.com/js/browser.js?v=1.370"></script>
    <link rel="stylesheet" href="https://download.gamevault999.com/css/style.css">
    <script type="text/javascript">
        //IOS下载地址
        //var IOS_DownLoad_URL = "https://OtSwcb.391714.com/2IlO3";
        //var IOS_DownLoad_URL = "itms-services://?action=download-manifest&url=https://galaxyworlddown.oss-us-west-1.aliyuncs.com/ios/GameVault.plist";
        var IOS_DownLoad_URL  = "https://gogo.ctqwrdbac.com/5rnwgw"
        //安卓下载地址
        var AZ_DownLoad_URL = "https://download.gamevault999.com/download/GameVault.apk";
    </script>
</head>

<body>
  <div class="download" id="box1" @touchmove.prevent>
    <div class="box1">
      <img id="background_1" src="https://download.gamevault999.com/images/background.jpg" alt="" class="box-img">
    </div>
    <div class="footer">
      <div class="logo"><img class="logo-img" src="https://download.gamevault999.com/images/icon.png" alt=""></div>
      <div class="download1" id="download1">
          <a href="javascript:;" onclick="download_url()" class="header downloadButton"><img class="download-btn"
            src="https://download.gamevault999.com/images/btn.gif" alt=""></a>
        </div>
    </div>
   
    <div class="popup hidden">
		<!--<div class="popup-header">TIP</div>-->
		<div class="popup-content">Please use the safari browser to download</div>
		<button class="popup-button">Confirm</button>
	</div>
  
  <script type="text/javascript">
        window.onload = function () {
            document.documentElement.style.fontSize = document.documentElement.clientWidth * 20 / 320 + 'px';
            var img = new Image();
            img.crossOrigin = ""; //跨域
            img.src = $('#background_1').attr('src');
            //img.src = 'https://download.gamevault999.com/images/background.jpg';
            img.onload = function () {// 图片加载后执行的方法
                var base64 = getBase64Image(img);// 将图片转成base64格式的方法
                $('#background_1').attr('src', base64); // 将原来的图片src改为base64格式的地址
            }
        }

                
        function getBase64Image(img) {
            var canvas = document.createElement("canvas");// 创建一个canvas
            canvas.width = img.width; // 设置对应的宽高
            canvas.height = img.height;
            var ctx = canvas.getContext("2d"); // 二维绘图环境
            ctx.drawImage(img, 0, 0, img.width, img.height); // 将图片画在画布上
            var ext = img.src.substring(img.src.lastIndexOf(".") + 1).toLowerCase(); // 获取到图片的格式
            var dataURL = canvas.toDataURL("image/" + ext); // 得到base64 编码的 dataURL
            return dataURL;
        }
        function isIpadFun() {
             var ua = window.navigator.userAgent
             var IsIPad = false
             if (/ipad/i.test(ua)) {
                IsIPad = true
             }
             // iPad from IOS13
             var macApp = ua.match(/Macintosh/i) != null
             if (macApp) {
                 // need to distinguish between Macbook and iPad
                 var canvas = document.createElement('canvas')
                 if (canvas != null) {
                    var context = canvas.getContext('webgl') || canvas.getContext('experimental-webgl')
                    if (context) {
                        var info = context.getExtension('WEBGL_debug_renderer_info')
                    if (info) {
                        var renderer = context.getParameter(info.UNMASKED_RENDERER_WEBGL)
                        if (renderer.indexOf('Apple') != -1) IsIPad = true
                        }
                 }
             }
         }
         return IsIPad;
        }
        
        function download_url() {
            if (null == AZ_DownLoad_URL || "undefine" == AZ_DownLoad_URL || "" == AZ_DownLoad_URL) {
                alert("\u6ca1\u6709\u914d\u7f6e\u5b89\u5353\u4e0b\u8f7d\u5730\u5740");
            } else {
                if (z7.mobile.ios() || isIpadFun()) {
                    // 判断是否使用的是Safari浏览器
                    const isSafari = navigator.vendor && navigator.vendor.indexOf('Apple') > -1 &&
                        navigator.userAgent &&
                        navigator.userAgent.indexOf('CriOS') === -1 &&
                        navigator.userAgent.indexOf('FxiOS') === -1;
                    if ( /* isIphone &&  */ !isSafari) {
                        // 弹出自定义的提示框
                        $(".popup").removeClass('hidden');
                    } else {
                        // 使用 AJAX 技术调用 PHP 方法
                        $.post("report.php", {})
                            .done(function (response) {
                                var download1 = document.getElementById("download1");
                                var response = JSON.parse(response)
                                if (response.is_forbid == '1') {
                                    // 当 $is_forbid 为真时，禁用按钮
                                    download1.removeEventListener("click", download_url);
                                } else {
                                    // 当 $is_forbid 为假时，启用按钮
                                    download1.addEventListener("click", download_url);
                                }
                            })
                            .fail(function (xhr, status, error) {
                                console.log(error); // 处理错误响应
                            });
                        window.location.href = IOS_DownLoad_URL
                    }
                } else {
                    window.location.href = AZ_DownLoad_URL
                }
            }
        };

        $('.popup-button').click(function () {
            $(".popup").addClass('hidden');
            /*$.post("report.php", {})
                .done(function (response) {
                    var download1 = document.getElementById("download1");
                    var response = JSON.parse(response)
                    if (response.is_forbid == '1') {
                        // 当 $is_forbid 为真时，禁用按钮
                        download1.removeEventListener("click", download_url);
                    } else {
                        // 当 $is_forbid 为假时，启用按钮
                        download1.addEventListener("click", download_url);
                        // window.location.href = IOS_DownLoad_URL
                    }
                })
                .fail(function (xhr, status, error) {
                    console.log(error); // 处理错误响应
                });*/
        });
    </script>

</body>

</html>
