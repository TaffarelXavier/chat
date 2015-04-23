<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <meta http-equiv="Content-Type" content="text/html;" />
        <script src="js/jquery-1.10.1.min.js"></script>
        <title>Offset</title>
        <style type="text/css">
            .right{
                position:fixed;
                width: 200px;
                height: 100%;
                right: 0px;
                top:0px;
                overflow:auto;
            }
            .right ul{
                padding:0px;
                margin:0px;
            }
            .right ul li{
                list-style:none;
                margin:2px;
            }
            .right ul li a{
                padding:10px 5px;
                background:#4989F1;
                color:white;
                display:block;
            }
            .right ul li a:hover{
                background: white;
                color:black;
            }
            .tooltip{
                position: fixed;
                width: 200px;
                height:200px;
                border:1px dotted #ccc;
                box-shadow:0px 0px 10px 0px rgba(0,0,0,0.5);
                z-index:9999;
                background:white;
                border-radius: 0px;
                text-align: center;
                padding:10px;
            }
            .tooltip > .arrow{
                position: absolute;
                border-top:15px solid transparent;
                border-left:15px solid white;
                border-bottom:15px solid transparent;
                border-right:15px solid transparent;   
                left:100%;
            }
            .tooltip textarea{
                position: absolute;
                max-height: 90%;
                bottom:5px;
                width: 200px;
                top:30px;
                left:0px;
                right:0px;
                margin:0px auto;
            }
            .tooltip span{
                display:block;
                text-align:left;
            }
        </style>
    </head>

    <body>
        <div class="tooltip" hidden="">
            <p class="arrow"></p>
            <span class="tooltip-title">Francisco Taffarel Xavier</span>
            <textarea>a</textarea>
        </div>
        <a href="#">Francisco Taffarel Xavier</a>
        <div class="right">
            <ul>
                <?php
                for ($i = 0; $i < 100; $i++) {


                    $hash = hash("whirlpool", md5(uniqid(rand(), true)));

                    $only_letters = preg_replace("/([0-9])/mi", "", $hash);

                    $only_numbers = preg_replace("/([a-z])/mi", "", $hash);

                    $total_palavras = strlen($only_numbers);

                    $n1 = substr($only_numbers, 0, 10);
                    $n2 = substr($only_numbers, 10, 10);
                    $n3 = substr($only_numbers, 20, 10);
                    $n4 = substr($only_numbers, 30, 10);

                    $s1 = substr($only_letters, 0, 10);
                    $s2 = substr($only_letters, 10, 10);
                    $s3 = substr($only_letters, 20, 10);
                    $s4 = substr($only_letters, 30, 10);

                    $p1_array = [
                        "$n1-$s1-$n3-$s4-$n2-$s3-$n1",
                        "$s3-$s1-$n2-$s1-$n1-$n4-$s2",
                        "$n4-$s2-$s1-$n4-$s3-$s3-$n2",
                        "$s2-$n2-$s4-$s3-$n3-$s1-$n3",
                        "$s1-$n3-$n2-$s2-$s4-$n3-$s3",
                        "$n1-$s4-$n4-$s4-$n3-$s4-$n2",
                        "$s3-$s1-$n2-$s2-$n2-$s3-$s1",
                        "$n2-$s3-$s2-$n3-$n1-$s4-$s1"
                    ];


                    $patt1 = "/("
                            . "\d{10}\-\w{10}-\d{10}\-\w{10}-\d{10}\-\w{10}\-\d{10}|"
                            . "\w{10}\-\w{10}-\d{10}\-\w{10}-\d{10}\-\d{10}\-\w{10}|"
                            . "\d{10}\-\w{10}-\w{10}\-\d{10}-\w{10}\-\w{10}\-\d{10}|"
                            . "\w{10}\-\d{10}-\w{10}\-\w{10}-\d{10}\-\w{10}\-\d{10}|"
                            . "\w{10}\-\d{10}-\d{10}\-\w{10}-\w{10}\-\d{10}\-\w{10}|"
                            . "\d{10}\-\w{10}-\d{10}\-\w{10}-\d{10}\-\w{10}\-\d{10}|"
                            . "\w{10}\-\w{10}-\d{10}\-\w{10}-\d{10}\-\w{10}\-\w{10}|"
                            . "\d{10}\-\w{10}-\w{10}\-\d{10}-\d{10}\-\w{10}\-\w{10}"
                            . ")/";


                    $chave = array_rand($p1_array);

                    $verificar = preg_match($patt1, $p1_array[$chave]);

                    echo "<li><a class='tol' data-hash='$p1_array[$chave]\n$verificar'>Teste $i</a></li>";
                }
                ?>
            </ul>
        </div>
        <script>

            permitir = 0;
            topo = 0;
            isSobre = false;
            manter = false;

            document.onmousemove = function (e) {

                w = Math.ceil(screen.width / 2);
                h = Math.ceil(screen.height / 2);

                topo = e.clientY;

                _right = 200 + "px";

                if (manter === false) {
                    if (e.clientX > w) {
                        if (e.clientY > h) {
                            $(".tooltip").css({top: e.clientY - $(".tooltip").width() + 40 + "px", right: _right});
                            $(".arrow").css({top: 140 + "px", right: _right});
                            //$("textarea").val("a");
                        }
                        else {
                            $(".tooltip").css({top: e.clientY - 40 + "px", right: _right});
                            $(".arrow").css({top: 0 + "px", right: _right});
                            //$("textarea").val("b");
                        }
                    } else {
                        if (e.clientY > h) {
                            $(".tooltip").css({top: e.clientY - $(".tooltip").height() - 10 + "px", right: _right});
                            //$("textarea").val("c");
                        }
                        else {
                            $(".tooltip").css({top: e.clientY - 0 + "px", right: _right});
                            //$("textarea").val("d");
                        }
                    }
                }
            };


            document.onclick = function () {
                if (isSobre === false) {
                    $(".tooltip").hide();
                }
            };

            $(".tol").mouseover(function () {
                var _this = $(this);

                $(".tooltip-title").html(_this.text());
                $("textarea").val(_this.attr('data-hash'));

                isSobre = true;
                manter = false;
                $(".tooltip").show();
            }).mouseout(function () {
                isSobre = false;
                manter = true;
            });

            $(".tooltip").mouseover(function () {
                isSobre = true;
            }).mouseout(function () {
                isSobre = false;
            });


            document.onkeyup = function (e) {
                if (e.keyCode === 27) {
                    $(".tooltip").hide();
                }
            };

        </script>
    </body>
</html>
