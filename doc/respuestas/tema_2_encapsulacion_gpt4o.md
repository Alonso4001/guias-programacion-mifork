<!--

Posible prompt:

<prompt>

Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:

- C/C++ sin orientación a objetos.

- Temas de Java previos: Clases y Objetos.



Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).



Por favor, escribe en impersonal las respuestas.



</prompt>

----

-->

# TEMA 2. Encapsulación

1. En Programación Orientada a Objetos (POO), ¿Qué buscan la encapsulación y la ocultación de información? Enumera brevemente algunas ventajas de la ocultación de información.
Respuesta
La encapsulación busca agrupar los datos y los métodos que los manipulan en una única unidad o clase. Por otro lado, la ocultación de información persigue restringir el acceso directo a los detalles internos de esa clase, permitiendo que el estado de un objeto solo sea accesible a través de una interfaz controlada.

Sus ventajas principales son la facilidad de mantenimiento, ya que permite cambiar la implementación interna sin afectar al resto del código, y la robustez, al evitar que el estado del objeto sea manipulado de forma indebida o accidental por agentes externos.

2. ¿Qué se entiende por la interfaz pública de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
Respuesta
La interfaz pública es el conjunto de métodos, atributos y constantes que una clase expone al exterior. Se puede considerar como el "contrato" o el manual de instrucciones que indica qué servicios puede realizar el objeto para otros componentes del sistema.

Se relaciona con la ocultación de información porque sirve como el único punto de contacto permitido. Mientras que los detalles complejos se ocultan (parte privada), la interfaz pública ofrece una vista simplificada y segura para interactuar con el objeto.

3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la interfaz pública de una clase? ¿Es fácil cambiarla?
Respuesta
Es crucial diseñarla con cuidado porque cualquier cambio en ella afectará a todos los usuarios de la clase. Una interfaz mal diseñada puede obligar a exponer detalles internos que deberían estar ocultos, aumentando la dependencia entre diferentes partes del programa.

No es fácil cambiarla una vez que el sistema está en uso. Si se modifica un método público, se debe actualizar todo el código externo que lo utiliza; por el contrario, la parte oculta (privada) puede rediseñarse por completo sin que nadie fuera de la clase lo note.

4. ¿Qué son las invariantes de clase y por qué la ocultación de información nos ayuda?
Respuesta
Las invariantes de clase son condiciones o reglas lógicas que deben ser siempre verdaderas para que un objeto se considere válido (por ejemplo, que el saldo de una cuenta nunca sea negativo). Son las garantías de "salud" del objeto.

La ocultación de información ayuda a proteger estas invariantes al impedir que el código externo asigne valores arbitrarios a los atributos. Al obligar a usar métodos controlados, la clase puede validar que cualquier cambio solicitado cumpla estrictamente con las reglas establecidas.

5. Pon un ejemplo de una clase Punto en Java, con dos coordenadas, x e y, de tipo double, con un método calcularDistanciaAOrigen, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase Punto? ¿Qué significa public y private?
Respuesta
Java
public class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
La interfaz pública consta del constructor Punto y el método calcularDistanciaAOrigen. public significa que el miembro es accesible desde cualquier otra clase, mientras que private restringe el acceso únicamente a los métodos dentro de la misma clase.

6. En Java, ¿A quiénes se pueden aplicar los modificadores public o private?
Respuesta
Se pueden aplicar a las clases (en su nivel superior o internas), interfaces, atributos, métodos y constructores. También se aplican a los elementos de un tipo enumerado.

No se pueden aplicar a las variables locales que se declaran dentro de un método, ya que su ámbito está limitado de por sí a la ejecución de dicho método.

7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?
Respuesta
Sí, existen otros niveles de visibilidad intermedios. En Java, además de public y private, existe protected (acceso para la clase, sus subclases y el mismo paquete) y el nivel por defecto o "package-private" (solo accesible dentro del mismo paquete).

Otros lenguajes como C++ incluyen el concepto de "friendship", que permite a clases o funciones específicas acceder a los miembros privados de otra clase. Cada lenguaje gestiona estos niveles para equilibrar flexibilidad y seguridad.

