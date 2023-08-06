# Las posibilidades de SQL son infinitas
Has aprendido que una consulta SQL usa **SELECT** , **FROM** y **WHERE** para especificar los datos que se devolverán desde la consulta. Esta lectura proporciona información más detallada sobre cómo estructurar las consultas, usar condiciones WHERE, elegir todas las columnas en una tabla, agregar comentarios y usar alias. Esta información hace que sea más fácil para ti entender (y escribir) consultas para poner SQL en práctica. En la última sección de esta lectura, se proporciona un ejemplo de lo que haría un analista de datos a fin de extraer los datos de los empleados para un proyecto. 

### Uso de mayúsculas, sangría y punto y coma
Puedes escribir tus consultas SQL solo en minúsculas, y no tienes que preocuparte por los espacios adicionales entre palabras. Sin embargo, el uso de mayúsculas y sangría puede ayudarte a leer la información más fácilmente. Mantén tus consultadas ordenadas. Serán más fáciles de revisar o solucionar si necesitas comprobarlas más adelante.

```sql
        SELECT 
                field1 
        FROM 
                table 
        WHERE 
                field1 = condition;
```
Ten cuenta que la instrucción SQL que se muestra arriba tiene un punto y coma al final. El punto y coma es un terminador de instrucción que forma parte de la norma SQL-92 del Instituto Nacional Estadounidense de Estándares (ANSI), la cual es una sintaxis común recomendada para su adopción por todas las bases de datos SQL. Sin embargo, no todas las bases de datos SQL han adoptado o cumplido con el uso del punto y coma, por lo que es posible que te encuentres con algunas instrucciones SQL que no terminan con un punto y coma. Si una instrucción funciona sin punto y coma, es correcta.

### Condiciones WHERE
En la consulta que se mostró anteriormente, la cláusula SELECT identifica la columna de la cual deseas extraer datos por nombre, **field1**, y la cláusula **FROM** identifica la tabla donde se encuentra la columna por nombre, **table**. Por último, la cláusula **WHERE** restringe la consulta para que la base de datos devuelva solo los datos con una coincidencia de valor exacta, o los datos que coincidan con una determinada condición que deseas satisfacer. 

Por ejemplo, si estás buscando a un cliente específico con el apellido Chavez, la cláusula WHERE sería: 

**WHERE field1 = 'Chavez'**

Sin embargo, si estás buscando a todos los clientes que tienen un apellido que empieza con las letras “Ch”, la cláusula WHERE sería:

**WHERE field1 LIKE 'Ch%'**

En conclusión, la cláusula LIKE es muy poderosa porque te permite decirle a la base de datos que busque un patrón determinado. El signo de porcentaje (%) se usa como comodín para que coincida con uno o más caracteres. En el ejemplo anterior, se devolverían tanto **Chávez** como **Chen**. Ten en cuenta que en algunas bases de datos se usa un asterisco (*) como comodín en lugar de un signo de porcentaje (%).

### ELEGIR (SELECT) todas las columnas
¿Puedes usar **SELECT \*** ?

En el ejemplo, si reemplazaras **SELECT field1** por **SELECT *** , elegirías todas las columnas de la tabla en lugar de la columna field1 sola. Desde el punto de vista de la sintaxis, es una instrucción SQL correcta, pero debes usar el asterisco (*) con moderación y precaución. Según cuántas columnas tenga una tabla, es posible que elijas una enorme cantidad de datos. Si eliges demasiados datos, es posible que la consulta se ejecute muy lentamente.

### Comentarios
Algunas tablas no están diseñadas con convenciones de nomenclatura suficientemente descriptivas. En el ejemplo, **field1** era la columna del apellido de un cliente; pero no podrías saberlo por el nombre. Un nombre más adecuado podría haber sido algo como **last_name**. En estos casos, puedes agregar comentarios junto a tu SQL para ayudarte a recordar qué representa el nombre. Los comentarios son textos colocados entre ciertos caracteres, **/\*** y **\*/**, o después de dos guiones (--), como se muestra a continuación. 

SQL statements with comments shown between /* and */ and after --

