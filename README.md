# responsive-slider
range slider



<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
    <script type="text/javascript" src="jquery.js"></script>
    <!--<script type="text/javascript" src="jquery-ui.js"></script>-->
    <style>
        .slider{
            position: relative;
            width: 30px;
            float: right;
            margin-top: 2%;
            margin-right: 100px;
            background:#0080c0;
            border-radius:20px;
            border:1px solid #000;
        }
        .dragDiv{
            position: absolute;
            top: 0px;
            width: 30px;
            height: 30px;
            background:#ff0000;
            border-radius:30px;
            border:1px solid #000;
        }
    </style>
    <script>
        var activityHeight = window.innerHeight;
        var halfactivityHeight = window.innerHeight/2;
        var noofBlocks = 2;
        var isDown = false;
        $(document).ready(function(){
            $( window ).resize(function(){resizeFn()});
            $(".slider").css("height",halfactivityHeight);
            $(".dragDiv").bind("mousedown", onSliderMouseDown);
            $(window).bind("mousemove", onSliderMouseMove);
            $(window).bind("mouseup", onSliderMouseUp);
            applyDrag();
        });
        function onSliderMouseDown(){
            isDown = true;
        }
        function onSliderMouseMove(event) {
            if (isDown) {
                var sliderHeight =  $(".slider").height();
                var innerDivHeight =  $(".dragDiv").height();
                var innerDivTop = event.pageY-$(".slider").offset().top-innerDivHeight/2;
                var posPercVal =  innerDivTop/(sliderHeight-innerDivHeight);
                posPercVal = Math.round(posPercVal*noofBlocks)/noofBlocks;
                if (posPercVal < 0) posPercVal = 0;
                else if (posPercVal > 1) posPercVal = 1;
                $(".dragDiv").attr("posPerc",posPercVal);
                var applyTop = (sliderHeight-innerDivHeight) * posPercVal;
                $(".dragDiv").css("top",applyTop);
            }
        }
        function onSliderMouseUp(){
            isDown = false;
        }
        function resizeFn() {
                halfactivityHeight = window.innerHeight/2;
                $(".slider").css("height",halfactivityHeight);
                applyDrag();
        }
        function applyDrag() {
            var sliderHeight =  $(".slider").height();
            var innerDivHeight =  $(".dragDiv").height();
            var posPerc = $(".dragDiv").attr("posPerc");
            if (posPerc) {
                var newTop = (sliderHeight-innerDivHeight)*posPerc;
                $(".dragDiv").css("top",newTop+"px");
            }
        }
    </script>
</head>
<body>    
    <div class="slider">
        <div class="dragDiv" attr="posPerc"></div>
    </div>
</body>
</html>
