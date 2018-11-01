ajax中接受PHP传递的json文件的输出格式
在学ajax在客户端接受传递的数据的时候，报错。发现是服务端传递数据输出的函数问题，用echo 而不是 var_dump
php中按着json格式写好了数据 
```
if(empty($_GET['id'])){
 	$json = json_encode($data);
 	var_dump($json);
 }else{
 	foreach ($data as $key) {
 		if($_GET['id']==$key['id']){
 		$json = json_encode($key);
 		var_dump($json);  //var_dump 会带有数据的详细信息输出，这里是需要作为数据返回给客户端。用echo输出纯数据
 	}
 	}
 }
 ```
 此时在客户端利用ajax接受进行判断
 ```
 var xhr = XMLHttpRequest()
 xhr.open('GET','...php')
 xhr.send()
 xhr.onreadystatechange=function(){
  if(this.readyState!==4)return
  console.log(this.responseText)
  ```
  这里后台能打印出来，直接进行JS的JSON.parse()会报错。翻来覆去折腾不知道怎么回事。对比学习资料才发现应该用echo
  这里是输出字符串数据进行调用，类似于在php中HTML的混编模式，用var_dump会添加解释信息，造成错误
 
