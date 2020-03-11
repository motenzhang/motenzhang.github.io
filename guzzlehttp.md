<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [获取返回数据](#%E8%8E%B7%E5%8F%96%E8%BF%94%E5%9B%9E%E6%95%B0%E6%8D%AE)
- [截获异常并返回记录异常信息](#%E6%88%AA%E8%8E%B7%E5%BC%82%E5%B8%B8%E5%B9%B6%E8%BF%94%E5%9B%9E%E8%AE%B0%E5%BD%95%E5%BC%82%E5%B8%B8%E4%BF%A1%E6%81%AF)

<!-- /MarkdownTOC -->
# Editor's Choice: GuzzleHttp
> {info} 替代CURL 次于app()->handle

<a id="%E8%8E%B7%E5%8F%96%E8%BF%94%E5%9B%9E%E6%95%B0%E6%8D%AE"></a>
## 获取返回数据
```php
// form_params填入参数
$response = $client->request('POST', 'getUsersByLevel', [
    'headers' => $headers,
    'form_params' => [
        'level' => $userInfo['department_info'][0]['department_level']
    ]
]);
# 获取返回数据需参考文档/源码 并非直接打印response
$result = $response->getBody()->getContents();
```
<a id="%E6%88%AA%E8%8E%B7%E5%BC%82%E5%B8%B8%E5%B9%B6%E8%BF%94%E5%9B%9E%E8%AE%B0%E5%BD%95%E5%BC%82%E5%B8%B8%E4%BF%A1%E6%81%AF"></a>
## 截获异常并返回记录异常信息
```php
# 异常详见http://docs.guzzlephp.org/en/stable/quickstart.html#exceptions
catch ( \GuzzleHttp\Exception\RequestException $e ) {
    // 发送网络错误(连接超时、DNS错误等)时
    echo $e->getRequest();
    if ($e->hasResponse()) {
        echo $e->getResponse();
    }
}
catch (\GuzzleHttp\Exception\ConnectException $e) {
    // 返回连接错误/网络错误比如url不对
    // ConnectException继承自RequestException
    Log::error( $e->getMessage() );
} catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // 返回400 500 错误
    // ClientException for 400-level errors
    // ServerException for 500-level errors
    // BadResponseException = ClientException + ServerException
    Log::error( $e->getMessage() );
}
```