```sql
        SELECT
                field1 /* this is the last name column*/
        FROM
                table -- this is the customer data table
        WHERE
                dield1 LIKE 'CH%';
```

Los comentarios también se pueden agregar dentro o fuera de una instrucción. Puedes usar esta flexibilidad para proporcionar una descripción general de lo que harás, notas paso a paso sobre cómo lo lograrás y por qué estableces diferentes parámetros o condiciones. 

    --This is an important query used later to join with the accounts table. 
            SELECT 
                    rowkey, -- key used to join with account_id
                    Info.date, -- date is in string format YYYY-MM-DD HH:MM:SS
                    Info.code -- e.g., 'pub-###'
            FROM 
                    Publishers

Mientras más cómodo te sientas con SQL, más fácil te resultará leer y comprender las consultas de un vistazo. Aun así, nunca está de más que tengas comentarios en una consulta para recordar lo que estás tratando de hacer. Esto también facilita que otros usuarios entiendan tu consulta si la compartes con ellos. A medida que tus consultas se vuelvan más complejas, esta práctica te ahorrará mucho tiempo y energía para comprender las consultas complejas que escribiste hace meses o años. 

#### Ejemplo de una consulta con comentarios
Este es un ejemplo de cómo se pueden escribir los comentarios en BigQuery:
```sql
        -- Pull basic informaction from the customer table
        SELECT 
                customer_id, --main ID used to join with customer_address
                first_name, --customet's first name from Loyalty program
                last_name --customer's Last name
        FROM 
                customer_data.customer_name
```

En el ejemplo anterior, se agregó un comentario antes de la instrucción SQL para explicar qué hace la consulta. Además, se agregó un comentario junto a cada uno de los nombres de columna para describir la columna y su uso. Generalmente, se admiten dos guiones (--). Por lo tanto, se recomienda usarlos de manera coherente. Puedes usar # en lugar de -- en la consulta anterior, pero # no se reconoce en todas las versiones de SQL; por ejemplo, MySQL no reconoce #.  También puedes colocar comentarios entre /* y */ si la base de datos que estás usando lo permite. 

A medida que perfecciones tus capacidades desde un punto de vista profesional, según la base de datos SQL que uses, podrás elegir los símbolos de delimitación de comentarios adecuados que prefieras y continuar su uso para mantener un estilo coherente. A medida que tus consultas se vuelvan más complejas, esta práctica te ahorrará mucho tiempo y energía para comprender las consultas complejas que escribiste, probablemente, hace varios meses o años.

### Alias
Para simplificarte la tarea, puedes asignar un nuevo nombre o **alias** a los nombres de columna o tabla para que sea más fácil trabajar con ellos (y evitar la necesidad de agregar comentarios). Esto se hace con una cláusula SQL AS. En el siguiente ejemplo, se asigna el alias **last_name** a **field1** y el alias **customers** a **table**.Estos alias son válidos solo para la duración de la consulta. Un alias no cambia el nombre real de una columna o tabla de la base de datos.

#### Ejemplo de una consulta con alias
```sql
        field1 AS last_name -- Alias to make my work easier
        table AS customers -- Alias to make my work easier

        SELECT
                last_name
        FROM
                customers
        WHERE
                last_name LIKE 'CH%';
```

### Pon SQL a trabajar como analista de datos
Imagina que eres un analista de datos que trabaja para una pequeña empresa, y tu gerente te pide algunos datos de los empleados. Tú decides escribir una consulta con SQL para obtener lo que necesitas de la base de datos. 

Quieres extraer todas las columnas: **empID, firstName, lastName, jobCode y salary**. Como sabes que la base de datos no es tan amplia, usas **SELECT \*** en lugar de escribir el nombre de cada columna en la cláusula **SELECT**.  Mediante esta opción, elegirás todas las columnas de la tabla Empleado (Employee) en la cláusula **FROM**.
```sql
        SELECT
                * 
        FROM 
                Employee
```
Ahora, puedes obtener información más específica sobre los datos que deseas de la tabla Empleado (Employee). Si deseas todos los datos sobre los empleados que trabajan en el código de trabajo **SFI**, puedes usar una cláusula **WHERE** para filtrar los datos en función de este requisito adicional. 

