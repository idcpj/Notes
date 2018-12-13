```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">

    <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
    <script src="https://cdn.bootcss.com/jquery-validate/1.19.0/jquery.validate.js"></script>
    <script src="https://cdn.bootcss.com/jquery-validate/1.19.0/localization/messages_zh.min.js"></script>
    <title>Document</title>
    <style>
        .form-validate .error{
            color: red;
        }
        .check::after{
            content: "✔验证成功";
            color:green;
            margin-left: 5px;
        }
    </style>
</head>

<body>

    <form class="form-validate" action="post">
        <!-- 验证长度 -->
        <label  > 账户 <input type="text" name="username" minlength="3"  required> </label> <br>
        <!-- 验证密码 -->
        <label> 密码 <input type="password" id="password" name="password"  > </label> <br>
        <label> 验证密码 <input type="password" name="valid_password" equalTo="#password" > </label> <br>
        <!-- 验证异步 -->
        <label >昵称 <input type="text" name="nickname" remote="a.php" > </label> <br>
        <!-- 验证整数 -->
        <label >年龄 <input type="text" name="age"  range="[3,200]"> </label><br>
        <!-- 邮箱验证 -->
        <label >邮箱 <input type="text" name="email" email="true"> </label>     <br>
        <!-- 验证自定义 -->
        <label > 手机号 <input type="text" name="phone" isMobile="true" ></label>  <br>
        <!-- 验证整数 -->
        <label >QQ <input type="text" name="qq" digits="true" ></label> <br>
        <!-- 图片 -->
        <label >图片 <input type="file" name="file"  accept="image/*"></label> <br>
        <label >性别
            <input type="radio" name="sex" value="1"  > 男
            <input type="radio" name="sex" value="2" > 女
        </label> <br>

        <label >
            省份
            <select name="identity" required="true" required>
                <!-- required vlaue不能为空 -->
                <option value="">请选择</option>  
                <option value="浙江">浙江</option>
                <option value="北京">北京</option>
                <option value="湖南">湖南</option>
                <option value="湖北">湖北</option>
            </select>
        </label> <br>

        <input type="submit" value="提交">
    </form>
       

    <script>
            // 自定义添加验证眼熟
        $.validator.addMethod("isMobile",function(value,element,params){
            var length = value.length;
            var mobile = /^(13[0-9]{9})|(18[0-9]{9})|(14[0-9]{9})|(17[0-9]{9})|(15[0-9]{9})$/;
            return this.optional(element) || (length == 11 && mobile.test(value));
        },"手机格式不正确");


        $(".form-validate").validate({
            debug:true, 
            //键盘松开时触发
            onfocusout: function (element) {
                //验证前删除 check类
                // $(element).siblings("label").remove();
                $(element).valid();
            },
            //把错误写在字段后面
            errorPlacement:function(error, element) {  
                error.appendTo(element.parent());  
            },
            success:function(label){
                // label.addClass("check");
            },
            messages:{
                nickname:{
                    remote:"重复的昵称"
                }            
            }
        });
    </script>
</body>
</html>
```