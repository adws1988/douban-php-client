## Examples of douban-php-client ##



1，请先申请[API\_KEY](http://www.douban.com/service/apikey/)，得到API\_KEY和私钥。

2，API认证授权。豆瓣API认证通过以下三个步骤完成：

> a). 获取未授权的 Request Token

> b). 请求用户授权 Request Token

> c). 使用授权后的 Request Token 换取 Access Token

Zend\_Gdata\_DouBan的方法programmaticLogin完成了上述过程，详细过程请参考代码。

下列命令生成了一个Zend\_Gdata\_DouBan对象，并完成了豆瓣API认证过程：
```
$client = new Zend_Gdata_DouBan($api, $secret);
$client->programmaticLogin();
```
在命令行运行上述代码时，输出如下提示信息：
```
please paste the url in your webbrowser, complete the authorization then come back:
http://www.douban.com/service/auth/authorize?oauth_token=5d6f7b964ef6f60c184e72c2ece4e224

```
将上述url连接拷贝到浏览器，进入到douban api认证授权页面，点击同意，即可完成对本次api访问的授权。

3，正常的douban api操作。完成上述认证过程，即可使用Zend\_Gdata\_DouBan所提供各种接口进行操作，下面例举了几个简单应用：
```
$peopleEntry = $client->getPeople('ahbei');
assert ($peopleEntry->getId() == 'http://api.douban.com/people/1000001');
assert ($peopleEntry->getLocation()->getText() == '北京');
assert ($peopleEntry->getTitle()->getText() == '阿北');

$peopleFeed = $this->_client->searchPeople('boy', 2, 10);
$arr = $peopleFeed->getEntry();
$arr_title = array();
foreach ($arr as $entry) {
    if ($entry->getTitle()) {
        $arr_title[$entry->getTitle()->getText()] = 1;
    }
}
assert (array_key_exists('cow-boy', $arr_title));

$peopleEntry = $client->getAuthorizedUid();
assert ($peopleEntry->getUid()->getText() == "2463802");

$peopleFeed = $this->_client->GetFriends("2463802");
$arr = $peopleFeed->getEntry();
$uid_arr = array();
foreach ($arr as $entry) {
    if ($entry->getUid()) {
        $uid_arr[$entry->getUid()->getText()] = 1;
    }
}
assert (array_key_exists("jili8", $uid_arr));
```

更多使用示例，请参考test\_douban.php

oauth的web示例请参考[douban-oauth-sample](http://code.google.com/p/douban-oauth-sample/source/browse/trunk#trunk/php)