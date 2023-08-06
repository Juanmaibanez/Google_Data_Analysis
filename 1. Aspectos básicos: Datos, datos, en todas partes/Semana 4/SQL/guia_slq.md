# Guía de SQL: Primeros pasos

Las computadoras usan diferentes idiomas para comunicarse entre sí, al igual que los seres humanos. **El lenguaje de consulta estructurado** (**SQL**, que se pronuncia “ese-cu-ele”) permite a los analistas de datos hablar con sus bases de datos. SQL es una de las herramientas de análisis de datos más útiles, especialmente cuando se trabaja con grandes conjuntos de datos en tablas. Puede ayudarte a investigar grandes bases de datos y rastrear texto (conocido como cadenas) y números, y filtrar el tipo exacto de datos que necesitas, mucho más rápido que una hoja de cálculo. 

Si es la primera vez que usas SQL, esta lectura te ayudará a adquirir los conceptos básicos para que veas lo útil que es SQL y, en particular, las consultas. Empezarás a escribir consultas SQL en muy poco tiempo.

### ¿Qué es una consulta?
Una **consulta** es una solicitud de datos o información que proviene de una base de datos. Cuando consultas bases de datos, usas SQL para comunicar tu pregunta o solicitud. Puedes intercambiar información con la base de datos siempre y cuando dominen el mismo idioma.

Cada lenguaje de programación, incluido SQL, sigue un conjunto de pautas único que se conoce como **sintaxis**. La **sintaxis** es la estructura predeterminada de un lenguaje, que incluye todas las palabras, los símbolos y la puntuación requeridos, así como su correcta colocación. Cuando escribes tus criterios de búsqueda con la sintaxis correcta, la consulta empieza a trabajar en extraer los datos que solicitaste de la base de datos de destino.

La sintaxis de cada consulta SQL es la misma: 

- Usa **SELECT** para elegir las columnas que deseas devolver.

- Usa **FROM** para elegir las tablas donde se encuentran las columnas que deseas.

- Usa **WHERE** para filtrar determinada información.

Una consulta SQL es como rellenar una plantilla. Descubrirás que, si escribes una consulta SQL desde cero, es mucho mejor iniciar una consulta escribiendo las palabras clave SELECT, FROM y WHERE en el siguiente formato: 
    
            SELECT

            FROM

            WHERE

A continuación, escribe el nombre de la tabla después del FROM, las columnas de la tabla que deseas después de SELECT y, por último, las condiciones que quieres agregar a tu consulta después del WHERE. Asegúrate de agregar un nuevo renglón y sangría cuando las agregues, como se muestra a continuación:

            SELECT
                    Columns you want to look at
            FROM
                    Table the data lives in
            WHERE
                    Certain condition is met

Seguir este método facilita el proceso de escribir consultas SQL. También puede ayudarte a cometer menos errores de sintaxis.

### Ejemplo de una consulta

Así es como aparecería una simple consulta en BigQuery, un almacén de datos de Google Cloud Platform.

            SELECT 
                    first_name 
            FROM 
                    customer_data.customer_name 
            WHERE 
                    first_name = 'Tony'

La consulta anterior usa tres comandos para localizar clientes que se llaman Tony:

1. **ELEGIR (SELECT)** la columna denominada **nombre (first_name)**

2. **DESDE (FROM)** una tabla denominada **nombre_del_cliente (customer_data)** (en un conjunto de datos denominado **nombre_del_cliente** [**customer_data**]) (el nombre del conjunto de datos siempre va seguido de un punto y, a continuación, del nombre de la tabla).

3. Pero solo se devuelven los datos **DONDE (WHERE)** el primer_nombre (first_name) es **Tony**

Los resultados de la consulta pueden ser similares a los siguientes:

| first_name | |
| ---------- | --- |
|Tony| |
|Tony| |
|Tony| |

En conclusión, esta consulta tenía la sintaxis correcta, pero no fue muy útil después de la devolución de los datos.

### Varias columnas en una consulta

En la vida real, tendrás que trabajar con más datos, además de los clientes llamados Tony. El mismo comando SELECT elige varias columnas que se pueden sangrar y agrupar.

