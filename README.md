<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	<title>Our Story of &amp; love</title>

    <link type="text/css" rel="stylesheet" href="./css/default.css">
	<script type="text/javascript" src="./js/jquery.js"></script>
	<script type="text/javascript" src="./js/jscex.js"></script>
	<script type="text/javascript" src="./js/jscex-parser.js"></script>
	<script type="text/javascript" src="./js/jscex-jit.js"></script>
	<script type="text/javascript" src="./js/jscex-builderbase.js"></script>
	<script type="text/javascript" src="./js/jscex-async.js"></script>
	<script type="text/javascript" src="./js/jscex-async-powerpack.js"></script>
	<script type="text/javascript" src="./js/functions.js" charset="utf-8"></script>
	<script type="text/javascript" src="./js/love.js" charset="utf-8"></script>
</head>
    <body>
        <!--这里放音乐哦 -->
		<audio autoplay="autopaly">
			<source src="./iloveu.mp3" audio="" mp3"="">
		</audio>

        <div id="main">
            <!-- 不兼容的提醒 -->
            <div id="error">亲爱哒，您的浏览器无法显示呐，麻烦请换成谷歌，火狐，360浏览器。么么哒！(づ￣ 3￣)づ！</div>
            <div id="wrap">
                <div id="text">
			        <div id="code">
			        	<span class="say"> Our Story</span><br>
						<span class="say"> </span><br>
			        	<span class="say"> For  龙宝宝 &amp;  龙宝宝 </span><br>
						<span class="say"> </span><br>
                        <span class="say"> 还记得我们相识的时候吗, 或许是缘分，或许是注定的。</span><br>
						<span class="say"> </span><br>
			        	<span class="say"> 就像一场梦一样,有开心,也有吵闹。</span><br>
						<span class="say"> </span><br>
			        	<span class="say"> 彼此依赖，彼此关心，彼此温暖，谢谢你这么包容我，喜欢我，爱我。</span><br>
						<span class="say"> </span><br>
			        	<span class="say"> 我也爱你的善良，温柔，就是太容易吃醋了。。。</span><br>
						<span class="say"> </span><br>
			        	<span class="say"> 我性格好多缺点你也都看到。。。</span><br>
						<span class="say"> </span><br>
			        	<span class="say"> 我想要和你在一起真实的感受生命，和你生活在一起,嫁给我吧！</span><br>
                        <span class="say"> </span><br>
                        <span class="say"> ..永远的..</span><br>
						<span class="say"> </span><br>
                        <span class="say"><span class="space"></span>龙宝宝 与 龙宝宝</span>
			        </div>
                </div>
                <div id="clock-box">
                    龙宝宝<span class="STYLE1">与</span>龙宝宝<span class="STYLE1">已经相识了</span>
                  <div id="clock"></div>
              </div>
                <canvas id="canvas" width="1100" height="680"></canvas>
            </div>
            
        </div>
    
    <script>
    </script>

    <script>
    (function(){
        var canvas = $('#canvas');
		
        if (!canvas[0].getContext) {
            $("#error").show();
            return false;
        }

        var width = canvas.width();
        var height = canvas.height();
        
        canvas.attr("width", width);
        canvas.attr("height", height);

        var opts = {
            seed: {
                x: width / 2 - 20,
                color: "rgb(190, 26, 37)",
                scale: 2
            },
            branch: [
                [535, 680, 570, 250, 500, 200, 30, 100, [
                    [540, 500, 455, 417, 340, 400, 13, 100, [
                        [450, 435, 434, 430, 394, 395, 2, 40]
                    ]],
                    [550, 445, 600, 356, 680, 345, 12, 100, [
                        [578, 400, 648, 409, 661, 426, 3, 80]
                    ]],
                    [539, 281, 537, 248, 534, 217, 3, 40],
                    [546, 397, 413, 247, 328, 244, 9, 80, [
                        [427, 286, 383, 253, 371, 205, 2, 40],
                        [498, 345, 435, 315, 395, 330, 4, 60]
                    ]],
                    [546, 357, 608, 252, 678, 221, 6, 100, [
                        [590, 293, 646, 277, 648, 271, 2, 80]
                    ]]
                ]] 
            ],
            bloom: {
                num: 700,
                width: 1080,
                height: 650,
            },
            footer: {
                width: 1200,
                height: 5,
                speed: 10,
            }
        }

        var tree = new Tree(canvas[0], width, height, opts);
        var seed = tree.seed;
        var foot = tree.footer;
        var hold = 1;

        canvas.click(function(e) {
            var offset = canvas.offset(), x, y;
            x = e.pageX - offset.left;
            y = e.pageY - offset.top;
            if (seed.hover(x, y)) {
                hold = 0; 
                canvas.unbind("click");
                canvas.unbind("mousemove");
                canvas.removeClass('hand');
            }
        }).mousemove(function(e){
            var offset = canvas.offset(), x, y;
            x = e.pageX - offset.left;
            y = e.pageY - offset.top;
            canvas.toggleClass('hand', seed.hover(x, y));
        });

        var seedAnimate = eval(Jscex.compile("async", function () {
            seed.draw();
            while (hold) {
                $await(Jscex.Async.sleep(10));
            }
            while (seed.canScale()) {
                seed.scale(0.95);
                $await(Jscex.Async.sleep(10));
            }
            while (seed.canMove()) {
                seed.move(0, 2);
                foot.draw();
                $await(Jscex.Async.sleep(10));
            }
        }));

        var growAnimate = eval(Jscex.compile("async", function () {
            do {
    	        tree.grow();
                $await(Jscex.Async.sleep(10));
            } while (tree.canGrow());
        }));

        var flowAnimate = eval(Jscex.compile("async", function () {
            do {
    	        tree.flower(2);
                $await(Jscex.Async.sleep(10));
            } while (tree.canFlower());
        }));

        var moveAnimate = eval(Jscex.compile("async", function () {
            tree.snapshot("p1", 240, 0, 610, 680);
            while (tree.move("p1", 500, 0)) {
                foot.draw();
                $await(Jscex.Async.sleep(10));
            }
            foot.draw();
            tree.snapshot("p2", 500, 0, 610, 680);

            // 会有闪烁不得意这样做, (＞﹏＜)
            canvas.parent().css("background", "url(" + tree.toDataURL('image/png') + ")");
            canvas.css("background", "#ffe");
            $await(Jscex.Async.sleep(300));
            canvas.css("background", "none");
        }));

        var jumpAnimate = eval(Jscex.compile("async", function () {
            var ctx = tree.ctx;
            while (true) {
                tree.ctx.clearRect(0, 0, width, height);
                tree.jump();
                foot.draw();
                $await(Jscex.Async.sleep(25));
            }
        }));

        var textAnimate = eval(Jscex.compile("async", function () {
		    var together = new Date();
		    together.setFullYear(1996, 11,16); 			//时间年月日
		    together.setHours(12);						//小时	
		    together.setMinutes(0);					//分钟
		    together.setSeconds(0);					//秒前一位
		    together.setMilliseconds(0);				//秒第二位

		    $("#code").show().typewriter();
            $("#clock-box").fadeIn(500);
            while (true) {
                timeElapse(together);
                $await(Jscex.Async.sleep(1000));
            }
        }));

        var runAsync = eval(Jscex.compile("async", function () {
            $await(seedAnimate());
            $await(growAnimate());
            $await(flowAnimate());
            $await(moveAnimate());

            textAnimate().start();

            $await(jumpAnimate());
        }));

        runAsync().start();
    })();
    </script>
</body>
</html>
