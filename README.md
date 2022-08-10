# PRUEBAS TX LoRa 
Resultados de pruebas de recepción y transmisión del modo LoRa en una estacion TinyGS

## Transmisión de packet de prueba
Se transmite un test packet tipeando "**p**" en la consola TinyGS. La respuesta en consola es la siguiente:

![image](https://user-images.githubusercontent.com/25980890/184034919-c73050dd-d8cf-4331-acfd-953e83e01a2b.png)

La transmisión es captada via **GNU Radio** y grabada como un archivo **IQ(float32)**. Se retransmite en la misma frecuencia utilizando un **LimeSDR-Mini**.
La transmisión es recibida en la consola TinyGS de la siguiente manera:

![image](https://user-images.githubusercontent.com/25980890/184036771-7c7d9baa-0171-478d-9a38-b17e9f2faf62.png)

Los bytes recibidos **54696e7947532d7465737420** corresponden a la expresión *HEX* de los carácteres ASCII "**TinyGS-test**".
Al mismo, tiempo, se recibe un mensaje del **TinyGS Personal Bot** anunciando la recepción de packets de prueba:

![image](https://user-images.githubusercontent.com/25980890/184039503-434abb17-e8e3-4a29-8322-03c29b5992e3.png)


Aparte del aviso del **TinyGS Personal Bot**, el packet de prueba aparece ahora en la página web de la estación TinyGS **Santiago_CE3SNA**
![image](https://user-images.githubusercontent.com/25980890/184039293-b9a2f83c-efae-47f1-964a-be25f8e64c65.png)


### Intento de decodificación con software externo

Se realiza una prueba en otra frecuencia para intentar decodificar la transmisión con un programa externo, utilizando el decodificador LoRa dentro del *ChirpChat Demodulator* del software **SDRangel**. Sin embargo, solo se logra una decodificación de los primeros bytes (revisando los issues de SDRangel hay comentarios sobre situaciones similares).

![image](https://user-images.githubusercontent.com/25980890/184037337-0710ce1e-64fe-4c88-8aae-b458e6488b3f.png)





## Transmisión de packet con texto libre
Utilizando la opción de transmitir texto libre, se emite un packet con la frase "Prueba texto libre CE3SNA".
En la consola TinyGS, esta acción es indicada como se muestra abajo. Interesantemente, **UHJ1ZWJhIHRleHRvIGxpYnJlIENFM1NOQQ==** es la representación de la frase "Prueba texto libre CE3SNA" en formato **base64**

![image](https://user-images.githubusercontent.com/25980890/184037804-6675c69a-fcf1-443c-bb9c-6d1688ea2f68.png)

Al igual que la transmisión del packet de prueba, esta transmisión fue grabada como archivo **IQ(float32)**. Al retransmitir este archivo, la decodificación en **SDRangel** es parcial (sólo 3 carácteres), lo que indicaría una posible deficiencia en la sincronización de decodificado:

![image](https://user-images.githubusercontent.com/25980890/184038696-97421b8f-a641-4d72-baa5-4d948a3e703e.png)

Sin embargo, en la consola TinyGS, la transmisión es recibida exitosamente:

![image](https://user-images.githubusercontent.com/25980890/184038879-a8bcfe2e-8f72-420b-ade1-de72212d707a.png)

Los bytes recibidos **50727565626120746578746f206c6962726520434533534e41** son la representación *HEX* del string original "Prueba texto libre CE3SNA".

La recepción de estos bytes no genera un aviso por parte del **TinyGS Personal Bot**, ni se refleja en la página web de la estación
