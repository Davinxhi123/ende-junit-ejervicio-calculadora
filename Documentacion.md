### 1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?
Es un proyecto que sirve como ejemplo básico para aprender y practicar cómo probar automáticamente que un código en Java funciona bien mediante las pruebas.

### 2. Revisa las pruebas de la suma y comenta lo que te parezca de interés
Lo que me parece más interesante es el hecho de poder cambiar el resultado esperado para comprobar que se produce un error en la prueba que se decida realizar,

### 3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.
- Determinar clases equivalentes:
    - Validos: numericos positivos y negativos
    - Invalidos: no numericos
- Valores límites: 
    - -$\infty$ a +$\infty$
- Pruebas aleatorias:
    | Caso de Prueba | Resultado |
    | --------- | --------- |
    | 20 / 10 | 2 |
    | -40 / -4 | 10 |
    | -30 / 10 | -3 |
    | 10 / 0 | 0 |
    | 0 / 10 | ERROR |

##### Implementación en junit:
```java
@Test
   void dividir() {
      Assertions.assertAll("Suma", new Executable[]{() -> {
         Assertions.assertEquals(2, Calculadora.dividir(1, 4), "20 / 10 = 2");
      }, () -> {
         Assertions.assertEquals(10, Calculadora.dividir(2, 3), "(-40) / (-4) = 10");
      }, () -> {
         Assertions.assertEquals(-3, Calculadora.dividir(0, 1), "(-30) / 10 = -3");
      }, () -> {
         Assertions.assertEquals(0, Calculadora.dividir(1, -2), "10 / 0 = 0");
      }, () -> {
         Assertions.assertEquals(OperacionNoValidaException(), Calculadora.dividir(1, -2), "0 / 10 = OperacionNoValidaException()");
      }});
   }
```