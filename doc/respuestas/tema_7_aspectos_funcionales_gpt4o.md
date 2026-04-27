<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Aspectos funcionales". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: clases y objetos, encapsulación, excepciones, composición, herencia, polimorfismo y genericidad.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

TEMA 7. Aspectos funcionales
1. ¿Qué es un puntero a una función? Pon un ejemplo de código en C, donde se define una función y que reciba una cadena de caracteres como parámetro y devuelva la cadena en mayúsculas. Crea un puntero en una variable local a dicha función llamado aMayusculas e invócala con el puntero.
Respuesta
Un puntero a función es una variable que almacena la dirección de memoria de un bloque de código ejecutable. En C, se declara especificando el tipo de retorno y los argumentos: char* (*aMayusculas)(char*) = funcionReal;. Permite invocar la función indirectamente, facilitando la creación de código flexible y callbacks.

2. ¿Qué es una función lambda en un lenguaje de programación? Pon un ejemplo similar al anterior en Javascript y otro en Java con funciones lambda. Usa una variable local aMayusculas para apuntar a la función lambda. Por simplicidad, en Java, emplea Function<String, String> para el tipo de la referencia a la función lambda.
Respuesta
Una función lambda es una función anónima definida en línea que puede tratarse como una variable. En JS se usa const aMayus = s => s.toUpperCase(); y en Java Function<String, String> aMayus = s -> s.toUpperCase();. Ambas omiten el nombre de la función para priorizar la lógica como un dato.

3. ¿Qué es el paradigma funcional? ¿Por qué a algunos lenguajes orientados a objetos como Java 8, se les llama multi-paradigma? ¿Qué quiere decir que las funciones son "ciudadanos de primera clase"?
Respuesta
El paradigma funcional se basa en funciones puras que evitan la mutabilidad y el estado compartido. Java 8 es multi-paradigma porque permite combinar POO con técnicas funcionales. Que las funciones sean "ciudadanos de primera clase" significa que pueden asignarse a variables, pasarse como parámetros o devolverse como resultados.

4. Explica la sintaxis básica de una función lambda en Java.
Respuesta
La sintaxis se compone de: parámetros, el operador flecha -> y el cuerpo. Ejemplo: (s) -> s.toUpperCase(). Si solo hay un parámetro se pueden omitir los paréntesis; si el cuerpo es una sola instrucción, no requiere llaves {} ni la palabra reservada return.

5. Ahora recibamos una función como parámetro a un método y la llamaremos desde dentro. Amplia los ejemplos anteriores de Java y JavaScript con un método llamado transformar, que reciba un String como parámetro y luego una función transformadora como lo es aMayúsculas y la invoque desde dentro.
Respuesta
En Java: void transformar(String s, Function<String, String> f) { System.out.println(f.apply(s)); }. En JS: function transformar(s, f) { console.log(f(s)); }. En ambos casos, el método delega la lógica de procesamiento a la función recibida, aumentando la reutilización del código.

6. Ahora, invoca transformar, con una nueva función lambda directamente en la llamada a transformar, por ejemplo, una función lambda que invierta la cadena. Define la función de inversión justo cuando la estás pasando como parámetro.
Respuesta
Se pasa la lógica en el momento de la llamada: transformar("Hola", s -> new StringBuilder(s).reverse().toString());. Esto evita declarar variables previas y permite inyectar comportamientos ad-hoc (como la inversión de texto) de forma extremadamente compacta y legible.

7. ¿Qué se entiende por cierre o "closure" en el contexto de las funciones lambda? Pon un ejemplo en Java de cómo una función lambda es capaz de acceder a una variable local en el contexto donde fue definida. Modifica el ejemplo anterior, creando otra función lambda para transformar una cadena, pero que lo que haga es concatenar a la cadena de entrada otra cadena que está en una variable local definida fuera de la función lambda.
Respuesta
Un closure es la capacidad de una lambda de capturar y acceder a variables de su entorno exterior. En Java, la variable externa debe ser final o "efectivamente final". Ejemplo: String sufijo = "!"; transformar("Hola", s -> s + sufijo);. La lambda "recuerda" el valor de sufijo incluso si se ejecuta en otro contexto.

8. Reflexiona: ¿en qué se diferencia entonces una función lambda de los punteros a funciones que hay en C?
Respuesta
A diferencia de los punteros de C, que son simples direcciones de memoria, las lambdas en Java son objetos que gestionan su propio estado (clausuras). Java ofrece seguridad de tipos y gestión de memoria automática (GC), mientras que en C el programador debe asegurar manualmente que la dirección sea válida.

9. Devolvamos ahora funciones. Creemos ahora una función que sea capaz de crear funciones "descuento". Una función "descuento", decrementa un porcentaje pasado como parámetro. Por simplicidad, usa Function<Double, Double> para su tipo. La función crearDescuento(porcentaje), recibe solo el porcentaje de descuento a aplicar y devuelve la función de descuento. Prueba a crear dos descuentos distintos y aplicarlos a una cantidad. Explica la closure en la función descuento.
Respuesta
Function<Double, Double> crearDescuento(double p) { return cant -> cant * (1 - p/100); }. La closure permite que la función devuelta retenga el valor de p original. Al llamar a desc10.apply(100), la lambda usa el 10% capturado previamente, aunque la función creadora ya haya finalizado.

