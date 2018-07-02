# Códigos


`Este código es un ejemplo`


```sh
#!/bin/bash

if [ $# -ne 1 ]; then 
                echo "Número de argumentos no validos, sólo se permite 1" 
                exit 1
        fi


if [ -f $1 ] && [ -n $1 ]; then
                echo -e "Todo OK"

        else
                echo -e "Error en el fitxer, no existeix o està buit"
                exit 1;
        fi

for x in $(cat $1); do
			url=$x
			code=$(curl -IL --silent  $url --write-out %{http_code} --output /dev/null)
			if [ $code -eq 200 ]; then 
				echo "Pagina $url funcionado! Code 200"
			elif [ $code -eq 404 ]; then
				echo "Página $url no funcionando! Error 404, archivo no encontrado"
			elif [ $code -eq 302 ]; then
				echo "Página $url funcionando en HTTP! Code 302"
			elif [ $code -eq 301 ]; then
				echo "Página $url movida permanentemente! Code 301"
			else
				echo "Pagina no funcionando"

			fi
		done
```