Aquí usas:
```sql
        SELECT 
                * 
        FROM 
                Employee 
        WHERE 
                jobCode = 'SFI'
```
Es posible que una parte de los datos de los resultados devueltos por la consulta SQL tengan el siguiente aspecto:

| empID | firstName | lastName | jobCode | salary |
| ----- | --------- | -------- | ------- | ------ |
|0002|Homer|Simpson|SFI|15000|
|0003|Marge|Simpson|SFI|30000|
|0034|Bart|Simpson|SFI|25000|
|0067|Lisa|Simpson|SFI|38000|
|0088|Ned|Flanders|SFI|42000|
|0076|Barney|Gumble|SFI|32000|

Supongamos que observas un amplio intervalo salarial para el código de trabajo **SFI**. Puede que quieras marcar a los empleados de todos los departamentos que tienen los salarios más bajos para tu gerente. Debido a que los pasantes también están incluidos en la tabla y tienen salarios inferiores a USD 30,000, debes asegurarte de que los resultados te devuelvan únicamente a los empleados de tiempo completo con salarios que sean menores que esa cantidad. En otras palabras, deseas excluir a los pasantes con el código de trabajo **INT** que también ganan menos de USD 30,000. La cláusula **AND** te permite analizar ambas condiciones. 

Tú creas una consulta SQL similar a la siguiente, en la cual <> significa “no es igual a”:
```sql
        SELECT
                *
        FROM
                Employee
        WHERE
                jobCode <> 'INT'
                AND salary <= 30000;>
```

Los datos obtenidos de la consulta SQL podrían ser parecidos a los siguientes (los datos de los pasantes con el código de trabajo INT no se devuelven):

| empID | firstName | lastName | jobCode | salary |
| ----- | --------- | -------- | ------- | ------ |
|0002|Homer|Simpson|SFI|15000|
|0003|Marge|Simpson|SFI|30000|
|0034|Bart|Simpson|SFI|25000|
|0108|Edna |Krabappel|TUL|18000|
|0099|Moe |Szyslak|ANA|28000|

Al contar con un rápido acceso a este tipo de datos mediante SQL, puedes proporcionarle a tu gerente muchas perspectivas diferentes acerca de los datos de los empleados, por ejemplo, si los salarios que ganan los empleados en toda la empresa son equitativos. Afortunadamente, la consulta muestra que solo dos empleados adicionales podrían necesitar un ajuste salarial, y compartes los resultados con tu gerente. 

Extraer los datos, analizarlos e implementar una solución podría, en última instancia, contribuir a mejorar la satisfacción y la lealtad de los empleados. Esto convierte a SQL en una herramienta muy poderosa. 

### Recursos para obtener más información
Los no abonados pueden acceder a estos recursos de forma gratuita; pero, si un sitio limita el número de artículos gratuitos por mes y tú ya alcanzaste tu límite, marca el recurso como favorito y vuelve a él más tarde.

- [Tutorial de SQL de W3Schools](https://www.w3schools.com/sql/default.asp): Si te gustaría explorar un tutorial detallado de SQL, este es el lugar perfecto para empezar. Este tutorial incluye ejemplos interactivos que puedes editar, analizar y recrear. Úsalo como referencia o completa todo el tutorial para practicar el uso de SQL. Haz clic en el botón verde Empezar el aprendizaje de SQL ahora o en el botón Siguiente para comenzar el tutorial.

- [Hoja de referencia de SQL](https://www.sqltutorial.org/sql-cheat-sheet/): Si eres un estudiante más avanzado, lee este artículo para obtener información sobre la sintaxis SQL estándar que se usa en PostgreSQL. Cuando finalices, sabrás mucho más sobre SQL y estarás preparado para aplicarlo en el análisis empresarial y otras tareas.