10. En Java, que es un lenguaje con comprobación estática de tipos, donde los tipos se declaran, toda función lambda tiene un tipo, que se conoce como interfaz funcional. ¿Qué es una interfaz funcional? ¿Qué requisitos tiene?
Respuesta
Es una interfaz que tiene exactamente un único método abstracto (SAM - Single Abstract Method). Puede contener métodos default o static, pero solo uno por implementar. Se identifica con la anotación opcional @FunctionalInterface para garantizar que sea compatible con expresiones lambda.

11. Creemos una interfaz funcional a mano. Por ejemplo, define la interfaz funcional del ejemplo que transforma la cadena en otra. Llámale Transformador, que define una función que convierte una cadena de texto (String) en otra (String).
Respuesta
Java
@FunctionalInterface
public interface Transformador {
    String ejecutar(String s);
}
// Uso: Transformador t = s -> s.toUpperCase();
Esta interfaz define el contrato mínimo para procesar textos, permitiendo que cualquier lambda que reciba y devuelva un String sea asignada a este tipo.

12. Ahora hagamos la interfaz funcional algo más genérica y empleando generics, para que permita definir un Transformador de un tipo en otro. Pon un ejemplo de un transformador que redondea un Double en un Integer.
Respuesta
Java
@FunctionalInterface
public interface TransformadorGen<T, R> {
    R ejecutar(T t);
}
// Redondeo: TransformadorGen<Double, Integer> r = d -> (int) Math.round(d);
El uso de genéricos <T, R> permite que la misma interfaz sirva para cualquier conversión de tipos, como pasar de un valor numérico real a uno entero.

13. Transformador, en su versión genérica, parece muy útil y reutilizable, hasta el punto de que es igual a una interfaz funcional que ya hay, que es Function<T, R>. Muestra las interfaces funcionales predefinidas que hay en Java.
Respuesta
Java ofrece: Function<T, R> (entrada T, salida R), Predicate<T> (entrada T, salida boolean), Consumer<T> (entrada T, sin salida) y Supplier<T> (sin entrada, salida T). Estas interfaces cubren los flujos de datos más comunes en el paradigma funcional de Java.

14. Vamos a ver ejemplos expresivos de funcional en Java. Estudiemos el List.forEach, como versión funcional del bucle for. Emplea el forEach para recorrer una lista de Integer y que muestre un mensaje si el entero es positivo.
Respuesta
Java
lista.forEach(n -> { if (n > 0) System.out.println("Positivo: " + n); });
El método forEach aplica una lambda de tipo Consumer a cada elemento. Es más expresivo que un for tradicional porque describe "qué" hacer con cada elemento en lugar de gestionar el índice o el iterador.

15. Repasando el tema de genericidad, fíjate en la firma de forEach, ¿por qué se usa Consumer<? super T> y no Consumer? Explica qué significa PECS, y explícalo para el caso de mejorar el ejemplo del método transformar la hora de definir el tipo de la función transformadora.
Respuesta
Se usa ? super T siguiendo la regla PECS (Producer Extends, Consumer Super): si vas a consumir datos, usa super para aceptar tipos más generales. En transformar, Function<? super T, ? extends R> permite que la función acepte un tipo padre de la entrada y devuelva un hijo del resultado esperado.

16. Referencias a métodos. Podemos obtener una referencia a métodos de objetos o clases. Pon un ejemplo en JavaScript y en Java, de una clase Persona con un método saludar. En el código principal, crea una Persona con un nombre, y obtén una referencia a su método saludar en una variable local. Invoca saludar con esa referencia a su método saludar.
Respuesta
En Java: Persona p = new Persona("Ana"); Runnable ref = p::saludar; ref.run();. En JS: const p = new Persona("Ana"); const ref = p.saludar.bind(p); ref();. Las referencias a métodos permiten apuntar directamente a una implementación existente sin envolverla en una lambda redundante.

17. ¿Qué tipos de referencias a método se pueden hacer en Java? Pon un ejemplo de referencia a método estático, a constructor, a método de instancia de una instancia concreta y a método de instancia sobre cualquier instancia.
Respuesta
Estático: Math::abs. 2. Constructor: ArrayList::new. 3. Instancia concreta: miObjeto::toString. 4. Instancia arbitraria de un tipo: String::toUpperCase. Estas cuatro variantes permiten reutilizar cualquier lógica previa como si fuera una función lambda.

18. Ordena una lista de Persona, cada persona tiene un nombre y una edad (de tipo entero). Ordena la lista de Persona con Collections.sort, pasándole como comparador una expresión lambda que compare la edad de ambas personas y si tienen la misma edad, se ordene por orden alfabético del nombre. Crea dos versiones: Una con la función de comparación hecha manualmente, y otra empleando Comparator.
Respuesta
Manual: Collections.sort(l, (p1, p2) -> p1.edad != p2.edad ? p1.edad - p2.edad : p1.nombre.compareTo(p2.nombre));.
Con Comparator: l.sort(Comparator.comparingInt(Persona::getEdad).thenComparing(Persona::getNombre));. La segunda versión es más legible, modular y evita errores en la lógica de comparación manual.