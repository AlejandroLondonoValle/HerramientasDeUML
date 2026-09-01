# Guía Introductoria a los Diagramas de Secuencia con Mermaid

## Autores

- Luis Alejandro Londoño Valle
- Juan Esteban Isaza Gómez
- Yeison Alejandro Zapata Gómez

---
 
## Tabla de Contenido
 
1. [Introducción a los Diagramas de Secuencia](#1-introducción-a-los-diagramas-de-secuencia)
2. [¿Qué es Mermaid?](#2-qué-es-mermaid)
3. [Estructura Básica de un Diagrama de Secuencia](#3-estructura-básica-de-un-diagrama-de-secuencia)
4. [Participantes y Actores](#4-participantes-y-actores)
5. [Mensajes y Flechas](#5-mensajes-y-flechas)
6. [Activación de Participantes](#6-activación-de-participantes)
7. [Fragmentos Combinados](#7-fragmentos-combinados)
8. [Notas Explicativas](#8-notas-explicativas)
9. [Numeración Automática de Mensajes](#9-numeración-automática-de-mensajes)
10. [Comentarios en el Código](#10-comentarios-en-el-código)
11. [Personalización Visual del Diagrama](#11-personalización-visual-del-diagrama)
12. [Buenas Prácticas de Diagramación](#12-buenas-prácticas-de-diagramación)
13. [Ejemplo Completo e Integrado](#13-ejemplo-completo-e-integrado)
14. [Errores Comunes y Cómo Evitarlos](#14-errores-comunes-y-cómo-evitarlos)
15. [Recursos Adicionales](#15-recursos-adicionales)
16. [Conclusión](#16-conclusión)
---

## 1. Introducción a los Diagramas de Secuencia

Un diagrama de secuencia es un tipo de diagrama de interacción definido dentro del Lenguaje Unificado de Modelado (UML, por sus siglas en inglés), cuyo propósito es representar de manera ordenada y temporal el intercambio de mensajes entre distintos elementos de un sistema. A diferencia de otros diagramas UML que se enfocan en la estructura estática de un sistema, el diagrama de secuencia se centra en el comportamiento dinámico, es decir, en cómo los distintos componentes de un sistema colaboran entre sí para completar un proceso determinado.

Este tipo de diagrama resulta particularmente útil para documentar procesos como la autenticación de usuarios, el procesamiento de pagos, la comunicación entre microservicios o cualquier flujo en el que el orden temporal de los mensajes sea relevante para comprender el funcionamiento del sistema.

## 2. ¿Qué es Mermaid?

Mermaid es una herramienta de generación de diagramas basada en texto plano, la cual permite crear representaciones visuales —como diagramas de flujo, diagramas de clases, diagramas de Gantt y, en particular, diagramas de secuencia— a partir de una sintaxis declarativa similar a la de Markdown. En lugar de dibujar manualmente cada elemento del diagrama, el usuario describe su estructura mediante líneas de código, y el motor de renderizado de Mermaid se encarga de calcular la posición, el trazado y el estilo visual de cada componente.

Esta característica convierte a Mermaid en una herramienta especialmente adecuada para el ámbito académico y profesional, ya que permite versionar los diagramas junto con el código fuente de un proyecto, modificarlos con facilidad y mantenerlos actualizados sin depender de herramientas de edición gráfica externas.

## 3. Estructura Básica de un Diagrama de Secuencia

Todo diagrama de secuencia en Mermaid debe iniciar con la palabra clave `sequenceDiagram`, la cual indica al motor de renderizado el tipo de diagrama que se va a construir. A partir de esta declaración, las líneas siguientes describen, en orden, los participantes del sistema y los mensajes que intercambian entre sí.

```
sequenceDiagram
  participant Cliente
  participant App

  Cliente->>App: confirmarCompra(carrito)
```

En este ejemplo mínimo se declaran dos participantes, Cliente y App, y posteriormente se define un único mensaje que fluye del primero hacia el segundo. Es importante señalar que la indentación no es obligatoria para que el diagrama funcione correctamente, aunque se recomienda utilizarla de manera consistente para mejorar la legibilidad del código fuente.

## 4. Participantes y Actores

Los participantes representan las entidades que intervienen en el proceso modelado. Estas entidades pueden ser personas, sistemas, servicios, componentes de software o cualquier otro elemento capaz de emitir o recibir mensajes.

### 4.1 La palabra clave `participant`

La declaración explícita de participantes se realiza mediante la palabra clave `participant`, seguida del identificador que se utilizará para referenciarlo en el resto del diagrama:

```
participant Banco
```

Cuando un participante se menciona por primera vez dentro de un mensaje sin haber sido declarado previamente, Mermaid lo crea de manera implícita en el orden en que aparece. Sin embargo, declarar los participantes de forma explícita al inicio del diagrama es la práctica recomendada, ya que permite controlar el orden en el que se presentan de izquierda a derecha, independientemente del orden en que participen en los mensajes.

### 4.2 La palabra clave `actor`

Como alternativa a `participant`, Mermaid ofrece la palabra clave `actor`, la cual renderiza al participante como una figura humana estilizada en lugar de un rectángulo. Esta opción resulta útil cuando el elemento representado corresponde a una persona, como un usuario o un cliente, en contraposición a un sistema o servicio automatizado:

```
actor Cliente
participant App
```

### 4.3 Alias de Visualización

En ocasiones, el identificador que se utiliza internamente para referenciar a un participante no coincide con el nombre que se desea mostrar en el diagrama, ya sea por restricciones de sintaxis —como la imposibilidad de usar tildes o espacios en los identificadores— o por preferencia estética. Para estos casos, Mermaid permite definir un alias mediante la palabra clave `as`:

```
participant BaseDatos as Base de Datos
participant Buro as "Buró de Crédito"
```

El identificador ubicado antes de `as` (`BaseDatos`, `Buro`) es el que debe utilizarse en el resto del código para referenciar al participante, mientras que el texto ubicado después de `as` es exclusivamente el que se mostrará en la etiqueta visible del diagrama.

## 5. Mensajes y Flechas

Los mensajes constituyen el elemento central de cualquier diagrama de secuencia, ya que representan la comunicación entre los distintos participantes. La sintaxis general de un mensaje sigue la siguiente estructura:

```
Origen[tipo de flecha]Destino: texto del mensaje
```

Mermaid ofrece diez variantes de flechas, cada una con un significado semántico distinto dentro de la convención UML. A continuación se describe minuciosamente cada una de ellas.

### 5.1 Flecha sólida sin punta (`->`)

```
Cliente->App: mensaje()
```

Esta variante dibuja una línea sólida sin ningún tipo de punta de flecha en el extremo. Su uso es poco frecuente en la práctica, ya que la ausencia de una punta dificulta identificar la dirección del mensaje; sin embargo, puede emplearse en diagramas simplificados donde la dirección se infiere fácilmente por el contexto o el orden de lectura.

### 5.2 Línea punteada sin punta (`-->`)

```
Cliente-->App: mensaje()
```

Idéntica a la anterior en cuanto a la ausencia de punta, pero con un trazo punteado en lugar de sólido. Al igual que la variante anterior, su uso es poco común debido a la ambigüedad que genera la falta de una punta de flecha.

### 5.3 Flecha sólida con punta llena (`->>`)

```
App->>Pasarela: procesarPago(monto, tarjeta)
```

Esta es, por amplio margen, la flecha más utilizada en los diagramas de secuencia. Representa un mensaje síncrono, es decir, una solicitud en la que el emisor permanece a la espera de una respuesta antes de continuar con su propia ejecución. Este tipo de mensaje es característico de las llamadas a métodos, las peticiones REST y, en general, cualquier interacción donde el flujo de control se detiene hasta recibir una contestación.

### 5.4 Línea punteada con punta llena (`-->>`)

```
Pasarela-->>App: pagoExitoso(idTransaccion)
```

Esta flecha se utiliza convencionalmente para representar la respuesta o el valor de retorno correspondiente a un mensaje síncrono previo. El trazo punteado permite distinguir visualmente, de un vistazo, cuáles líneas del diagrama corresponden a solicitudes y cuáles corresponden a respuestas.

### 5.5 Flechas bidireccionales (`<<->>` y `<<-->>`)

```
Cliente<<->>App: negociarSesion()
Cliente<<-->>App: confirmarNegociacion()
```

Introducidas en versiones recientes de Mermaid, estas variantes dibujan puntas de flecha en ambos extremos de la línea, ya sea con trazo sólido o punteado. Se utilizan para representar comunicación bidireccional simultánea, como ocurre en ciertos protocolos de negociación o en conexiones de tipo socket donde ambos participantes envían y reciben información como parte de un mismo intercambio conceptual.

### 5.6 Flecha sólida con cruz (`-x`)

```
App-xPasarela: procesarPago(monto, tarjeta)
```

La cruz en el extremo de la línea indica un mensaje perdido o fallido, es decir, una comunicación que fue enviada pero que nunca llegó a su destino o que fue descartada antes de ser procesada. Esta notación resulta útil para modelar escenarios de fallo de red, tiempos de espera agotados o mensajes descartados por el receptor.

### 5.7 Línea punteada con cruz (`--x`)

```
Pasarela--xApp: pagoExitoso(idTransaccion)
```

Representa el mismo concepto que la variante anterior —un mensaje perdido—, pero aplicado específicamente a una respuesta que nunca llega a su origen, en lugar de a una solicitud inicial.

### 5.8 Flecha sólida abierta (`-)`)

```
App-)ColaDeEventos: publicarEvento(pagoRealizado)
```

La punta de flecha abierta, en contraposición a la punta llena, se reserva para representar mensajes asíncronos. En un mensaje asíncrono, el emisor no espera ninguna respuesta inmediata y continúa su ejecución sin bloquearse. Esta notación es la adecuada para modelar sistemas basados en colas de mensajes, arquitecturas orientadas a eventos o cualquier comunicación de tipo publicador-suscriptor.

### 5.9 Línea punteada abierta (`--)`)

```
ColaDeEventos--)App: eventoConfirmado()
```

Corresponde a la contraparte asíncrona de la respuesta síncrona: se utiliza cuando el receptor de un evento asíncrono, en algún momento posterior, notifica de vuelta al emisor original sin que este haya quedado esperando dicha notificación.

### 5.10 Tabla Resumen de Flechas

| Sintaxis | Trazo | Punta | Significado |
|---|---|---|---|
| `->` | Sólido | Ninguna | Mensaje simple sin dirección explícita |
| `-->` | Punteado | Ninguna | Mensaje simple sin dirección explícita |
| `->>` | Sólido | Llena | Solicitud síncrona |
| `-->>` | Punteado | Llena | Respuesta o retorno |
| `<<->>` | Sólido | Llena en ambos extremos | Comunicación bidireccional |
| `<<-->>` | Punteado | Llena en ambos extremos | Comunicación bidireccional de retorno |
| `-x` | Sólido | Cruz | Mensaje perdido o fallido |
| `--x` | Punteado | Cruz | Respuesta perdida o fallida |
| `-)` | Sólido | Abierta | Mensaje asíncrono |
| `--)` | Punteado | Abierta | Respuesta asíncrona |

## 6. Activación de Participantes

La activación de un participante es un recurso visual que permite representar el intervalo de tiempo durante el cual dicho participante se encuentra ejecutando una acción, en lugar de permanecer inactivo a la espera de recibir un mensaje. Gráficamente, la activación se representa como una barra rectangular angosta superpuesta sobre la línea de vida del participante correspondiente.

### 6.1 Activación Explícita

La activación puede declararse de manera explícita mediante las palabras clave `activate` y `deactivate`:

```
Cliente->>App: confirmarCompra(carrito)
activate App
App->>Pasarela: procesarPago(monto, tarjeta)
deactivate App
```

### 6.2 Notación Abreviada

Con el propósito de reducir la extensión del código, Mermaid ofrece una notación abreviada mediante los símbolos `+` y `-`, añadidos inmediatamente después de la flecha del mensaje:

```
Cliente->>+App: confirmarCompra(carrito)
App-->>-Cliente: confirmacionCompra(idOrden)
```

En este ejemplo, el signo `+` en el primer mensaje activa a App en el instante en que recibe el mensaje, mientras que el signo `-` en el segundo mensaje lo desactiva en el instante en que envía su respuesta. Es fundamental que cada activación tenga su correspondiente desactivación; de lo contrario, la barra de activación permanecerá abierta hasta el final del diagrama, lo cual generalmente no refleja el comportamiento real del sistema.

### 6.3 Activaciones Anidadas

Un mismo participante puede tener más de una activación simultánea si, durante el procesamiento de un mensaje, recibe un segundo mensaje antes de haber respondido al primero. En estos casos, Mermaid dibuja las barras de activación una al lado de la otra, permitiendo representar visualmente la profundidad de las llamadas anidadas.

## 7. Fragmentos Combinados

Los fragmentos combinados son estructuras que permiten representar lógica condicional, repetitiva o alternativa dentro de un diagrama de secuencia, de forma análoga a las estructuras de control en un lenguaje de programación.

### 7.1 Alternativas (`alt` / `else`)

El fragmento `alt` permite representar caminos alternativos y mutuamente excluyentes dentro del flujo, de manera equivalente a una estructura condicional `if / else`:

```
alt tarjeta aprobada
  Banco-->>Pasarela: aprobado(autorizacion)
else tarjeta rechazada
  Banco-->>Pasarela: rechazado(motivo)
end
```

Es posible incluir más de una cláusula `else` dentro de un mismo bloque `alt` para representar más de dos caminos posibles, y toda estructura `alt` debe cerrarse obligatoriamente con la palabra clave `end`.

### 7.2 Bloques Opcionales (`opt`)

El fragmento `opt` representa un segmento del flujo que ocurre únicamente si se cumple una condición determinada, sin que exista una ruta alterna obligatoria en caso de que dicha condición no se cumpla:

```
opt el cliente tiene un cupón
  Cliente->>App: aplicarCupon(codigo)
end
```

A diferencia de `alt`, el fragmento `opt` no contempla una cláusula `else`: si la condición no se cumple, el diagrama simplemente continúa con el mensaje siguiente al bloque, sin ninguna consecuencia adicional.

### 7.3 Repeticiones (`loop`)

El fragmento `loop` permite representar un conjunto de mensajes que se repiten mientras se cumple una condición determinada, de forma equivalente a un ciclo `while` o `for`:

```
loop hasta un máximo de tres intentos
  App->>Pasarela: procesarPago(monto, tarjeta)
end
```

### 7.4 Procesamiento en Paralelo (`par`)

El fragmento `par` se utiliza para representar mensajes que ocurren de manera simultánea o concurrente, en lugar de secuencial. Cada rama paralela se separa mediante la palabra clave `and`:

```
par notificación al cliente
  App-->>Cliente: enviarCorreoConfirmacion()
and notificación al almacén
  App-->>Almacen: notificarNuevoPedido()
end
```

### 7.5 Sección Crítica (`critical`)

El fragmento `critical` representa un bloque de mensajes que debe ejecutarse sin interrupciones, es decir, una sección donde no se permite que otro proceso intervenga simultáneamente. Opcionalmente puede incluir rutas alternativas mediante la palabra clave `option`:

```
critical conexión a la base de datos
  App->>BaseDatos: abrirConexion()
option conexión fallida
  App-->>Cliente: errorDeConexion()
end
```

### 7.6 Interrupciones (`break`)

El fragmento `break` indica que, si se cumple determinada condición, el flujo del diagrama se interrumpe inmediatamente en ese punto, sin continuar con los mensajes posteriores:

```
break si el usuario no está autenticado
  App-->>Cliente: accesoDenegado()
end
```

### 7.7 Resaltado de Regiones (`rect`)

Aunque no constituye un fragmento de lógica condicional propiamente dicho, la palabra clave `rect` permite resaltar visualmente una región del diagrama mediante un fondo de color, lo cual resulta útil para llamar la atención sobre un conjunto de mensajes especialmente relevante:

```
rect rgb(240, 240, 240)
  App->>Pasarela: procesarPago(monto, tarjeta)
  Pasarela-->>App: pagoExitoso(idTransaccion)
end
```

## 8. Notas Explicativas

Las notas permiten añadir comentarios visibles directamente sobre el diagrama, sin que estos constituyan mensajes entre participantes. Resultan útiles para aclarar el contexto de una sección del diagrama o para documentar decisiones de diseño. Existen tres posiciones posibles para una nota:

```
Note right of Cliente: El cliente debe estar autenticado
Note left of App: Este servicio valida el formato de los datos
Note over Cliente,App: Ambos participantes intercambian un token de sesión
```

La variante `Note over` permite que la nota abarque visualmente a más de un participante a la vez, lo cual es útil para documentar un acuerdo o condición que involucra a varios elementos del sistema simultáneamente.

## 9. Numeración Automática de Mensajes

Cuando el diagrama contiene una cantidad considerable de mensajes, puede resultar conveniente numerarlos automáticamente para facilitar su referencia en un documento o exposición escrita. Esto se logra mediante la palabra clave `autonumber`, ubicada inmediatamente después de `sequenceDiagram`:

```
sequenceDiagram
  autonumber
  Cliente->>App: confirmarCompra(carrito)
  App->>Pasarela: procesarPago(monto, tarjeta)
```

En el ejemplo anterior, Mermaid asignará automáticamente el número 1 al primer mensaje y el número 2 al segundo, sin que sea necesario escribir dicha numeración de forma manual.

## 10. Comentarios en el Código

Es posible incluir comentarios dentro del código de un diagrama de secuencia, los cuales no se renderizan visualmente y sirven exclusivamente como anotaciones para quien lee o edita el código fuente. Los comentarios se declaran anteponiendo el símbolo de porcentaje doble:

```
%% Este comentario no aparecerá en el diagrama final
Cliente->>App: confirmarCompra(carrito)
```

## 11. Personalización Visual del Diagrama

Mermaid permite modificar la apariencia visual de un diagrama mediante una directiva de inicialización, la cual se coloca antes de la palabra clave `sequenceDiagram`. Esta directiva admite, entre otros parámetros, la definición de un tema predeterminado y la inyección de estilos CSS personalizados:

```
%%{init: {'theme': 'base', 'themeVariables': {'primaryColor': '#0284C7'}}}%%
sequenceDiagram
  Cliente->>App: confirmarCompra(carrito)
```

Esta funcionalidad resulta especialmente útil cuando se desea que la paleta de colores del diagrama coincida con la identidad visual de una presentación o de un documento institucional.

## 12. Buenas Prácticas de Diagramación

Con el propósito de producir diagramas claros y fáciles de interpretar, se recomienda observar las siguientes prácticas:

Declarar todos los participantes de forma explícita al inicio del diagrama, en el orden en que se desea que aparezcan de izquierda a derecha, en lugar de permitir que Mermaid los cree de manera implícita.

Mantener los nombres de los mensajes lo suficientemente descriptivos como para comprender su propósito, pero sin incluir texto excesivamente extenso que dificulte la lectura del diagrama.

Verificar que toda activación abierta mediante `activate` o el signo `+` cuente con su correspondiente desactivación, con el fin de evitar barras de activación que permanezcan abiertas de manera incorrecta.

Cerrar siempre los fragmentos combinados con la palabra clave `end`, incluyendo aquellos que contienen cláusulas adicionales como `else`, `and` u `option`.

Utilizar alias mediante la palabra clave `as` cuando el identificador interno de un participante no coincida con el nombre que se desea presentar visualmente, especialmente cuando dicho nombre contiene tildes, espacios o caracteres especiales.

## 13. Ejemplo Completo e Integrado

A continuación se presenta un ejemplo que integra varios de los conceptos descritos a lo largo de esta guía, correspondiente a un proceso simplificado de compra en línea:

```
sequenceDiagram
  autonumber
  participant Cliente
  participant App
  participant Pasarela
  participant Banco
  participant BaseDatos as Base de Datos

  Cliente->>+App: confirmarCompra(carrito)
  opt el cliente tiene un cupón
    Cliente->>App: aplicarCupon(codigo)
  end
  App->>+Pasarela: procesarPago(monto, tarjeta)
  Pasarela->>+Banco: validarTarjeta(numero, monto)
  alt tarjeta aprobada
    Banco-->>-Pasarela: aprobado(autorizacion)
    Pasarela-->>-App: pagoExitoso(idTransaccion)
    App->>+BaseDatos: guardarOrden(orden)
    BaseDatos-->>-App: ordenGuardada(idOrden)
  else tarjeta rechazada
    Banco-->>Pasarela: rechazado(fondos insuficientes)
    Pasarela-->>App: pagoFallido(motivo)
    App-->>Cliente: solicitarOtroMetodoPago()
  end
  App-->>-Cliente: confirmacionCompra(idOrden)
```

Este ejemplo combina la declaración explícita de participantes, la numeración automática de mensajes, un fragmento opcional, un fragmento alternativo y el uso de activaciones mediante la notación abreviada.

## 14. Errores Comunes y Cómo Evitarlos

Mensaje sin texto posterior a los dos puntos. Todo mensaje debe incluir una descripción después del símbolo de dos puntos; una línea como `Cliente->>App:` sin texto adicional generará un error de sintaxis.

Fragmentos combinados sin la palabra clave `end`. Cada apertura de `alt`, `opt`, `loop`, `par`, `critical` o `break` debe cerrarse obligatoriamente, incluso si el fragmento contiene únicamente una línea en su interior.

Activaciones sin su correspondiente desactivación. Abrir una activación con `+` sin cerrarla posteriormente con `-` no genera necesariamente un error de sintaxis, pero produce un resultado visual incorrecto, ya que la barra de activación permanecerá dibujada hasta el final del diagrama.

Uso de caracteres no permitidos en los identificadores. Los identificadores de los participantes no deben contener tildes, espacios ni símbolos especiales; en caso de requerir dichos caracteres en la etiqueta visible, debe recurrirse al uso de un alias mediante la palabra clave `as`.

Uso de la palabra `end` como parte del texto de un mensaje. Debido a que `end` es una palabra reservada dentro de la sintaxis de Mermaid, su uso como texto libre dentro de un mensaje puede interrumpir la interpretación correcta del diagrama; en caso de ser necesario, debe encerrarse entre paréntesis, comillas o corchetes.

## 15. Recursos Adicionales

Editor en línea oficial: https://mermaid.live, el cual permite escribir el código de un diagrama y visualizar el resultado de manera inmediata, sin necesidad de instalar ningún software adicional.

Documentación oficial del proyecto: https://mermaid.js.org, donde se encuentra la referencia completa de la sintaxis correspondiente a todos los tipos de diagramas soportados por la herramienta.

Extensiones para editores de código, disponibles tanto para Visual Studio Code como para otros entornos de desarrollo, las cuales permiten previsualizar los diagramas directamente dentro del editor mientras se escribe el código correspondiente.

## 16. Conclusión

Mermaid constituye una herramienta accesible y poderosa para la elaboración de diagramas de secuencia, particularmente adecuada para contextos académicos y de desarrollo de software, en los cuales resulta valioso poder versionar, modificar y mantener actualizada la documentación técnica de un sistema con la misma facilidad con la que se modifica su código fuente. El dominio de la sintaxis presentada en esta guía —participantes, tipos de mensajes, activaciones, fragmentos combinados y notas— constituye una base suficiente para modelar la gran mayoría de los procesos de negocio e interacciones de software que un estudiante o profesional de la ingeniería de software encontrará en la práctica.