<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Genericidad". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: clases y objetos, encapsulación, excepciones, composición, herencia y polimorfismo.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
TEMA 6. Genericidad
1. Estructura con void* u Object
En C se usa void* para que un array almacene punteros a cualquier tipo, requiriendo casting manual. En Java, un Object[] permite guardar cualquier instancia porque todas heredan de Object, pero se pierde la información del tipo real al recuperar el dato.

2. Programación genérica
Es un paradigma que permite escribir código independiente del tipo de dato específico. El uso de Object es un ejemplo básico de genericidad por polimorfismo, pero no es óptimo porque no ofrece seguridad de tipos en tiempo de compilación.

3. Problemas de chequeo
El uso de void* u Object traslada los errores al tiempo de ejecución (como ClassCastException). El compilador no puede verificar qué se guarda, obligando a realizar "downcastings" manuales que ensucian el código y facilitan la aparición de bugs.

4. Parámetros de tipo
Son marcadores (como <T>) que representan un tipo que se definirá al instanciar la clase. Permiten que el compilador verifique la consistencia, asegurando que solo se introduzcan y extraigan objetos del tipo declarado sin necesidad de casts.

5. Ejemplo Java vs C++
En C++ se usa std::vector<std::string> y en Java ArrayList<String>. Ambos permiten añadir y recuperar cadenas con seguridad, pero C++ genera código nuevo para cada tipo (plantillas) mientras que Java reutiliza el mismo código para todos.

6. Type Erasure vs Instanciación
C++ crea una copia física de la clase por cada tipo usado. Java usa Type Erasure: el compilador elimina los genéricos tras verificar los tipos y los sustituye por Object en el bytecode, manteniendo un único archivo .class para ahorrar espacio.

7. Clase Par<T, U>
Java
public class Par<T, U> {
    private T primero; private U segundo;
    public Par(T t, U u) { primero = t; segundo = u; }
    public T getPrimero() { return primero; }
}
Se usa para devolver dos valores de distinto tipo en un solo objeto, como Par<Double, Double> para una media y su desviación.

8. Método seleccionaUno
Un método genérico <T> garantiza que los argumentos y el retorno sean del mismo tipo exacto. Con Object, podrías pasar un String y un Integer por error y el compilador no te avisarías, provocando un fallo al intentar usar el resultado.

9. Restricciones (extends)
<T extends Number> limita el genérico a clases que hereden de Number. Tras el Type Erasure, Java sustituye T por Number en el bytecode, permitiendo usar métodos como doubleValue() que no existen en un Object genérico.

10. Reflexión sobre Punto
La versión con <T extends Number> garantiza que todas las coordenadas de un Punto sean del mismo tipo exacto. Esto evita mezclar un Integer con un Double en el mismo objeto, algo que la solución simple con Number sí permitiría.

11. Ejemplo Punto2D/3D tipado
Al definir interface Punto<T extends Punto<T>>, el método distanciaA(T p) ya recibe el tipo correcto. Esto elimina la necesidad de usar instanceof o lanzar excepciones de ejecución, ya que el error de tipo se detecta al compilar.

12. Covarianza e Invarianza
String[] es covariante con Object[] (permitido, pero arriesgado en ejecución). List<String> es invariante respecto a List<Object> (prohibido por el compilador) para asegurar que no se inserten objetos erróneos en una colección tipada.

13. Wildcards (?)
? extends T (covarianza) sirve para leer de una lista tratándola como tipo T. ? super T (contravarianza) sirve para escribir en una lista, garantizando que esta puede aceptar objetos de tipo T o sus descendientes de forma segura.