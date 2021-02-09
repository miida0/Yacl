# CURL

### 参考

- [curl cookbook](https://catonmat.net/cookbooks/curl)

### POST请求

- `-X`发送一个空数据的POST请求
```shell
curl -X POST https://www.domain.com
```

- `-d`发送POST数据
  - 使用`-d`参数时，`header`中`Content-Type`被设置成了`application/x-www-form-urlencoded`。
  - 使用`-d`参数时，`-X POST`可以省略，`curl`自动隐形设置为`POST`请求。
```shell
curl -d "user=user&passwd=passwd" -X POST https://www.domain.com/login/
```

- 更直观的`POST`请求数据
```shell
curl -d "user=user" -d "passwd=passwd" https://www.domain.com/login/
```

- `-L`跟踪重定向
```shell
curl -L -d "user=user" https://www.domain.com/login/
```

- `-H 'Content-Type: application/json'`发送`JSON`格式的数据
  - 必须显式地使用`-H 'Content-Type: application/json'`
```shell
curl -d '{"user":"user","passwd":"passwd"}' -H 'Content-Type: application/json' https://www.domain.com/login/
```

- `-H 'Content-Type: text/xml'`发送`XML`格式的数据
```shell
curl -d '<user><login>ann</login><password>123</password></user>' -H 'Content-Type: text/xml' https://www.domain.com/login/
```

- `-H 'Content-Type: text/plain'`发送`纯文本`格式的数据
```shell
curl -d 'hello curl' -H 'Content-Type: text/plain' https://www.domain.com/login/
```

- `-d '@data.txt'`发送数据文件
  - 文件名前的`@`不可省略。
```shell
curl -d '@data.txt' https://www.domain.com/login/
```

- `--data-urlencode`
  - 使用`--data-urlencode`替换`-d`参数显式地进行`urlencode`。
  - 不使用`--data-urlencode`参数时需要确保数据已经进行了`urlencode`。
```shell
curl --data-urlencode "comment=hello world" https://www.domain.com/login/
```

- `-F`发送一个文件
  - 数据中的`file`是上传表单的`name`。
  - `-F`会隐式地把`Content-Type`设置成`multipart/form-data`。
```shell
curl -F 'file=@image.png' https://www.domain.com/profile/
```

- 发送文件并设置`MIME`
```shell
curl -F 'file=@image.png;type=image/png' https://www.domain.com/profile/
```

- 发送文件同时重命名
  - 服务器只接收到了`new.png`。
```shell
curl -F 'file=@image.png;type=image/png;filename=new.png' https://www.domain.com/profile/
```