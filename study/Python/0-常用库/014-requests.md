##### 1 安装

```
pip3 install requests
```


##### 2 用法


四种请求方式：get post put delete

```
res1 = requests.get('http://httpbin.org/get')  # 发送一个get请求；get类型用来获取数据，请求数据在url中

res2 = requests.post('http://httpbin.org/post', data={'key': 'value'})  # 发送一个post请求 ，post类型用来提交数据，请求数据在请求体中，就是data中

res3 = requests.put('http://httpbin.org/put', data={'key': 'value'})  # 发送一个put请求，put类型用来修改数据，请求数据在请求体中

res4 = requests.delete('http://httpbin.org/delete')  # 发送一个delete请求，delete用来删除数据，请求数据在url中
```

获得一个 Response 对象

```
response = requests.request('get','http://httpbin.org/get')  # 返回请求结果的响应码
```

给 get 请求增加请求参数

1. Requests 允许你使用 params 关键字参数，

2. 以一个字符串字典来提供这些参数。

3. 注意字典里值为 None 的键都不会被添加到 URL 的查询字符串里。

4. 字典的 value 可以是列表

```
payload = {'key1': 'value1', 'key2': ['value2', 'value3']}
res5 = requests.get('http://httpbin.org/get', params=payload)
```

响应内容

1. Requests 会自动解码来自服务器的内容。大多数 unicode 字符集都能被无缝地解码。
2. 请求发出后，Requests 会基于 HTTP 头部对响应的编码作出有根据的推测。
3. 当你访问 r.text 之时，Requests 会使用其推测的文本编码。
4. Requests 使用了什么编码，并且能够使用 r.encoding 属性来改变它
5. 如果你改变了编码，每当你访问 r.text ，Request 都将会使用 r.encoding 的新值

```
res6 = requests.get('https://api.github.com/events')
res7 = requests.get('http://httpbin.org/get')

res6.encoding
res7.encoding

res6.text
res7.text
```
JSON 响应内容

1. Requests 中也有一个内置的 JSON 解码器
2. 如果 JSON 解码失败， r.json() 就会抛出一个异常
3. 响应内容是 401 (Unauthorized)，尝试访问 r.json() 将会抛出 ValueError: No JSON object could be decoded 异常。
4. 成功调用 r.json() 并不意味着响应的成功.有的服务器会在失败的响应中包含一个 JSON 对象（比如 HTTP 500 的错误细节）
5. 要检查请求是否成功，请使用 r.raise_for_status() 或者检查 r.status_code 是否和你的期望相同

```
res9 = requests.get('https://api.github.com/events')
res9.json()
res9.raise_for_status()
res9.status_code
```

请求添加 HTTP 头部，只要传递一个 dict 给 headers 参数就可以了

```
url = 'https://api.github.com/some/endpoint'
headers = {'user-agent': 'my-app/0.0.1'}
r = requests.get(url, headers=headers)


```
POST 请求

1. 传递一个字典给 data 参数。数据字典在发出请求时会自动编码为表单形式
2. data 参数传入一个元组列表。在表单中多个元素使用同一 key 的时候，这种方式尤其有效
3. 发送 string 而不是 dict
4. 使用 json 参数直接传递，然后它就会被自动编码
```
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.post("http://httpbin.org/post", data=payload)
print(r.text)

payload = (('key1', 'value1'), ('key1', 'value2'))
r = requests.post('http://httpbin.org/post', data=payload)

url = 'https://api.github.com/some/endpoint'
payload = {'some': 'data'}
r = requests.post(url, data=json.dumps(payload))

url = 'https://api.github.com/some/endpoint'
payload = {'some': 'data'}
r = requests.post(url, json=payload)
```
访问cookie

```
url = 'http://example.com/some/cookie/setting/url'
r = requests.get(url)

r.cookies['example_cookie_name']
```

发送cookies参数
```
url = 'http://httpbin.org/cookies'
cookies = dict(cookies_are='working')
r = requests.get(url, cookies=cookies)
```