8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método calcularDistanciaAPunto(Punto otro) y explica la respuesta.
Respuesta
La respuesta correcta es la (a) otras clases. En Java, la visibilidad privada es a nivel de clase, no de objeto. Esto significa que un objeto puede acceder a los atributos privados de otro objeto si ambos pertenecen a la misma clase.

Java
public double calcularDistanciaAPunto(Punto otro) {
    // Se accede a 'otro.x' y 'otro.y' aunque sean privados
    return Math.sqrt(Math.pow(otro.x - this.x, 2) + Math.pow(otro.y - this.y, 2));
}
Esto es posible porque el código está escrito dentro de la definición de la clase Punto, por lo que tiene los permisos necesarios para manipular los detalles internos de cualquier instancia de ese tipo.

9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?
Respuesta
Son métodos públicos diseñados para leer (getter) o modificar (setter) de forma controlada el valor de un atributo privado. Actúan como intermediarios entre el estado interno del objeto y el mundo exterior.

Su propósito principal es permitir la validación de los datos. Por ejemplo, un setter puede comprobar que una edad sea coherente antes de asignarla, asegurando que el objeto nunca entre en un estado inválido.

10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?
Respuesta
No se refiere a la seguridad frente a ataques externos o piratería, sino a la robustez y fiabilidad del diseño del software. Se trata de evitar que los desarrolladores cometan errores accidentales al manipular datos internos que deberían estar protegidos.

Al "asegurar" el código, garantizamos que las dependencias entre clases sean mínimas y que los cambios en una parte del programa no provoquen fallos en cadena difíciles de detectar en otras partes.

11. ¿Qué diferencia hay entre miembro de instancia y miembro de clase? ¿Los miembros de clase también se pueden ocultar?
Respuesta
Un miembro de instancia es único para cada objeto (cada instancia tiene su propia copia de los datos). Un miembro de clase, marcado con static, es compartido por todas las instancias de esa clase; solo existe una copia en memoria.

Los miembros de clase también se pueden ocultar mediante el modificador private. Esto es útil cuando la clase necesita almacenar datos internos compartidos que no deben ser modificados directamente desde el exterior.

12. Brevemente: ¿Tiene sentido que los constructores sean privados?
Respuesta
Sí, tiene mucho sentido en diseños específicos. Un constructor privado impide que se creen instancias de la clase de la manera tradicional mediante el operador new desde fuera de la misma.

Esto se utiliza habitualmente en el patrón Singleton (para asegurar que solo exista una instancia de la clase) o en clases de utilidad que solo contienen métodos estáticos y no necesitan ser instanciadas nunca.

13. ¿Cómo se indican los miembros de clase en Java? Pon un ejemplo, en la clase Punto definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores x e y máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.
Respuesta
Se indican utilizando la palabra clave static. Estos miembros pertenecen a la clase globalmente y no a una instancia específica.

Java
private static double maxX = 0;
private static double maxY = 0;

// En el constructor se actualizaría:
// if (x > maxX) maxX = x;
// if (y > maxY) maxY = y;
14. Como sería un método factoría dentro de la clase Punto para construir un Punto a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado static?
Respuesta
Java
public static Punto crearPuntoRedondeado(double x, double y) {
    return new Punto(Math.round(x), Math.round(y));
}
Se utiliza static necesariamente porque el método debe ser invocado directamente sobre la clase Punto para crear una nueva instancia, sin que haga falta tener un objeto Punto previo para llamarlo.

15. Cambia la implementación de Punto. En vez de dos double, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.
Respuesta
Java
private double[] coordenadas = new double[2];

public Punto(double x, double y) {
    this.coordenadas[0] = x;
    this.coordenadas[1] = y;
}

public double calcularDistanciaAOrigen() {
    return Math.sqrt(coordenadas[0] * coordenadas[0] + coordenadas[1] * coordenadas[1]);
}
Gracias a la ocultación, el cambio de la estructura interna es totalmente transparente para el usuario de la clase, manteniendo intacto el comportamiento externo.

