<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
    margin: 0;
    padding: 0;
}
.main{
    width: 800px;
    height: 1120px;
    margin: 10px auto;
    overflow: hidden; 
    box-shadow: 2px 2px 2px 2px silver;
}
.header{
    position: relative;
    width: 100%;
    height: 60px;
    line-height: 60px;
}
.header h2{
    float: left;
    margin: 10px
     40px;
    width: 120px;
    font-weight: 500;
    color: rgb(84, 185, 172);
}
.header p{
    float: left;
    margin-top: 4px;
    color: rgb(155, 155, 155);
}
.border{
    border:0;
    position: relative;
    width: 100%;
    height: 8px;
}
.border_a{
    position: absolute;
    top: 0;
    left: 0;
    width: 160px;
    height: 8px;
    background-color:rgb(84, 185, 172); 
    margin-left: 0;
}
.border_a::after{
    content: '';
    position: absolute;
    top:2.4px;
    right: -5.5px;
    width: 0;
    height: 0;
    border-top: 5.6px solid rgb(84, 185, 172);
    border-bottom:5.6px solid transparent;
    border-left:5.6px solid transparent;
    border-right:5.6px solid transparent;
    transform: rotate(45deg);
}
td{
    border:0px!important;
}
.border_b{
    position: absolute;
    top: 0;
    right: 0;
    width: 620px;;
    height: 8px;
    background-color:rgb(155, 155, 155);
}
.border_b::before{
    content: '';
    position: absolute;
    top:-5px;
    left: -5.5px;
    width: 0;
    height: 0;
    border-top: 5.6px solid rgb(155, 155, 155);
    border-bottom:5.6px solid transparent;
    border-left:5.6px solid transparent;
    border-right:5.6px solid transparent;
    transform: rotate(-135deg);
}
.content{
    width: 700px;
    height: 1000px;
    border: 2px solid rgb(84, 185, 172);
    border-bottom:0px ;
    border-right: 0;
    margin: 20px auto;
}
.content_db1,
.content_db2,
.content_db3,
.content_db4,
.content_db5
{
    position: relative;
    width: 100%;
    height: 170px;
    border-bottom: 2px solid rgb(84, 185, 172);
}
.content_db1{
    position: relative;
    width: 100%;
    height: 160px;
    border-bottom: 2px solid rgb(84, 185, 172);
}
.content_db5{
    border: 0;
    padding-top:10px;
}
.content_db5 p{
    margin-bottom: 0px;
}
.content_db1 table tr td{
    display: inline-block;
    box-sizing: border-box;
    width: 230px;
    height: 40px;
    padding: 0 5px;
    line-height: 40px;
}
.tsd{
    display: inline-block;
    width:118px;
    height: 118px;
}
.content_db1 table tr td img{
    width: 118px;
    height: 118px;
    margin-left: 40px;
}
.content_db1 span,
.content_db2 span,
.content_db3 span,
.content_db4 span,
.content_db5 span
{
    position: absolute;
    top: -17px;
    left: -15px;
    width:120px;
    height: 17px;
    background-color: rgb(122, 213, 201);
    text-align: center;
    line-height: 17px;
    color: aliceblue;
}
.content_db1 span:after,
.content_db2 span:after,
.content_db3 span:after,
.content_db4 span:after,
.content_db5 span:after
{
    content: '';
    position: absolute;
    top: 5px;
    left: 108px;
    border-top: 12px solid rgb(122, 213, 201);
    border-left: 12px solid transparent;
    border-bottom: 12px solid transparent;
    border-right: 12px solid transparent;
    transform: rotate(45deg);
}
.content_db1 span::before,
.content_db2 span::before,
.content_db3 span::before,
.content_db4 span::before,
.content_db5 span::before
{
    content: '';
    position: absolute;
    top: 7px;
    left: 4px;
    border-top: 10px solid rgb(80, 198, 180);
    border-left: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-right: 10px solid transparent;
    transform: rotate(-135deg); 
}
.content_db2>ul>li{
    list-style: none;
    margin: 0 0 10px 20px;
}
.content_db3  p,
.content_db4  p,
.content_db5  p
{
    display: block;
    margin:  0 0 0px 20px;
}
h5{
    display: inline-block;
    margin-left: 20px;
}
        </style>
</head>
<body>
    <div class="main">
        <div class="header">
            <h2>个人简历</h2>
          <p>  &nbsp;&nbsp; &nbsp;该简历由html5+css3制作</p>
        </div>
        <div class="border">
        <div class="border_a"></div>
        <div class="border_b"></div>
        </div>
        <div class="content">
            <div class="content_db1">
                <span>基本信息</span>
                <table>
                    <tr>
                        <td>姓名:苗忠豪</td>
                        <td>年龄:22岁</td>
                    </tr>
                    <tr>
                        <td>性别:男</td>
                        <td>身份:本科应届生</td>
                         </tr>
                    <tr>
                        <td>电话:15634017180</td>
                        <td>邮箱:2563591125@qq.com</td>
                    </tr>
                </table>
            </div>
            <div class="content_db2"><span>求职意向</span>
                <ul>
                    <li>意向职位:web前端实习生</li>
                    <li>意向城市:山东济南</li>
                    <li>意向薪资:可面议</li>
                    <li>现实情况:大四在校生</li>
                </ul>
            </div>
            <div class="content_db3"><span>教育背景</span>
                <p class="3p1">2019-09~2023-06</p>
                <p class="3p2">山东管理学院</p>
                <p class="3p3">计算机科学与技术专业</p>
                <p class="3p4"><h5>主修课程:</h5>专业基础课程:电路原理、数字逻辑、微机原理、操作系统原理、计算机原理、算法与数据结构、C语言</p>
            </div>
            <div class="content_db4"><span>荣誉证书</span>
            <br><p class="5p1"><strong>·</strong>英语四级，听说读写能力良好，能流利的用英语进行日常交流，能快速浏览英文文档和书籍；</p>
            <br><p class="5p2"><strong>·</strong>通过二级甲等普通话水平测试</p>
           </div>
            <div class="content_db5"><span>自我评价</span>
            <p>工作积极认真，细心负责，在大学四年间学习专业知识的情况下熟悉并熟练运用办公自动化软件，善于在工作、学习中发现问题，解决问题
                。喜欢学习，踏实肯干，喜欢动手跟动脑结合。认真负责，喜欢团队合作也比较适合独立工作，有很强的社会责任感，
                喜欢迎接挑战，吃苦耐劳。
            </p></div>
        </div>
    </div>
</body>