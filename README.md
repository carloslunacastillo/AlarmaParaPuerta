# AlarmaParaPuerta

***
## Indice 
+ [descripcion del programa](#descripcion)
+ [circuito en digital](#circuito)    
+ [codigo en arduino](#codigo)
+ [Contacto](#contacto)
***
## Descripcion   
Alarma para puerta con reducción en el consumo de energía y temporizador 

 Programa que simula una alarma para intrusos, cuándo la puerta se abre emite un sonido que es la alarma.
 Como requisito, se reduce el consumo de energía al mínimo. Mientras la alarma no esté sonando el
 arduino deberá consumir la mínima cantidad de energía.
 Cuando la puerta se cierre esta deberá de dejar de sonar y regresar al estado de bajo  
 consumo energético. 
 
 Adicionalmente, se agregó un método que funciona como temporizador: la alarma sonará por 5 segundos, descansará 4 segundos 
 y si la puerta sigue abierta, volverá a sonar, y si está cerrada, ya no sonará.
 
 Nota: se hará uso de un imán para simular la puerta.

Material utilizado:

•	1 LED

•	9 resistores delimitadores de 3300 Ω

•	1 Buzzer

•	1 Display de 7 segmentos

•	1 Reed switch

•	cables macho - macho (20 aproximadamente)

•	1 protoboard

•	1 placa Arduino

***
## circuito 
![circuito](Diagrama.png)
***
## codigo 
~~~

/*
 created by Carlos Leonardo Luna Castillo
 27/sep/2018
 
 */

#include <LowPower.h>     //Inclusión de la librería LowPower para el ahorro de energía  

int alarma = 13;            //Declaración del pin de la bocina
int frecuencia = 120;       //Declaración de la frecuencia que emitirá el pitido de la bocina
int puerta=2;               //Se declara el pin del reed switch que va recivir  el estado de la puerta 
int led=3;                  //Se declara el pin del led que indicará cuándo la alarma está activa

void setup(){   
  
  pinMode(6,OUTPUT);         //Definición de salida para el display en el pin 6
  pinMode(7,OUTPUT);         //Definición de salida para el display en el pin 7
  pinMode(8,OUTPUT);         //Definición de salida para el display en el pin 8
  pinMode(9,OUTPUT);         //Definición de salida para el display en el pin 9
  pinMode(10,OUTPUT);        //Definición de salida para el display en el pin 10
  pinMode(11,OUTPUT);        //Definición de salida para el display en el pin 11
  pinMode(12,OUTPUT);        //Definición de salida para el display en el pin 12  
  pinMode(puerta,INPUT);     //Definición de entrada para el reed switch que está definido en el pin 2        
  pinMode(led,OUTPUT);       //Definición de salida para el led que está definido en el pin 3
  pinMode(alarma,OUTPUT);    //Definición de salida para el buzzer que está definido en el pin 13
  
}                             

/*Metodo para despligue en Display de 7 segmentos, según las
señales que se le manden. Se unen los pines del arduino a su 
respectiva variable*/

void display (int a,int b,int c,int d,int e,int f,int g){ 
  digitalWrite(6,a);                                       
  digitalWrite(7,b);                                      
  digitalWrite(8,c);                                     
  digitalWrite(9,d);                                     
  digitalWrite(10,e);                                     
  digitalWrite(11,f);                                     
  digitalWrite(12,g);                                     
}                                                        

void loop(){           

  /*Implementación del método sleep para el ahorro de energía, el primer 
    parametro es el tiempo que dura en apagar los convertidores de analógico a digital,
    en este caso son 4 segundos.*/
   
  LowPower.powerDown(SLEEP_4S, ADC_OFF, BOD_OFF);
       
      if(digitalRead(puerta)==HIGH){                //Ciclo if para activar la alarma cuando la puerta esté abierta
         digitalWrite(led,HIGH);                    //Si la puerta está abierta, se enciende el led
         tone(alarma,frecuencia);                   //Al mismo tiempo, se activa la bocina con la frecuencia definida
          display(1,0,0,0,1,0,0);                   //Combinación de parámetos para formar el número 5 en el display e iniciar la cuenta regresiva 
          delay(1000);                              //Retraso de un segundo para el número 5
          display(0,1,0,0,0,1,1);                   //Combinación de parámetos para formar el número 4 en el display 
          delay(1000);                              //Retraso de un segundo para el número 4
          display(0,0,1,0,1,0,0);                   //Combinación de parámetos para formar el número 3 en el display 
          delay(1000);                              //Retraso de un segundo para el número 3
          display(0,0,1,0,0,0,1);                   //Combinación de parámetos para formar el número 2 en el display
          delay(1000);                              //Retraso de un segundo para el número 2
          display(0,1,1,1,1,1,0);                   //Combinación de parámetos para formar el número 1 en el display
          delay(1000);                              //Retraso de un segundo para el número 1
          noTone(buzzer);                           //Ordena a la bocina que deje de emitir el pitido 
      }                                             
      digitalWrite(led,LOW);                        //Se apaga el led de la alarma
}                                                     

~~~


## contacto
~~~

Elaborado por: Carlos Leonardo Luna Castillo
correo: carl_dharius@hotmail.com


~~~


