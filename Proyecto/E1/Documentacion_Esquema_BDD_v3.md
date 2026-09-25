# Documentación Completa del Esquema de Base de Datos

A continuación, se detalla el modelo separando claramente las Entidades Fuertes, Entidades Débiles y Agregaciones, asignando tipos de datos lógicos (como `VARCHAR`, `DATE`, `INTEGER`) a cada atributo y explicando qué almacena la relación final en la base de datos.

**Notas:**
-En la imagen con los diagramas la parte superior tiene las entidades con sus atributos, el resto de esquemas son relaciones necesarias para solucionar distintas necesidades del enunciado, en estos se presentan agregaciones que para simpleza de los esquemas son mencionados como entidades débiles al ser usadas en otras relaciones.
-Los atributos heredados son marcados con "[]".
-Cuando la llave de una identidad se usa para relaciones o agregaciones se marca con la primera letra y un punto, ej: rut director -> D.rut.
-Aunque varias entidades que representen personas, solo Jugador y Técnico son hijos de otra ya que son las unicas que comparten la necesidad de cubrir sanciones.
-Cambios sobre estos esquemas son posibles dependiendo de las necesidades de las siguentes entregas.
-Con el fin de manteder flexibilidad para las próximas entregas se decidió que el atributo rut y rut/pasaporte de las personas serán conciderados el mismo bajo el nombre rut/pasaporte.

---

## 1. Entidades Fuertes

### 1.1 Entidad Padre

* **Sentenciable**
  * `rut/pasaporte` (PK): `VARCHAR(20)`
  * `nombre completo`: `VARCHAR(100)`
  * `fecha de nacimiento`: `DATE`
  * `nacionalidad`: `VARCHAR(50)`
  * **Justificación:** Entidad padre que guarda el registro general y los datos personales compartidos de todos los individuos (jugadores y técnicos) que participan en el campeonato y son susceptibles a recibir faltas o sentencias disciplinarias.

### 1.2 Entidades Hijas (Subtipos de Personas)

* **Jugador** *(Hereda de Sentenciable)*
  * **Atributos Heredados:**
        *`rut/pasaporte` (PK): `VARCHAR(20)`
        *`nombre completo`: `VARCHAR(100)`
        *`fecha de nacimiento`: `DATE`
        *`nacionalidad`: `VARCHAR(50)`
    * **Atributos Propios:**
        *`sueldo`: `INTEGER` (o `DECIMAL(10,2)`)
        *`posición`: `VARCHAR(30)`

* **Técnico** *(Hereda de Sentenciable)*
  * **Atributos Heredados:**
        *`rut/pasaporte` (PK): `VARCHAR(20)`
        *`nombre completo`: `VARCHAR(100)`
        *`fecha de nacimiento`: `DATE`
        *`nacionalidad`: `VARCHAR(50)`
    * **Atributos Propios:**
    * *(En este esquema, el Técnico se define principalmente por su rol y hereda todos los datos personales sin atributos adicionales propios mostrados, más allá de sus relaciones con el equipo).*

### 1.3 Otras Entidades de Personas

* **Dirigente**
  * `rut/pasaporte` (PK): `VARCHAR(20)`
    * `nombre completo`: `VARCHAR(100)`
    * `fecha de nacimiento`: `DATE`
    * `nacionalidad`: `VARCHAR(50)`
    * `email`: `VARCHAR(100)`
    * `cargo`: `VARCHAR(50)`
    * `teléfono`: `VARCHAR(20)`

* **Árbitro**
  * `rut/pasaporte` (PK): `VARCHAR(20)`
    * `nombre completo`: `VARCHAR(100)`
    * `fecha de nacimiento`: `DATE`
    * `nacionalidad`: `VARCHAR(50)`
    * `email`: `VARCHAR(100)`
    * `teléfono`: `VARCHAR(20)`

