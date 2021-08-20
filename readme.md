# Laravel web application runner

An simple Apache based image for running Laravel application includes scheduler and queue workers.

Available variants: `frengky/laravel`, `frengky/laravel:php8`, `frengky/laravel:php7`

*Environment variables*:

| Name | Description | Example Value |
|------|-------------|---------------|
| PHP_EXT_XDEBUG | Enable XDEBUG extension | 1 |
| XDEBUG_CONFIG | [XDEBUG configuration](https://xdebug.org/docs/all_settings) | client_host=host.docker.internal |
| PHP_INI_SENDMAIL_PATH | PHP ini sendmail path | /usr/sbin/sendmail -S your-mail-host:3025 -t -i |

## Running a Laravel application
Running a php website with current directory as the document root, on port `8080`
```
docker run -it --rm -v $(pwd):/app -p 8080:8080 frengky/laravel
```

Access Laravel's artisan command
```
docker run -it --rm -v $(pwd):/app frengky/laravel php artisan route:list
```

## Debugging in Visual Code (XDEBUG)

To debugging in Visual Code Make sure the `PHP Debug` extension are installed on your remote too.
Adjust your `launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/app": "${workspaceRoot}"
            }
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9003
        }
    ]
}
```
