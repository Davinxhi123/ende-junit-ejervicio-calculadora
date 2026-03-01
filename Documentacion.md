### 1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?
Es un proyecto que sirve como ejemplo básico para aprender y practicar cómo probar automáticamente que un código en Java funciona bien mediante las pruebas.

### 2. Revisa las pruebas de la suma y comenta lo que te parezca de interés
Lo que me parece más interesante es el hecho de poder cambiar el resultado esperado para comprobar que se produce un error en la prueba que se decida realizar.

### 3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.
- En este caso tenemos dos entradas (dividendo y dividor) y una salida que es el resultado de la division.
- Determinar clases equivalentes:
   - Dividendo: todos los números son válidos.
   - Divisor: todos los números son válidos menos el 0; el 0 no es válido.
- Valores límites: (cada entrada tiene unos valores limites distintos)
   - Dividendo (D1): 
      - -infinito: valor mínimo.
      - +infinito: valor máximo.
      - Válidas: D1 < 0 | D1 > 0 | D1 = 0
   - Divisor (D2):
      - -infinito: valor mínimo.
      - 0: valor intermedio pero no valido
      - +infinito: valor máximo.
      - Válidas: D2 < 0 | D2 > 0
      - No Válidas: D2 = 0 
   - Conjetura de errores: comprobaremos que cuando el divisor sea 0 dará error.
- Casos de pruebas: (aplicando los limites para cubrir todos los casos)
    | Caso de Prueba | Dividendo | Divisor | Salida |
    | - | - | - | - |
    | CP1 | 4 | 2 | 2 |
    | CP2 | -6 | -3 | 2 |
    | CP3 | 4 | -4 | -1 |
    | CP4 | -8 | 4 | -2 |
    | CP5 | 0 | 4 | 0 |
    | CP6 | 0 | -2 | 0 |
    | CP7 | 7 | 0 | ERROR |
    | CP8 | -3 | 0 | ERROR |
    | CP9 | 0 | 0 | ERROR |

##### Implementación en junit:
```java
@Test
    void dividirPositivos() {
        int valor1 = 4;
        int valor2 = 2;
        int esperado = 2;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirNegativos() {
        int valor1 = -6;
        int valor2 = -3;
        int esperado = 2;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirPositivoNegativo() {
        int valor1 = 4;
        int valor2 = -4;
        int esperado = -1;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirNegativoPositivo() {
        int valor1 = -8;
        int valor2 = 4;
        int esperado = -2;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirCeroEntrePositivo() {
        int valor1 = 0;
        int valor2 = 4;
        int esperado = 0;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirCeroEntreNegativo() {
        int valor1 = 0;
        int valor2 = -2;
        int esperado = 0;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }
    
    @Test
    void dividirEntreCero() {
        int valor1 = 7;
        int valor2 = 0;

        assertThrows(OperacionNoValidaException.class, () -> {
         Calculadora.dividir(valor1, valor2);
      });
    }

    @Test
    void dividirNegativoEntreCero() {
        int valor1 = -3;
        int valor2 = 0;

        assertThrows(OperacionNoValidaException.class, () -> {
         Calculadora.dividir(valor1, valor2);
      });
    }

    @Test
    void dividirCeroEntreCero() {
        int valor1 = 0;
        int valor2 = 0;

        assertThrows(OperacionNoValidaException.class, () -> {
         Calculadora.dividir(valor1, valor2);
      });
    }
```