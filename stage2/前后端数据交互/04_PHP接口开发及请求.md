# PHP接口开发及请求
## 接口开发
>接口开发通常是从前端拿到数据，经过处理后，返回给前端人员整理数据后的数据，因此通常分为以下几步：
1. 从前端获取数据
```
$uname = $_REQUEST["uname"]
```
2. 处理数据
> 处理数据通常是从数据库中查询数据
```
$servername = "localhost";
$username = "root";
$password = "root";
$dbname = "students";

	
//创建数据库连接
$conn = new mysqli($servername,$username,$password,$dbname);
//设置字符集
$conn->set_charset("utf8");
//检测数据库连接
if($conn->connect_error){
	die("连接失败: " . $conn->connect_error);
}
echo "连接成功";

// 数据库连接成功后写SQL语句
$sql = "select * from user where uname='$uname'";
$result = $conn->query($sql);
if($result->num_rows > 0){
    while($row=mysqli_fetch_assoc($result)){
        $rows[] = $row;
    }
}

//从数据库中获取的所有数据都在$rows中

```
3. 将数据输出给前端开发人员
```
// 把得到的结果集转换为json
echo json_encode($rows);
```

# 请求
>前端发起请求的方式通常为使用jQuery的ajax
```
    $.ajax({
        url:"接口地址",
        data:{uname:"用户名"},
        success:function(data){
            //从服务器上获取数据，解析数据
            console.log(data);
            ...
        }
    })
```
>或者使用form表单提交
```
<form action="接口地址">
    <input type="text" name="uname">
    <input type="submit />
</form>
```