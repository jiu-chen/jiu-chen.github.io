# go http请求中body的封装方法


go语言不像python,  它是静态强类型语言, 在使用变量之前必须声明好类型。  
在使用go `net/http` 发送 http 请求的时候，常常遇到请求所带的body是一个value类型不唯一的情况。比如有一个这样的request json body:
``` json
{
    "id": 10,
    "name": "jc",
    "groups": ["g1", "g2"],
    "info": {
        "address": "xxxx",
        "hobby": ["noodle","sandwich"],
        "age": 11
    }
}
```
在python中，没有类型要求，只需要一步一步写下去即可:
``` python
import request
#  ...
body = {
    "id": 10,
    "name": "jc",
    "groups": ["g1", "g2"],
    "info": {
        "address": "xxxx",
        "hobby": ["noodle","sandwich"],
        "age": 11
    }
}
resp = requests.post(url, headers=headers, data=json.dumps(body))
```
但是在go中，必须将这样的body封装成一个固定类型的变量, 因为json body 中的value类型有int, string, list, map, 所以只能用interface{}作为body的value类型
``` go
var body map[string]interface{} =map[string]interface{} {
    "id": 10,
    "name":"js",
    "groups": []string{"g1","g2"},
    "info": map[string]interface{}{
        "address":"xxxx",
        "hobby": []string{"noodle","sandwich"},
        "age":11,
    }
}
```
然后将其作为变量传入函数: 
``` go
func send(body map[string]interface{}) error {
    bodyBytes, err := json.Marshal(body) // Marshal 
	if err != nil {
		logs.Error("json Marshal fail.")
	}
	reqBody := io.NopCloser(bytes.NewReader(bodyBytes)) // 构造 io.ReadCloser
	request := &http.Request{
		Method: "POST",
		URL:    url,
		Header: map[string][]string{
			"Content-Type": {"application/json"},
		},
		Body: reqBody,
	}
	resp, err := http.DefaultClient.Do(request)
    //...
    return nil
}
```
这就是go中http body 格式比较复杂的封装方法  
试试吧


