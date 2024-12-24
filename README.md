# bypass-testcookie-php

A simple PHP library designed to help you bypass the protection mechanism of the Nginx testcookie module.

## Usage Instructions

### 1. Download and Include the Library

First, download the `testcookie-decrypt.php` file and include it in your project:

```php
require_once './testcookie-decrypt.php';
// Your code here...
```

### 2. Retrieve the HTML of the Validation Page

You can use the [php-curl-class](https://github.com/php-curl-class/php-curl-class) library to fetch the HTML of the validation page, or alternatively, use cURL or `file_get_contents()`:

```php
$url = 'http://nihao.rf.gd/'; // Replace with your target URL

// Initialize cURL
$curl = new Curl();
$curl->setUserAgent('Mozilla/5.0 (iPad; U; CPU OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5');
$curl->get($url);

// Handle potential errors
if ($curl->error) {
    die('Error: ' . $curl->errorMessage);
}

// Store the HTML response
$html = $curl->response; // Ensure that $html contains the HTML of the validation page.
```

### 3. Extract the Cookie Value

With just two lines of code, you can extract the test cookie value:

```php
$abc = parseabc($html);
$value = getTestCookieValue($abc[0], $abc[1], $abc[2]);
```

### 4. Set the Test Cookie and Send the Request

Now, set the cookie named `__test` with the value of `$value`, and send another request to verify if the bypass is successful:

```php
$curl->setCookies(array(
  '__test' => $value
));

$curl->get($url);
// Further actions...
```

## Acknowledgements

Special thanks to [slowaAES](https://github.com/octopius/slowaes) for their contributions.