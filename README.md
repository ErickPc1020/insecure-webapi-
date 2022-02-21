# insecure-webapi-
Tópicos de Ciberseguridad 

						--Parche Acceso a db.json--

El parche de esta vulnerabilidad consiste en modificar de la expresión regular que contiene el archivo .htaccess agregándole la extensión “json” después de la extensión “php” tal como lo podemos observar en las siguientes líneas de código: 

						--Dirección de .htaccess:--

/var/www/html/wapp$ cat .htaccess

						--Expresión .htaccess original:--

Enable rewrite engine and route requests to framework
RewriteEngine On

Some servers require you to specify the `RewriteBase` directive
In such cases, it should be the path (relative to the document root)
containing this .htaccess file

RewriteRule ^(lib|tmp)\/|\.(ini|php)$ - [R=404]

RewriteCond %{REQUEST_FILENAME} !-l
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule .* index.php [END,QSA]
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization},L]

						--Expresión .htaccess modificada--

Enable rewrite engine and route requests to framework
RewriteEngine On

Some servers require you to specify the `RewriteBase` directive
In such cases, it should be the path (relative to the document root)
containing this .htaccess file

RewriteRule ^(lib|tmp)\/|\.(ini|php|json)$ - [R=404]

RewriteCond %{REQUEST_FILENAME} !-l
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule .* index.php [END,QSA]
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization},L]

							--Paso Final:--

Una vez realizada la modificación de la expresión se guardan los cambios y finalmente se reinicia el servicio utilizando el siguiente comando “sudo systemctl restart apache2”.

