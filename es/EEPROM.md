Memoria programable de s�lo lectura(EEPROM )
=======

El robot Erle est� equipado con una sola **CAT24C256W** EEPROM para permitir que el software pueda identificar la tarjeta.

| Nombre | Tama�o ( bytes) | Contenido |
| ----- | ------------- | ---------- |
| Cabecera | 4 | ` 0xAA `, ` 0x55 `, ` 0x33 `, ` 0xEE son ` |
| Nombre de la tarjeta | 8 | Nombre para la tarjeta en **ASCII**: ` A335BONE ` |
| Versi�n | 4 | C�digo Versi�n de hardware para la tarjeta en **ASCII**: ` � 00A� � 3 ` para Rev A3, ` 00A4 ` para Rev A4, ` 00A5 ` para Rev A5, ` 00A6 ` para Rev A6 |
| N�mero de serie | 12 | N�mero de serie de la placa. 12 cadena de caracteres ASCII es ** ** con el siguiente esquema: ` WWYY4P16nnnn ` , donde ` WW ` es una semana de 2 d�gitos del a�o de fabricaci�n, ` YY ' se corresponde con el a�o de fabricaci�n, ` ` nnnn es un tablero de incrementar n�mero. |
| La opci�n de configuraci�n | 32 | ** ASCII **: ` 0000000000000000000000000000000 ` ( 64 0s en hexadecimal) |
| RSVD | 6 | ** ASCII **: ` 000.000 ` |
| RSVD | 6 | ** ASCII **: ` 000.000 ` |
| RSVD | 6 | ** ASCII **: ` 000.000 ` |
| Seguridad | 20 | protecci�n de robo de la Junta |
| Disponible | 32682 | Disponible para otro c�digo / datos no vol�til |