* **Integrantes Tribunal**
  * `rut/pasaporte` (PK): `VARCHAR(20)`
    * `nombre completo`: `VARCHAR(100)`
    * `fecha de nacimiento`: `DATE`
    * `email`: `VARCHAR(100)`
    * `teléfono`: `VARCHAR(20)`


### 1.3 Entidades de Organizaciones y Recintos

* **Equipo**
  * `rut` (PK): `VARCHAR(20)`
  * `nombre`: `VARCHAR(100)`
  * `dirección`: `VARCHAR(200)`
  * `email`: `VARCHAR(100)`
  * `presidente`: `VARCHAR(100)`

* **Estadio**
  * `dirección` (PK / Clave compuesta): `VARCHAR(200)`
  * `nombre` (PK / Clave compuesta): `VARCHAR(100)`
  * `cantidad espectadores`: `INTEGER`
  * `tipo`: `VARCHAR(50)`

* **Campeonato**
  * `nombre` (PK): `VARCHAR(100)`
  * `tipo`: `VARCHAR(50)`


---

## 2. Entidades Débiles

Las entidades débiles no existen por sí solas; requieren de la clave primaria de una entidad fuerte (o de una agregación) para ser identificadas unívocamente.

* **Falta de Partido**
  * `color`: `VARCHAR(20)` (ej. Amarilla, Roja)
  * `minuto`: `INTEGER`
  * **Relación Final:** Guarda el registro histórico de las infracciones cometidas `en` un Partido específico `por` un actor Sentenciable (como un Jugador). Para existir, debe heredar el ID del partido y el ID del infractor.
* **Gol de Partido**
  * `minuto`: `INTEGER`
  * **Relación Final:** Almacena el registro exacto de las anotaciones producidas `de` (dentro de) un Partido, indicando en qué minuto ocurrió y vinculando `hecho por` qué Jugador específico.
* **Sentencias**
  * `fecha de sentencia`: `DATE`
  * `motivo`: `VARCHAR(255)`
  * `cantidad de fechas`: `INTEGER`
  * **Relación Final:** Guarda los dictámenes disciplinarios o suspensiones aplicadas a un "Sancionable" en el contexto de un "Campeonato". Requiere la clave del participante infractor y del campeonato.

---

## 3. Agregaciones

Las agregaciones empaquetan una relación (entre varias entidades) y la tratan como una entidad de orden superior. Sus relaciones finales suelen guardar combinaciones de Claves Foráneas (FK) más sus atributos de relación propios.

* **Partido (Agregación de Encuentro)**

  * **Atributos de la Relación:**
    * `fecha`: `DATE`
    * `hora`: `TIME`
    * `ganador`: `VARCHAR(20)` (Guarda el RUT del equipo vencedor, si aplica).
  * **Composición:** Integra las FK del Equipo Local (`E.L.rut`), Equipo Visitante (`E.V.rut`), Campeonato (`C.nombre`) y Estadio.
  * **Relación Final:** Guarda la programación y resultado de un evento deportivo unificado. Al convertirse en una agregación, permite que este suceso centralizado sirva de ancla para que se le asignen Árbitros, Goles y Faltas sin tener que referenciar a los equipos o al estadio de forma separada en cada suceso.
* **Plantel Jugadores / Cuerpo Técnico / Grupo Dirigentes (Conformación de Equipos)**

  * **Atributos de la Relación:**
    * `fecha inicio`: `DATE`
    * `fecha fin`: `DATE`
  * **Composición:** Integra la FK del `Equipo` y la FK de la Persona (`Jugador`, `Técnico` o `Dirigente`).
  * **Relación Final:** Guarda el historial de contratos, pertenencia o afiliación de los deportistas, técnicos o directivos a un club determinado en un periodo de tiempo (`fecha inicio` a `fecha fin`).
* **Árbitro de partidos**

  * **Composición:** Integra la FK del `Árbitro` y la clave de la agregación `Partido`.
  * **Relación Final:** Guarda la designación o asignación oficial de las autoridades (terna arbitral, cuarto árbitro, etc.) responsables de impartir justicia en un encuentro programado específico.