Si solicitas varios campos de datos de una tabla, debes incluir estas columnas en el comando SELECT. Cada columna está separada por una coma, como se muestra a continuación:

```sql
        SELECT 
                Column A, 
                Column B, 
                Column C 
        FROM 
                Table where the data lives 
        WHERE 
                certain condition is met
```

Este es un ejemplo de cómo aparecería en BigQuery:

```sql
        SELECT 
                customer_id, 
                first_name, 
                last_name 
        FROM 
                customer_data.customer_name 
        WHERE 
                first_name = 'Tony'
```

La consulta anterior usa tres comandos para localizar clientes que se llaman Tony:

1. **ELEGIR (SELECT)** las columnas denominadas **id_del_cliente (customer_id), nombre (first_name)** y **apellido (last_name)**

2. **DESDE (FROM)** una tabla denominada **nombre_del_cliente (customer_data)** (en un conjunto de datos denominado **nombre_del_cliente** [**customer_data**]) (el nombre del conjunto de datos siempre va seguido de un punto y, a continuación, del nombre de la tabla)3. Pero solo se devuelven los datos **DONDE (WHERE)** el nombre (first_name) es Tony”

3. Pero solo se devuelven los datos DONDE (WHERE) el nombre (first_name) es Tony


La única diferencia entre esta consulta y la anterior es que se eligen más columnas de datos. La consulta anterior eligió solamente el nombre (first_name), mientras que esta consulta elige el ID_del_cliente (customer_id) y el apellido (last_name), además del nombre (first_name). En general, para usar los recursos de manera más eficiente, debes elegir solo las columnas que necesitas. Por ejemplo, tiene sentido que elijas más columnas si vas a usar los campos adicionales en tu cláusula WHERE. Si tienes varias condiciones en tu cláusula WHERE, pueden escribirse de la siguiente manera:

            SELECT 
                    ColumnA, 
                    ColumnB, 
                    ColumnC 
            FROM 
                    Table where the data lives 
            WHERE 
                    Condition 1 
                    AND condition 2 
                    AND condition 3

Ten en cuenta que, a diferencia del comando SELECT, que usa una coma para separar campos/variables/parámetros, el comando WHERE usa la instrucción AND para conectar condiciones. Cuando te conviertas en un escritor de consultas más experimentado, usarás otros conectores u operadores, como OR y NOT. 

Este es un ejemplo de BigQuery con varios campos usados en una cláusula WHERE:

```sql

        SELECT 
                customer_id, first_name, last_name 
        FROM 
                customer_data.customer_name 
        WHERE 
                customer_id>0 
                AND first_name = 'Tony' 
                AND last_name = 'Magnolia'
```

La consulta anterior usa tres comandos para localizar clientes con un ID de cliente válido (mayor que 0) cuyo nombre es Tony, y su apellido es Magnolia.

1. **ELEGIR (SELECT)** las columnas denominadas **id_del_cliente (customer_id), nombre (first_name**) y **apellido (last_name)**

2. **DESDE (FROM)** una tabla denominada **nombre_del_cliente (customer_data)** (en un conjunto de datos denominado **nombre_del_cliente** [**customer_data**]) (el nombre del conjunto de datos siempre va seguido de un punto y, a continuación, del nombre de la tabla).

3. Pero solo devuelve los datos **DONDE (WHERE)** el ID_del_cliente (customer_id) es mayor que **0**, **el nombre** (first_name) es **Tony** y el apellido (last_name) es **Magnolia**.

Ten en cuenta que una de las condiciones es una condición lógica que comprueba si el ID_del_cliente (customer_id) es mayor que cero.

Si un cliente se llama Tony Magnolia, los resultados de la consulta podrían ser:

| 1967 | Tony |
| ---- | ---- |


Si hay más de un cliente con el mismo nombre, los resultados de la consulta podrían ser:

| 1967 | Tony | Magnolia |
| ---- | ---- | -------- |
| 7689 | Tony | Magnolia |


### Conclusión clave

Lo más importante es recordar cómo usar SELECT, FROM y WHERE en una consulta. Una vez que hayas practicado cómo escribir tus propias consultas SQL más adelante en el programa, las consultas con varios campos serán más sencillas.