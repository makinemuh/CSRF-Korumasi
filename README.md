# DemirPHP CSRF Sınıfı
CSRF açığını önlemek amacıyla geliştirilmiş belirti (token) oluşturup/kontrol eden bir PHP sınıfı

## Kullanımı
Form sayfasındayken sınıfı uygulamamıza dahil ettiğimizden ve oturumu (session) başlattığımızdan emin olduktan sonra

```php
session_start();
echo Csrf::field();
// Örnek çıktı: 
// <input type="hidden" name="csrf" value="M2I4ODRhYTkyNTI1M2RkMWFlNTlmMTVjODY2ZjE2Mzg3OWQ5MDQyMw=="> 
```
ya da şu şekilde:
```php
session_start();
$token = Csrf::token();
echo '<input type="text" name="_csrfToken" value="$token">';
```

Daha sonra, POST ettiğimiz sayfada kontrolü şu şekilde yapıyoruz:

```php
if (Csrf::check()) {
	// Doğrulama başarılı
} else {
	// Doğrulama başarısız
}

// veya
// Csrf::check($_POST['csrf']);
// ya da, girdi adı farklıysa
// Csrf::check($_POST['__csrfToken']);
// Csrf::check($token);
```

İstersek, kontrolü yapmadan önce zaman aşımını belirleyebiliyoruz. Geçerli olarak 900 saniye yani 15 dakikadır.

```php
Csrf::timeout(30*60); // 30 tane 60 saniye, 30 dakika
var_dump(Csrf::check()); // true|false
```
