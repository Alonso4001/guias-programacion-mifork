<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Herencia". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones y Composición.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
Tema 4.2. Herencia
1. ¿Qué es la herencia y "A es-un B"?
La herencia permite crear clases basadas en otras ya existentes. La relación "es-un" significa que una subclase es una versión especializada de la superclase. Esto implica compatibilidad de tipos (un Artillero puede usarse donde se pida un Soldado) y herencia de estado/comportamiento (la subclase recibe los atributos y métodos del padre).

Java
// Ejemplo resumido
Soldado[] ejercito = { new Artillero("Rafa", 5), new Zapador("Luis", 10) };
for (Soldado s : ejercito) s.saludar(); 
2. Constructores y super
Al instanciar una subclase, se ejecutan los constructores en cadena desde la superclase hasta la subclase. Se usa super(...) para llamar al constructor del padre, siendo obligatorio si el padre no tiene un constructor vacío.

3. Atributos privados en memoria
Los atributos privados del padre sí ocupan espacio en la memoria del objeto hijo. Sin embargo, no son accesibles directamente por nombre; la subclase debe usar métodos públicos o protegidos del padre para interactuar con ellos.

4. Extensibilidad
La herencia permite que el sistema crezca sin modificar código antiguo. Si mañana creas un Medico, el código que gestiona el array de Soldado seguirá funcionando sin cambios porque el nuevo tipo es compatible.

5. Castings e instanceof
El Upcasting (de hijo a padre) es automático. El Downcasting (de padre a hijo) requiere un moldeado manual (Tipo). Se usa instanceof antes de un downcasting para evitar que el programa falle si el objeto no es del tipo esperado.

6. Acceso protected
El modificador protected permite que los miembros sean visibles para la propia clase, sus subclases y las clases del mismo paquete. Es el equilibrio entre el private total y el public abierto.

7. Clase Object
En Java, toda clase hereda de Object si no se especifica otra cosa. Esto asegura que cualquier objeto tenga métodos base como toString() o equals().

8. Herencia múltiple
Java no permite herencia múltiple de clases para evitar conflictos de nombres y lógica. Esta necesidad se cubre mediante el uso de interfaces.

9. Excepciones personalizadas
Al ser objetos, puedes crear excepciones propias extendiendo RuntimeException.

Java
public class UsuarioNoEncontradoException extends RuntimeException {
    private Usuario usuario;
    public UsuarioNoEncontradoException(Usuario u, Throwable causa) {
        super("Error: " + u.getNombre(), causa);
        this.usuario = u;
    }
}
10, 11 y 12. Herencia vs. Composición
Se debe evitar la herencia solo para ahorrar código porque genera un acoplamiento rígido (clase base frágil). Se prefiere la composición porque es más flexible y no rompe la encapsulación, ya que no depende de los detalles internos del padre.

13. Ejemplo: Persona vs. DatosPersonales
Herencia: Estudiante extends Persona. El estudiante es una persona.
Composición: Estudiante tiene un atributo DatosPersonales. El estudiante tiene datos. La composición es más limpia si los datos personales pueden cambiar de estructura sin afectar la lógica del estudiante.