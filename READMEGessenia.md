
En `JavaScript`, hay dos tipos de alcance:

* **`ámbito local`** 
* **`Alcance global`**

Recordemos que cada función crea un nuevo ámbito.

El ámbito de aplicación determina la accesibilidad (visibilidad) de estas variables, como por ejemplo las variables definidas dentro de una función no son accesibles (visible) desde fuera de la función.


## FUNCTIONS and SCOPE

Asignamos el evento al documento `html` en el **ambiente lexical global** para que cuando la página haya terminado de cargar correctamente se ejecute la función anónima o huerfana que se le dió como parámetro al evento ready.

```js
$(document).ready(function() {
```
Posteriormente se ejecutará el comando en la consola

```js
console.log('Probar con el número valido 4544164785372342');
```
Esto mostrará un número válido de tarjeta de crédito.

Posteriormente, declaramos las variables en el **ambiente lexical local**:

```js
 var $inputCard = $('#card-number');
 var $inputMonth = $('.input-month');
 var $inputYear = $('.input-year');
 var $buttonNext = $('#next');
 var regexOnlyNumbers = /^[0-9]+$/;
 var labelErrorOrSuccessMessages = $('label[for="card-number"]');
```

Asignaremos el evento  a la **variable local** que nos permita capturar el input del usuario

```js
$inputCard.on('input', function() {

  });
```
Declaramos una **función de ambito local** que habilita el boton del formulario:
```js
function activeButton() {
    $buttonNext.attr('disabled', false);
  }
 ```

Declaramos una **función de ambito local** que desabilita el boton del formulario:
```js
  function desactiveButton() {  
    $buttonNext.attr('disabled', true);
  } 
```
Declaramos una **función de ambito local** que valida la longitud del input ingresado por el usuario:
```js
  function longitud(input) {
    if (input.trim().length === 16) {
      return input;
    }
  }
  ```

Declaramos una **función de ambito local** que valida el ingreso de solo números, input ingresado por el usuario
```js
  function soloNumeros(input) {
    var regex = /^[0-9]+$/;
    if (regex.test(input)) {
      return input;
    }
  }
  ```
 Declaramos una **función de ambito local** que valida que el número ingresado sea una un número de tarjeta valido.

 ```js
  function isValidCreditCard(numberCard) {
    var creditCardNumber = soloNumeros(longitud(numberCard));
    if (creditCardNumber !== undefined) {
      var arr = [];
      var sumaTotal = 0;
      for (var index = creditCardNumber.length - 1; index >= 0; index--) {
        arr.push(creditCardNumber[index]);
      }
      for (var index = 1; index < arr.length; index = index + 2) {
        arr[index] = arr[index] * 2;
        if (arr[index] >= 10) {
          arr[index] = arr[index] - 9;
        }    
      }
     
      for (var index = 0; index < arr.length; index++) {
        sumaTotal = sumaTotal + parseInt(arr[index]);
      }
     
      if (sumaTotal % 10 === 0) {
        console.log('Es una tarjeta valida');
        activeButton();
      } else {
        console.log('No es un numero valido');
        desactiveButton();
      }
    } else {
      console.log('Verifique el numero de su tarjeta'); 
      desactiveButton();  
    }
  }
});
 ```

 ### Autor:
 Gessenia Canales