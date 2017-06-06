## Apache AB


``` bash
# iniciar servidor
$ rackup -s webrick -p 4567

# probar primero con un request y un hilo
$ ab -n 1 -c 1 http://localhost:4567/ping

# probar con mas concurrencia que requests
$ ab -n 1 -c 2 http://localhost:4567/ping
# => ab: Cannot use concurrency level greater than total number of requests

# probar con 1000 requests concurrentes
$ ab -n 1000 -c 100 http://localhost:4567/ping

#              min  mean[+/-sd] median   max
# Connect:        0    0   0.9      0       4
# Processing:    23  197  33.1    200     330
# Waiting:       17  195  34.3    198     330
# Total:         26  197  32.5    200     330

$ rackup -s puma -p 4567

$ ab -n 1000 -c 100 http://localhost:4567/ping
#               min  mean[+/-sd] median   max
# Connect:        0    1   1.6      0       8
# Processing:    48   97  22.7     91     215
# Waiting:       45   94  22.3     88     204
# Total:         55   98  23.3     92     218

# instalar thin
$ gem install thin
$ rackup -s thin -p 4567

$ ab -n 1000 -c 100 http://localhost:4567/ping
# Connection Times (ms)
#               min  mean[+/-sd] median   max
# Connect:        0    1   1.4      0       7
# Processing:    48   64   9.3     60     110
# Waiting:       36   58   9.2     54     104
# Total:         53   64  10.0     60     113

$ puma -p 4567 -w 4

# Connection Times (ms)
#              min  mean[+/-sd] median   max
# Connect:        0    4   4.1      3      23
# Processing:     1   19  10.2     17      54
# Waiting:        1   13   8.1     11      37
# Total:          1   24  10.5     21      61


# probar matar que pasa si matás uno de los procesos
$ kill ...
#
# starting server
# [12711] - Worker 3 (pid: 12984) booted, phase: 0

# ahora repetir para una nueva ruta: fibo?n=, donde n es un número "pesado" para tu máquina 30-37.
# Comparar en particular thin vs puma non-clustered.
# Usar la configuración  puma -p 4567 -w 4 -t 10:10 (hacerlo usando rackup vs puma directamente)

# finalmente, repetir con la ruta de hit
# usar menos requests y menos concurrencia.
# Prestar atención a la tasa de errores. Comparar resultados de
#
#    * puma non-clustered y puma clustered.
#    * puma non-clustered y thin.
#
# sacar conclusiones. Mirar https://github.com/igrigorik/em-http-request
```

## Siege

Mirar https://www.joedog.org/siege-manual/