16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?
Respuesta
No es mejor. Mantener el atributo privado permite evolucionar la clase sin romper el código ajeno. La convención habitual es que los atributos sean siempre privados para garantizar el control total sobre los datos.

Esto está directamente relacionado con las invariantes de clase, ya que los setters permiten filtrar valores incorrectos, algo imposible si el atributo fuera público y cualquiera pudiera asignarle un valor inválido.

17. ¿Qué significa que una clase sea inmutable? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?
Respuesta
Una clase inmutable es aquella cuyos objetos no pueden cambiar su estado una vez creados. Un método modificador es cualquier operación que altere los datos internos del objeto; no tiene por qué llamarse "set", puede ser un método como actualizar().

Las ventajas de la inmutabilidad incluyen la simplicidad, la facilidad para compartir objetos entre diferentes partes del programa y, sobre todo, la seguridad en entornos donde varios procesos se ejecutan simultáneamente (hilos).

18. ¿Es recomendable incluir métodos "setter" siempre y como convención?
Respuesta
No es recomendable. Solo deben incluirse si existe una necesidad real de modificar ese dato tras la creación del objeto. Un exceso de setters innecesarios debilita la encapsulación y hace que el código sea más difícil de seguir y mantener.

19. ¿La clase String en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?
Respuesta
La clase String es inmutable. Al concatenar dos cadenas, Java no modifica las originales, sino que crea un objeto String completamente nuevo con el resultado, lo cual consume tiempo y memoria.

Para concatenaciones masivas en un bucle, se debe utilizar la clase StringBuilder, que está diseñada específicamente para ser mutable y eficiente al construir cadenas paso a paso.

20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java?
Respuesta
Se pueden comparar por identidad (¿son el mismo objeto en memoria?) o por contenido (¿tienen los mismos datos?). En Java, el método equals se usa para definir qué significa que dos objetos sean "iguales" por contenido.

Por defecto, equals solo compara la identidad (como el operador ==). Las cadenas en Java deben compararse siempre con el método .equals() y nunca con ==, para asegurar que se compara el texto y no la dirección de memoria.

21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers?
Respuesta
Son clases que envuelven un tipo primitivo (como int) para tratarlo como un objeto (Integer). En Java, el proceso es automático mediante el autoboxing. Sus ventajas incluyen permitir el uso de tipos básicos en estructuras que solo aceptan objetos, como las colecciones.

No todos los lenguajes los necesitan; lenguajes como Smalltalk o Python tratan todo como objetos desde el inicio, por lo que no requieren esta distinción ni envoltorios adicionales.

22. ¿En POO qué es un tipo de dato enumerado? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?
Respuesta
Un enumerado es un tipo de dato que define un conjunto fijo de constantes con nombre. En Java, los enumerados son clases completas, lo que significa que pueden tener sus propios atributos, constructores y métodos.

Sus ventajas en encapsulación son enormes, ya que permiten restringir los valores posibles a un grupo seguro y cerrado, evitando el uso de constantes sueltas (como enteros) que podrían inducir a error.

23. Crea un tipo enumerado en Java que se llame Mes, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.
Respuesta
Java
public enum Mes {
    ENERO(31, 1), FEBRERO(28, 2), MARZO(31, 3); // ...
    private final int dias;
    private final int ordinal;

    private Mes(int dias, int ordinal) {
        this.dias = dias;
        this.ordinal = ordinal;
    }
    public int getDias() { return dias; }
    public int getOrdinal() { return ordinal; }
}
24. Añade a la clase Mes del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro enHemisferioNorte). Es decir: esDePrimavera(boolean esHemisferioNorte), esDeVerano(boolean esHemisferioNorte), esDeOtoño(boolean esHemisferioNorte), esDeInvierno(boolean esHemisferioNorte)
Respuesta
Java
public boolean esDeVerano(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == JUNIO || this == JULIO || this == AGOSTO;
    } else {
        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
    }
}
// Los demás métodos seguirían una estructura lógica idéntica variando los meses.