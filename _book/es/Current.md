Medici�n de corriente
===========

El BEAGLEBONE tiene un m�todo seg�n el cual se puede medir el consumo de corriente de la junta, sin contar el puerto Host USB y tarjetas de expansi�n. La ca�da de tensi�n en una resistencia de 0,1 ohmios se mide para determinar el consumo de corriente.

! [actual] ( img / currentmeas.png )

Conexi�n `SYS_5V`
----------
El carril `SYS_5V` se mide para determinar la parte alta de la resistencia en serie . El carril ` SYS_5V ` est� conectado a la ` pasador ` MUX_OUT . Antes de ser conectado al segundo multiplexor interno, la tensi�n se divide por 3 . Una se�al de ` 5V ` dar� lugar a una tensi�n de 1.66V ` ` en el ` pasador ` MUX_OUT .


Conexi�n ` SYS_VOLT `
-------
El carril ` SYS_VOLT ` se mide para determinar la parte alta de la resistencia en serie . El carril ` SYS_VOLT ` est� conectado a la MUX_OUT mediante el establecimiento de los registros dentro de la TPS65217B . Las resistencias R2 ` ` y ` R1 ` se proporcionan para mantener la misma configuraci�n de divisor de tensi�n como se encuentra en el carril de ` SYS_5V ` situado interna a la TPS65217B . Sin embargo , un carril de 5V le dar� ` 1.41V ` a diferencia de la ` 1.66V ` encontraron interna a la TPS65217B . Esto se resuelve a un divisor de 2,8. Aseg�rese de trabajar esto en sus c�lculos finales .

Conexi�n ` MUX_OUT `
-------
La conexi�n ` MUX_OUT ` se divide por 2 antes de ser conectado al procesador . La raz�n de esto es que si est� conectado el voltaje de la bater�a , no tiene divisor de tensi�n internamente . Si est� conectado podr�a da�ar el procesador . Cuando el c�lculo de las tensiones para cada lado de las resistencias , que la tensi�n se divide por 2 . Aseg�rese e incluir esto en sus c�lculos .

C�lculo actual
---------
El c�lculo para el actual se basa en 0,1 mV es igual a 1 mA . Puede utilizar la siguiente f�rmula para calcular la corriente utilizando las lecturas de voltaje como le�do por el procesador.

`` `
( ( ( SYS_5V * 2 ) * 3,3 ) - ( ( SYS_VOLT * 2 ) * 3,54 ) ) ) / 0,1 = total ( mA )
`` `