# Reto Final Fase 2 Modulo 2 Sesion 4

Arrow function
Buenas para funciones rápidas de una linea. 
Ejemplo : const calcAge= birthYear => 2037 - birthYear;
Su this se refiere al contexto que "envuelve a la función" referente a un this léxico.
Como característica: mantiene su contexto en todo su interior. This en su interior siempre apunta al contexto de la Arrow Function.

 This
Es tercero en el execution context. Es una variable especial que se crea para cada contexto de ejecución  (cada función).
Toma el valor de (apunta al) "propietario" de la función en la que se utiliza la palabra clave this.
esto NO es estático. Depende de cómo se llame a la función, y su valor solo se asigna cuando el
en realidad se llama a la función.

Ejemplos de this..
Method this = <Object que llama al metodo>
Simple function call :  this = undefined
Arrow functions  this = <this de función circundante (this léxico )>
Event listener   this = <DOM element al que está adjunto el handler>
