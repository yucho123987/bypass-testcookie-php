# bypass-testcookie-php
A simple library written in PHP that helps you bypass the protection of the Nginx testcookie module.
## How to use
1. Download and include `testcookie-decrypt.php` in your project:
```php
require_once './testcookie-decrypt.php';
// Your code...
 ```
2. get the HTML code of the validation page (I use [php-curl-class](https://github.com/php-curl-class/php-curl-class) here but you can also use cURL even `file_get_contents()` :
```php
$url = 'http://nihao.rf.gd/'; // Your target URL
$curl = new Curl();
$curl->setUserAgent('Mozilla/5.0 (iPad; U; CPU OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5');
$curl->get($url);
if ($curl->error) {
  die('Error: '.$curl->errorMessage);
}
$html = $curl->response; // Note: You should check if the $html variable is the HTML code of validation page.
```
3. get the cookie value with just 2 lines of code:
```php
$abc = parseabc($html);
$value = getTestCookieValue($abc[0], $abc[1], $abc[2]);
```
4. Now set a cookie named `__test` and its value should be the content of the variable $value, then send a request again  to see if you are successful!
```
$curl->setCookies(array(
  '__test' => $value
));
$curl->get($url);
// ...
```
## Thanks
[slowaAES](https://github.com/octopius/slowaes)