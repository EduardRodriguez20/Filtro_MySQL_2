# Proyecto Parte 2

Eduard Andres Rodriguez Holguin - Campuslands

### Creacion y poblacion de las tablas

A continuacion se especifica la creacion de tablas y la poblacion de ellas mismas teniendo en cuenta mi criterio.

#### Creacion y Poblacion

```sql
   CREATE DATABASE TMB_DB;
   USE TMB_BD;

   CREATE TABLE `Zona`(
      `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      `nombre` VARCHAR(255) NOT NULL
   );
   INSERT INTO Zona (id, nombre) VALUES
      (1, 'Norte'),
      (2, 'Sur'),
      (3, 'Oriente'),
      (4, 'Occidente'),
      (5, 'Floridablanca'),
      (6, 'Girón'),
      (7, 'Piedecuesta');


   CREATE TABLE Rutas(
      id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      nombre VARCHAR(255) NOT NULL,
      id_zona INT NOT NULL,
      tiempo_ruta TIME NOT NULL,
      FOREIGN KEY (id_zona) REFERENCES Zona (id) 
   );
   INSERT INTO `Rutas` (id, nombre, id_zona, tiempo_ruta) VALUES
      (1, 'Universidades', 1, '2:00:00'),
      (2, 'Café Madrid', 1, '2:15:00'),
      (3, 'Cacique', 1, '1:45:00'),
      (4, 'Diamantes', 3, '1:50:00'),
      (5, 'Terminal', 3, '2:00:00'),
      (6, 'Prado', 3, '1:30:00'),
      (7, 'Cabecera', 1, '1:30:00'),
      (8, 'Ciudadela', 4, '2:00:00'),
      (9, 'Punta Estrella', 4, '2:30:00'),
      (10, 'Niza', 4, '2:45:00'),
      (11, 'Autopista', 5, '2:15:00'),
      (12, 'Lagos', 5, '2:15:00'),
      (13, 'Centro Florida', 5, '2:30:00');


   CREATE TABLE `Estaciones`(
      `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      `nombre` VARCHAR(255) NOT NULL
   );
   INSERT INTO `Estaciones` (id, nombre) VALUES
      (1, 'Colseguros'),
      (2, 'Clínica Chicamocha'),
      (3, 'Plaza Guarín'),
      (4, 'Mega Mall'),
      (5, 'UIS'),
      (6, 'UDI'),
      (7, 'Santo Tomás'),
      (8, 'Boulevard Santander'),
      (9, 'Búcaros'),
      (10, 'Rosita'),
      (11, 'Puerta del Sol'),
      (12, 'Cacique'),
      (13, 'Plaza Satélite'),
      (14, 'La Sirena'),
      (15, 'Provenza'),   
      (16, 'Fontana'),
      (17, 'Gibraltar'),
      (18, 'Terminal'),
      (19, 'Mutis'),
      (20, 'Plaza Real');


   CREATE TABLE `Estaciones_ruta`(
      `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      `id_ruta` INT NOT NULL,
      `id_estacion` INT NOT NULL,
      FOREIGN KEY (id_ruta) REFERENCES Rutas (id),
      FOREIGN KEY (id_estacion) REFERENCES Estaciones (id)
   );
   INSERT INTO `Estaciones_ruta` (id, id_ruta, id_estacion) VALUES
      (1, 1, 1),
      (2, 1, 2),
      (3, 1, 3),
      (4, 1, 4),
      (5, 1, 5),
      (6, 1, 6),
      (7, 1, 7),
      (8, 3, 8),
      (9, 3, 9),
      (10, 3, 10),
      (11, 3, 11),
      (12, 3, 12),
      (13, 4, 13),
      (14, 4, 14),
      (15, 4, 15),
      (16, 5, 16),
      (17, 5, 17),
      (18, 8, 18),
      (19, 8, 19),
      (20, 8, 20);
      

   CREATE TABLE `Bus`(
      `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      `placa` VARCHAR(255) NOT NULL
   );
   INSERT INTO `Bus` (id, placa) VALUES
      (1, 'XVH345'),
      (2, 'XDL965'),
      (3, 'XFG847'),
      (4, 'XRJ452'),
      (5, 'XDF459'),
      (6, 'XET554'),
      (7, 'XKL688'),
      (8, 'XXL757');


   CREATE TABLE `Conductor`(
      `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      `nombres` VARCHAR(255) NOT NULL,
      `apellidos` VARCHAR(255) NOT NULL
   );
   INSERT INTO `Conductor` (id, nombres, apellidos) VALUES
      (1, 'Andrés Manuel', 'López Obrador'),
      (2, 'Nicolás', 'Maduro Moros'),
      (3, 'Alberto', 'Fernández'),
      (4, 'Luiz Inácio', 'Lula da Silva'),
      (5, 'Gabriel', 'Boric'),
      (6, 'Miguel', 'Díaz-Canel'),
      (7, 'Daniel', 'Ortega'),
      (8, 'Gustavo', 'Petro Urrego'),
      (9, 'Luis', 'Arce'),
      (10, 'Xiomara', 'Castro');


   CREATE TABLE `Programacion`(
      `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      `id_conductor` INT NOT NULL,
      `id_bus` INT NOT NULL,
      `id_ruta` INT NOT NULL,
      `dia` ENUM('Lunes', 'Martes', 'Miercoles', 'Jueves', 'Viernes', 'Sabado', 'Domingo'),
      FOREIGN KEY (id_conductor) REFERENCES Conductor (id),
      FOREIGN KEY (id_bus) REFERENCES Bus (id),
      FOREIGN KEY (id_ruta) REFERENCES Rutas (id)
   );
   INSERT INTO `Programacion` (id, id_conductor, id_ruta, id_bus, dia) VALUES
      (1, 5, 1, 1, "Lunes"),
      (2, 5, 1, 1, "Martes"),
      (3, 5, 1, 3, "Miercoles"),
      (4, 5, 1, 3, "Jueves"),
      (5, 5, 2, 5, "Viernes"),
      (6, 5, 2, 5, "Sabado"),
      (7, 5, 2, 5, "Domingo"),
      (8, 3, 4, 5, "Lunes"),
      (9, 3, 4, 6, "Martes"),
      (10, 3, 4, 1, "Miercoles"),
      (11, 3, 5, 1, "Jueves"),
      (12, 3, 5, 3, "Viernes"),
      (13, 3, 5, 3, "Sabado"),
      (14, 3, 5, 3, "Domingo"),
      (15, 10, 10, 3, "Lunes"),
      (16, 10, 10, 3, "Martes"),
      (17, 10, 10, 5, "Miercoles"),
      (18, 10, 10, 5, "Jueves"),
      (19, 10, 10, 4, "Viernes"),
      (20, 10, 11, 7, "Sabado"),
      (21, 10, 11, 7, "Domingo"),
      (22, 7, 11, 7, "Lunes"),
      (23, 7, 11, 7, "Martes"),
      (24, 6, 12, 7, "Miercoles"),
      (25, 6, 12, 7, "Jueves"),
      (26, 6, 12, 7, "Viernes"),
      (27, 6, 12, 6, "Sabado"),
      (28, 6, 12, 6, "Domingo");
```

### Consultas

1. Cantidad de Paradas por Ruta
   ```sql
      SELECT Rutas.nombre AS Nombre_ruta, 
      COUNT(Estaciones_ruta.id_estacion) AS Cantidad_estaciones
      FROM `Estaciones_ruta`
      INNER JOIN Rutas ON Estaciones_ruta.id_ruta = Rutas.id
      GROUP BY Estaciones_ruta.id_ruta, Rutas.nombre;
   ```

   Resultado:
   
   ```bash
      +---------------+---------------------+
      | Nombre_ruta   | Cantidad_estaciones |
      +---------------+---------------------+
      | Universidades |                   7 |
      | Cacique       |                   5 |
      | Diamantes     |                   3 |
      | Terminal      |                   2 |
      | Ciudadela     |                   3 |
      +---------------+---------------------+

   ```
2. Nombre de las Paradas de la Ruta Universidades
   ```sql
      SELECT Estaciones.nombre AS Estaciones FROM `Estaciones_ruta`
      INNER JOIN `Estaciones` ON Estaciones_ruta.id_estacion = Estaciones.id
      WHERE Estaciones_ruta.id_ruta = 1;
   ```

   Resultado:
   
   ```bash
      +---------------------+
      | Estaciones          |
      +---------------------+
      | Colseguros          |
      | Clínica Chicamocha  |
      | Plaza Guarín        |
      | Mega Mall           |
      | UIS                 |
      | UDI                 |
      | Santo Tomás         |
      +---------------------+
   ```
3. Nombres de las Rutas No Programadas
   ```sql
      SELECT Rutas.nombre FROM Rutas
      WHERE Rutas.id NOT IN (SELECT Programacion.id_ruta FROM `Programacion`);
   ```

   Resultado:
   
   ```bash
      +----------------+
      | nombre         |
      +----------------+
      | Cacique        |
      | Prado          |
      | Cabecera       |
      | Ciudadela      |
      | Punta Estrella |
      | Centro Florida |
      +----------------+
   ```
4. Rutas Programadas sin Conductor Asignado
   ```sql
      SELECT Rutas.nombre AS Ruta FROM `Programacion`
      INNER JOIN `Rutas` ON Programacion.id_ruta = Rutas.id
      WHERE Programacion.id_conductor IS NULL;
   ```

   Resultado:
   
   ```bash
      Empty set (0,00 sec)
   ```

   Porque el resultado es vacio? Esto se debe a que en la tabla Programacion no hay ningun id_conductor NULL osea, que no este asignado, esto responde a la solicitud del problema.

5. Conductores No Asignados a la Programación
   ```sql
      SELECT CONCAT(Conductor.nombres, " ",Conductor.apellidos) AS Conductor FROM `Conductor`
      WHERE Conductor.id NOT IN (SELECT Programacion.id_conductor FROM `Programacion`);
   ```

   Resultado:
   
   ```bash
      +-------------------------------+
      | Conductor                     |
      +-------------------------------+
      | Andrés Manuel López Obrador   |
      | Nicolás Maduro Moros          |
      | Luiz Inácio Lula da Silva     |
      | Gustavo Petro Urrego          |
      | Luis Arce                     |
      +-------------------------------+
   ```
6. Buses No asignados a la Programación
   ```sql
      SELECT Bus.placa AS Placa_Bus FROM `Bus`
      WHERE Bus.id NOT IN (SELECT Programacion.id_bus FROM `Programacion`);
   ```

   Resultado:
   
   ```bash

   ```
7. Zonas NO Programadas
   ```sql
      SELECT Zona.nombre AS Zona FROM `Zona`
      WHERE Zona.id NOT IN (SELECT Zona.id FROM `Programacion`
      INNER JOIN `Rutas` ON Programacion.id_ruta = Rutas.id
      INNER JOIN `Zona` ON Rutas.id_zona = Zona.id);
   ```

   Resultado:
   
   ```bash
      +-----------+
      | Placa_Bus |
      +-----------+
      | XDL965    |
      | XXL757    |
      +-----------+
   ```

   Porque no aparece la zona Oriente en las Zonas que NO estan programadas? Porque en el ingreso de mis datos adicione la Zona Oriente a las que si estan programadas, Esto lo puede validar con la siguiente consulta:

   ```sql
      SELECT DISTINCTROW Zona.id, Zona.nombre FROM `Programacion`
      INNER JOIN `Rutas` ON Programacion.id_ruta = Rutas.id
      INNER JOIN `Zona` ON Rutas.id_zona = Zona.id;
   ```

   Resultado:
   
   ```bash
      +----+---------------+
      | id | nombre        |
      +----+---------------+
      |  1 | Norte         |
      |  3 | Oriente       |
      |  4 | Occidente     |
      |  5 | Floridablanca |
      +----+---------------+
   ```

8. Programación asignada a cada conductor (Conductor, Ruta y Día)
   ```sql
      SELECT CONCAT(Conductor.nombres, " ", Conductor.apellidos) AS Conductor,
      Rutas.nombre AS Ruta,
      Programacion.dia AS Dia FROM `Programacion`
      INNER JOIN `Conductor` ON Programacion.id_conductor = Conductor.id
      INNER JOIN `Rutas` ON Programacion.id_ruta = Rutas.id;
   ```

   Resultado:
   
   ```bash
      +--------------------+---------------+-----------+
      | Conductor          | Ruta          | Dia       |
      +--------------------+---------------+-----------+
      | Gabriel Boric      | Universidades | Lunes     |
      | Gabriel Boric      | Universidades | Martes    |
      | Gabriel Boric      | Universidades | Miercoles |
      | Gabriel Boric      | Universidades | Jueves    |
      | Gabriel Boric      | Café Madrid   | Viernes   |
      | Gabriel Boric      | Café Madrid   | Sabado    |
      | Gabriel Boric      | Café Madrid   | Domingo   |
      | Alberto Fernández  | Diamantes     | Lunes     |
      | Alberto Fernández  | Diamantes     | Martes    |
      | Alberto Fernández  | Diamantes     | Miercoles |
      | Alberto Fernández  | Terminal      | Jueves    |
      | Alberto Fernández  | Terminal      | Viernes   |
      | Alberto Fernández  | Terminal      | Sabado    |
      | Alberto Fernández  | Terminal      | Domingo   |
      | Xiomara Castro     | Niza          | Lunes     |
      | Xiomara Castro     | Niza          | Martes    |
      | Xiomara Castro     | Niza          | Miercoles |
      | Xiomara Castro     | Niza          | Jueves    |
      | Xiomara Castro     | Niza          | Viernes   |
      | Xiomara Castro     | Autopista     | Sabado    |
      | Xiomara Castro     | Autopista     | Domingo   |
      | Daniel Ortega      | Autopista     | Lunes     |
      | Daniel Ortega      | Autopista     | Martes    |
      | Miguel Díaz-Canel  | Lagos         | Miercoles |
      | Miguel Díaz-Canel  | Lagos         | Jueves    |
      | Miguel Díaz-Canel  | Lagos         | Viernes   |
      | Miguel Díaz-Canel  | Lagos         | Sabado    |
      | Miguel Díaz-Canel  | Lagos         | Domingo   |
      +--------------------+---------------+-----------+
   ```
9. Programación asignada a conductores que hacen rutas de más de dos horas
   ```sql
      SELECT CONCAT(Conductor.nombres, " ", Conductor.apellidos) AS Conductor,
      Rutas.nombre AS Ruta,
      Programacion.dia AS Dia FROM `Programacion`
      INNER JOIN `Conductor` ON Programacion.id_conductor = Conductor.id
      INNER JOIN `Rutas` ON Programacion.id_ruta = Rutas.id
      WHERE Rutas.tiempo_ruta > "2:00:00";
   ```

   Resultado:
   
   ```bash
      +--------------------+--------------+-----------+
      | Conductor          | Ruta         | Dia       |
      +--------------------+--------------+-----------+
      | Gabriel Boric      | Café Madrid  | Viernes   |
      | Gabriel Boric      | Café Madrid  | Sabado    |
      | Gabriel Boric      | Café Madrid  | Domingo   |
      | Xiomara Castro     | Niza         | Lunes     |
      | Xiomara Castro     | Niza         | Martes    |
      | Xiomara Castro     | Niza         | Miercoles |
      | Xiomara Castro     | Niza         | Jueves    |
      | Xiomara Castro     | Niza         | Viernes   |
      | Xiomara Castro     | Autopista    | Sabado    |
      | Xiomara Castro     | Autopista    | Domingo   |
      | Daniel Ortega      | Autopista    | Lunes     |
      | Daniel Ortega      | Autopista    | Martes    |
      | Miguel Díaz-Canel  | Lagos        | Miercoles |
      | Miguel Díaz-Canel  | Lagos        | Jueves    |
      | Miguel Díaz-Canel  | Lagos        | Viernes   |
      | Miguel Díaz-Canel  | Lagos        | Sabado    |
      | Miguel Díaz-Canel  | Lagos        | Domingo   |
      +--------------------+--------------+-----------+
   ```
10. Nombres de Zonas y cantidad de rutas que tienen programadas (Contar)
   ```sql
      SELECT Zona.nombre, COUNT(Programacion.id_ruta) AS Cantidad_Rutas FROM `Programacion`
      INNER JOIN `Rutas` ON Programacion.id_ruta = Rutas.id
      INNER JOIN `Zona` ON Rutas.id_zona = Zona.id
      GROUP BY Zona.nombre;
   ```

   Resultado:
   
   ```bash
      +---------------+----------------+
      | nombre        | Cantidad_Rutas |
      +---------------+----------------+
      | Norte         |              7 |
      | Oriente       |              7 |
      | Occidente     |              5 |
      | Floridablanca |              9 |
      +---------------+----------------+
   ```

   Como comentaba en el punto 7 en la forma en la que ingrese mis datos, en las rutas programadas, hay rutas que son de la Zona de Oriente, por lo tanto aparece en el resultado.