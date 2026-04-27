<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Polimorfismo". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones, Composición y Herencia.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
Tema 5. Polimorfismo
1. Polimorfismo y sobreescritura
El polimorfismo permite que una referencia de superclase ejecute métodos específicos de sus subclases según el objeto real en memoria. La sobreescritura es la técnica de redefinir un método del padre en el hijo para especializar su comportamiento manteniendo la misma firma.

2. Ligadura dinámica
Es el mecanismo donde Java decide qué método ejecutar en tiempo de ejecución basándose en el objeto real y no en el tipo de la variable. En Java es automática, mientras que en C++ requiere la palabra virtual y en Python es intrínseca por su naturaleza dinámica.

3. Ejemplo Soldados
El polimorfismo permite que, al recorrer un array de tipo Soldado que contiene Zapador y Artillero, cada objeto ejecute su propia versión de saludar(). La ligadura dinámica garantiza que se invoque el método del hijo aunque la referencia sea del padre.

4. Uso de super
Se utiliza super.metodo() dentro de una sobreescritura para ejecutar la lógica de la superclase antes o después de la lógica específica de la subclase. Esto permite extender o complementar la funcionalidad original en lugar de reemplazarla por completo.

5. Restricciones y @Override
La sobreescritura exige mantener el nombre y parámetros exactos, permitiendo un tipo de retorno compatible (covariante). La anotación @Override es una directiva para que el compilador verifique que la sobreescritura es correcta y no una simple sobrecarga accidental.

6. Polimorfismo inicial
Java aplica polimorfismo desde el inicio al permitir sobreescribir métodos de la clase raíz Object, como toString(). Esto hace que cualquier herramienta estándar de Java (como System.out.println) use nuestras versiones personalizadas automáticamente.

7. Clases y métodos abstractos
Un método abstracto es una declaración sin cuerpo que obliga a las subclases a implementarlo para poder ser instanciadas. Se utiliza la palabra abstract tanto en la definición del método como en la declaración de la clase que lo contiene.

8. Modificador final
El modificador final impide que una clase tenga herencia o que un método sea sobreescrito, bloqueando el polimorfismo por seguridad o diseño. Un ejemplo claro en la API de Java es la clase String, que es final e inmutable.

9. Interfaces
Las interfaces son contratos que definen comportamientos (métodos) sin implementar lógica ni estado. A diferencia de las clases, una misma clase puede implementar múltiples interfaces, permitiendo que un objeto cumpla varios roles independientes.

10. Ejemplo Punto y Línea
El método calcularDistancia es abstracto en Punto y se implementa en Punto2D y Punto3D usando instanceof y downcasting. La clase Linea usa polimorfismo para calcular su longitud llamando al método sin saber si los puntos son de 2 o 3 dimensiones.

11. Herencia de interfaces
Una interfaz puede extender a otra (herencia) para ampliar el contrato original. A diferencia de las clases, Java permite la herencia múltiple entre interfaces, permitiendo que una interfaz hija agrupe métodos de varios padres.