# Documentación del Esquema de Base de Datos - Campeonato de Fútbol

## 1. Información General

**Nombre de la Base de Datos:** `campeonato_futbol`

**Descripción del Proyecto:**
Base de datos para gestionar información de campeonatos de fútbol, incluyendo equipos, jugadores, técnicos, árbitros, partidos, estadios y sanciones.

**Notación ER Utilizada:**

- [X] **ER Chen**: Enfoque teórico clásico (entidades, relaciones, atributos con notación formal)
- [ ] **ER Ramakrishnan (EER)**: Extensión de Chen con especialización, generalización y agregación

**Fecha de Elaboración:** [10/09/2026]

---

## 2. Entidades

### 2.1 Listado de Entidades

| #  | Nombre Entidad                    | Tipo        | Descripción                                     |
| -- | --------------------------------- | ----------- | ------------------------------------------------ |
| 1  | **Técnico**                | Fuerte      | Entrenadores de equipos                          |
| 2  | **Jugador**                 | Fuerte      | Deportistas que participan en partidos           |
| 3  | **Dirigente**               | Fuerte      | Directivos de equipos o campeonatos              |
| 4  | **Árbitro**                | Fuerte      | Árbitros que dirigen partidos                   |
| 5  | **Integrantes Tribunal**    | Fuerte      | Miembros del tribunal de árbitros               |
| 6  | **Equipo**                  | Fuerte      | Equipos participantes                            |
| 7  | **Campeonato**              | Fuerte      | Campeonatos o torneos                            |
| 8  | **Estadio**                 | Fuerte      | Lugares donde se juegan los partidos             |
| 9  | **Partido**                 | Débil      | Encuentros entre equipos (depende de Campeonato) |
| 10 | **Sentenciable**            | Fuerte      | Entidad para sanciones                           |
| 11 | **Sancionable**             | Fuerte      | Entidad padre de los que pueden ser sancionados  |
| 12 | **Falta de Partido**        | Débil      | Infracciones cometidas en un partido             |
| 13 | **Gol de Partido**          | Débil      | Goles anotados en un partido                     |
| 14 | **Sentencias**              | Débil      | Castigos aplicados por infracciones              |
| 15 | **Fecha-hora**              | Fuerte      | [Completar descripción]                         |
| 16 | **Cuerpo Técnico**         | Agregación | Conjunto de técnicos de un equipo               |
| 17 | **Plantel Jugadores**       | Agregación | Conjunto de jugadores de un equipo               |
| 18 | **Equipo de Campeonato**    | Agregación | Participación de un equipo en un campeonato     |
| 19 | **Partido de Campeonato**   | Agregación | Partidos específicos de un campeonato           |
| 20 | **Equipo Local de Estadio** | Agregación | Relación de equipo como local en un estadio     |
| 21 | **Grupo Dirigentes**        | Agregación | Conjunto de dirigentes de un equipo              |

---

### 2.2 Detalle de Entidades

#### Entidad: **Técnico**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil | [ ] Entidad Derivada

**Descripción:**
[Descripción detallada del propósito de la entidad Técnico]

**Atributos:**

| Atributo            | Tipo de Dato | Constraints  | Descripción                      |
| ------------------- | ------------ | ------------ | --------------------------------- |
| T.rut/pasaporte     | VARCHAR(20)  | PK, NOT NULL | Identificador único del técnico |
| nombre completo     | VARCHAR(100) | NOT NULL     | Nombre del técnico               |
| fecha de nacimiento | DATE         | NOT NULL     | Fecha de nacimiento               |
| nacionalidad        | VARCHAR(50)  | NOT NULL     | Nacionalidad del técnico         |

**Clave Primaria:** `T.rut/pasaporte`

**Claves Candidatas:** [Si existen otras opciones de clave]

**Restricciones Especiales:** [UNIQUE, CHECK, valores por defecto]

**Notas:** [Consideraciones especiales]

---

#### Entidad: **Jugador**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil | [ ] Entidad Derivada

**Descripción:**
[Descripción detallada del propósito de la entidad Jugador]

**Atributos:**

| Atributo            | Tipo de Dato  | Constraints  | Descripción                     |
| ------------------- | ------------- | ------------ | -------------------------------- |
| J.rut/pasaporte     | VARCHAR(20)   | PK, NOT NULL | Identificador único del jugador |
| nombre completo     | VARCHAR(100)  | NOT NULL     | Nombre del jugador               |
| fecha de nacimiento | DATE          | NOT NULL     | Fecha de nacimiento              |
| nacionalidad        | VARCHAR(50)   | NOT NULL     | Nacionalidad                     |
| posición           | VARCHAR(30)   | NOT NULL     | Posición en el campo            |
| equipo              | VARCHAR(50)   | NULL         | Equipo actual                    |
| sueldo              | DECIMAL(10,2) | NULL         | Salario mensual                  |

**Clave Primaria:** `J.rut/pasaporte`

**Claves Candidatas:** [Si existen]

**Restricciones Especiales:** [UNIQUE, CHECK]

**Notas:** [Consideraciones]

---

#### Entidad: **Dirigente**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil | [ ] Entidad Derivada

**Descripción:**
[Descripción detallada]

**Atributos:**

| Atributo        | Tipo de Dato | Constraints   | Descripción                  |
| --------------- | ------------ | ------------- | ----------------------------- |
| D.rut/pasaporte | VARCHAR(20)  | PK, NOT NULL  | Identificador único          |
| nombre completo | VARCHAR(100) | NOT NULL      | Nombre                        |
| cargo           | VARCHAR(50)  | NOT NULL      | Cargo dentro de la estructura |
| [atributo]      | [Tipo]       | [Constraints] | [Descripción]                |

**Clave Primaria:** `D.rut/pasaporte`

**Notas:** [Consideraciones]

---

#### Entidad: **Árbitro**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada]

**Atributos:**

| Atributo            | Tipo de Dato | Constraints  | Descripción         |
| ------------------- | ------------ | ------------ | -------------------- |
| A.rut/pasaporte     | VARCHAR(20)  | PK, NOT NULL | Identificador único |
| nombre completo     | VARCHAR(100) | NOT NULL     | Nombre               |
| fecha de nacimiento | DATE         | NOT NULL     | Fecha de nacimiento  |
| nacionalidad        | VARCHAR(50)  | NOT NULL     | Nacionalidad         |

**Clave Primaria:** `A.rut/pasaporte`

---

#### Entidad: **Integrantes Tribunal**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada]

**Atributos:**

| Atributo | Tipo de Dato | Constraints | Descripción   |
| -------- | ------------ | ----------- | -------------- |
| [id]     | [Tipo]       | PK          | [Descripción] |

---

#### Entidad: **Equipo**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada]

**Atributos:**

| Atributo    | Tipo de Dato | Constraints | Descripción         |
| ----------- | ------------ | ----------- | -------------------- |
| [id_equipo] | [Tipo]       | PK          | Identificador único |
| [nombre]    | [Tipo]       | NOT NULL    | [Descripción]       |

---

#### Entidad: **Campeonato**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada]

**Atributos:**

| Atributo | Tipo de Dato | Constraints | Descripción         |
| -------- | ------------ | ----------- | -------------------- |
| [id]     | [Tipo]       | PK          | Identificador único |

---

#### Entidad: **Estadio**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada]

**Atributos:**

| Atributo     | Tipo de Dato | Constraints | Descripción         |
| ------------ | ------------ | ----------- | -------------------- |
| [id_estadio] | [Tipo]       | PK          | Identificador único |
| [nombre]     | [Tipo]       | NOT NULL    | Nombre del estadio   |
| dirección   | VARCHAR(200) | NOT NULL    | Ubicación           |

---

#### Entidad: **Partido** (Entidad Débil)

**Tipo:** [ ] Entidad Fuerte | [x] Entidad Débil

**Entidad Propietaria:** `Campeonato`

**Descripción:**
[Descripción detallada]

**Atributos:**

| Atributo         | Tipo de Dato | Constraints    | Descripción             |
| ---------------- | ------------ | -------------- | ------------------------ |
| id_campeonato    | INT          | FK, PK Parcial | Referencia al campeonato |
| hora             | TIME         | PK Parcial     | Hora del partido         |
| fecha            | DATE         | PK Parcial     | Fecha del partido        |
| dirección       | VARCHAR(200) | NOT NULL       | Lugar del partido        |
| equipo_local     | VARCHAR(50)  | NOT NULL       | Equipo local             |
| equipo_visitante | VARCHAR(50)  | NOT NULL       | Equipo visitante         |

**Clave Primaria Compuesta:**

```
PK = (id_campeonato, hora, fecha, dirección)
```

**Justificación de entidad débil:**
[Explicar por qué depende de Campeonato]

---

#### Entidad: **Sentenciable**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada - Entidad que puede recibir sanciones]

**Atributos:**

| Atributo | Tipo de Dato | Constraints | Descripción         |
| -------- | ------------ | ----------- | -------------------- |
| [id]     | [Tipo]       | PK          | Identificador único |

**Nota:** Esta es una entidad padre para especialización

---

#### Entidad: **Sancionable**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada - Diferenciación de Sentenciable]

---

#### Entidad: **Falta de Partido** (Entidad Débil)

**Tipo:** [ ] Entidad Fuerte | [x] Entidad Débil

**Entidad Propietaria:** `Partido`

**Descripción:**
[Infracciones cometidas durante un partido]

**Atributos:**

| Atributo   | Tipo de Dato | Constraints    | Descripción          |
| ---------- | ------------ | -------------- | --------------------- |
| id_partido | INT          | FK, PK Parcial | Referencia al partido |
| id_falta   | INT          | PK Parcial     | Número de falta      |
| minuto     | INT          | NOT NULL       | Minuto en que ocurre  |
| [atributo] | [Tipo]       | [Constraints]  | [Descripción]        |

---

#### Entidad: **Gol de Partido** (Entidad Débil)

**Tipo:** [ ] Entidad Fuerte | [x] Entidad Débil

**Entidad Propietaria:** `Partido`

**Descripción:**
[Goles anotados en un partido]

**Atributos:**

| Atributo        | Tipo de Dato | Constraints    | Descripción              |
| --------------- | ------------ | -------------- | ------------------------- |
| id_partido      | INT          | FK, PK Parcial | Referencia al partido     |
| numero_gol      | INT          | PK Parcial     | Número secuencial de gol |
| minuto          | INT          | NOT NULL       | Minuto del gol            |
| J.rut/pasaporte | VARCHAR(20)  | FK, NOT NULL   | Jugador que anota         |

---

#### Entidad: **Sentencias** (Entidad Débil)

**Tipo:** [ ] Entidad Fuerte | [x] Entidad Débil

**Entidad Propietaria:** [Completar]

**Descripción:**
[Castigos o sanciones aplicadas]

---

#### Entidad: **Fecha-hora**

**Tipo:** [x] Entidad Fuerte | [ ] Entidad Débil

**Descripción:**
[Descripción detallada]

---

---

## 3. Estructuras de Especialización/Generalización

### 3.1 Especialización: **Sancionable**

**Entidad Padre (Generalización):** `Sancionable`

**Entidades Hijas (Especializaciones):**

- `Técnico`
- `Jugador`
- `Árbitro`

**Tipo de Especialización:**

- [X] **Total** (todo sancionable es una especialización)
- [ ] **Parcial** (puede haber sancionables sin especialización)

**Superposición:**

- [X] **Disjunta** (una instancia pertenece a máximo una especialización)
- [ ] **Solapada** (una instancia puede pertenecer a varias)

**Notación ER:**

- [X] **Chen** (triángulo + relaciones)
- [ ] **Ramakrishnan** (triángulo/círculo)

**Atributos Heredados de Sancionable:**
[Listar atributos que heredan los hijos]

**Atributos Específicos por Especialización:**

| Especialización | Atributos Propios                                                | Descripción                    |
| ---------------- | ---------------------------------------------------------------- | ------------------------------- |
| Técnico         | T.rut/pasaporte, nombre completo, fecha nacimiento, nacionalidad | Datos específicos del técnico |
| Jugador          | J.rut/pasaporte, posición, sueldo, equipo                       | Datos específicos del jugador  |
| Árbitro         | A.rut/pasaporte, [otros]                                         | Datos específicos del árbitro |

**Justificación de Estructura Elegida:**
[Explicar por qué se modeló así - por qué total/disjunta]

**Estrategia de Implementación SQL:**

- [X] **Single Table** (una tabla con discriminador)
- [ ] **Joined Table** (tabla padre + tablas hijas)
- [ ] **Class Table** (tablas independientes)
- [ ] **EAV** (Entity-Attribute-Value)

**Razón de la Estrategia:**
[Explicar por qué se eligió esta estrategia]

**Código SQL Representativo:**

```sql
-- Opción 1: Single Table (si se elige esta)
CREATE TABLE Sancionable (
    rut_pasaporte VARCHAR(20) PRIMARY KEY,
    tipo ENUM('Técnico', 'Jugador', 'Árbitro') NOT NULL,
    nombre_completo VARCHAR(100) NOT NULL,
    fecha_nacimiento DATE NOT NULL,
    nacionalidad VARCHAR(50) NOT NULL,
    -- Atributos específicos (NULL para otros tipos)
    posicion VARCHAR(30),
    sueldo DECIMAL(10,2),
    -- ...
    INDEX (tipo)
);

-- Opción 2: Joined Table (si se elige esta)
CREATE TABLE Sancionable (
    rut_pasaporte VARCHAR(20) PRIMARY KEY,
    nombre_completo VARCHAR(100) NOT NULL,
    -- ...
);

CREATE TABLE Tecnico (
    rut_pasaporte VARCHAR(20) PRIMARY KEY,
    -- atributos específicos
    FOREIGN KEY (rut_pasaporte) REFERENCES Sancionable(rut_pasaporte)
);
-- Similares para Jugador y Árbitro
```

---

### 3.2 Especialización: **Sentenciable**

**Entidad Padre:** `Sentenciable`

**Entidades Hijas:**

- `Dirigente`
- `Árbitro`
- `Integrantes Tribunal`

**Tipo:**

- [ ] **Total** | [ ] **Parcial**
- [ ] **Disjunta** | [ ] **Solapada**

**Justificación:**
[Completar]

**Estrategia de Implementación:**

- [ ] **Single Table** | [ ] **Joined Table** | [ ] **Class Table**

**Razón:**
[Completar]

---

## 4. Entidades Débiles y Agregaciones

### 4.1 Entidades Débiles

#### Entidad Débil: **Partido**

**Entidad Propietaria:** `Campeonato`

**Relación Identificadora:**

- Relación: `es_partido_de`
- Multiplicidad: (1,N) de Campeonato a Partido

**Clave Primaria Compuesta:**

```
PK = (id_campeonato, fecha, hora, dirección)
```

**Discriminante:**
`fecha`, `hora`, `dirección` (atributos que, junto con la FK, identifican el partido)

**Descripción:**
Un partido solo existe si existe un campeonato al que pertenece.

**Justificación:**
[Explicar por qué no es entidad fuerte - por qué depende de Campeonato]

---

#### Entidad Débil: **Falta de Partido**

**Entidad Propietaria:** `Partido`

**Relación Identificadora:**

- Relación: `contiene_falta`
- Multiplicidad: (1,N) de Partido a Falta

**Clave Primaria Compuesta:**

```
PK = (id_campeonato, fecha, hora, dirección, id_falta)
```

**Discriminante:**
`id_falta`

**Descripción:**
Una falta solo existe en el contexto de un partido específico.

---

#### Entidad Débil: **Gol de Partido**

**Entidad Propietaria:** `Partido`

**Clave Primaria Compuesta:**

```
PK = (id_campeonato, fecha, hora, dirección, numero_gol)
```

---

#### Entidad Débil: **Sentencias**

**Entidad Propietaria:** [Completar]

**Clave Primaria Compuesta:**

```
PK = [Completar]
```

---

### 4.2 Agregaciones

#### Agregación: **Cuerpo Técnico**

**Relación Agregada:** `Equipo` ─── `está_compuesto_por` ─── `Técnico` (N:N)

**Entidad que se Relaciona con la Agregación:** [Completar]

**Descripción:**
El Cuerpo Técnico es una agregación de la relación N:N entre Equipo y Técnico. Permite que otras entidades (como Campeonato) se relacionen específicamente con el conjunto de técnicos de un equipo.

**Justificación:**
[Explicar por qué fue necesario crear esta agregación]

**Ejemplo de Datos:**

```sql
-- Tabla de relación N:N entre Equipo y Técnico
CREATE TABLE Cuerpo_Tecnico (
    id_equipo INT NOT NULL,
    rut_tecnico VARCHAR(20) NOT NULL,
    fecha_inicio DATE NOT NULL,
    PRIMARY KEY (id_equipo, rut_tecnico),
    FOREIGN KEY (id_equipo) REFERENCES Equipo(id_equipo),
    FOREIGN KEY (rut_tecnico) REFERENCES Tecnico(rut_pasaporte)
);
```

---

#### Agregación: **Plantel Jugadores**

**Relación Agregada:** `Equipo` ─── `tiene_plantel` ─── `Jugador` (N:N)

**Entidad que se Relaciona:** [Completar]

**Descripción:**
Conjunto de jugadores de un equipo.

---

#### Agregación: **Equipo de Campeonato**

**Relación Agregada:** `Equipo` ─── `participa_en` ─── `Campeonato` (N:N)

**Entidad que se Relaciona:** [Completar]

**Descripción:**
Representación de la participación de un equipo en un campeonato específico.

---

#### Agregación: **Partido de Campeonato**

**Relación Agregada:** [Completar]

**Descripción:**
[Completar]

---

#### Agregación: **Equipo Local de Estadio**

**Relación Agregada:** `Equipo` ─── `es_local_en` ─── `Estadio` (N:N)

**Descripción:**
Un equipo puede tener un estadio local, o puede jugar en múltiples estadios.

---

#### Agregación: **Grupo Dirigentes**

**Relación Agregada:** `Equipo` ─── `lidera` ─── `Dirigente` (N:N)

**Descripción:**
Conjunto de dirigentes que lideran un equipo.

---

## 5. Relaciones

### 5.1 Listado de Relaciones

| # | Nombre              | Entidad 1    | Card. | Entidad 2        | Card. | Tipo                 |
| - | ------------------- | ------------ | ----- | ---------------- | ----- | -------------------- |
| 1 | participa_en        | Equipo       | (1,N) | Campeonato       | (1,N) | N:N (Agregación)    |
| 2 | es_local_en         | Equipo       | (1,N) | Estadio          | (1,N) | N:N (Agregación)    |
| 3 | lidera              | Dirigente    | (1,N) | Equipo           | (1,N) | N:N (Agregación)    |
| 4 | está_compuesto_por | Equipo       | (1,N) | Técnico         | (1,N) | N:N (Agregación)    |
| 5 | tiene_plantel       | Equipo       | (1,N) | Jugador          | (1,N) | N:N                  |
| 6 | es_partido_de       | Campeonato   | (1,N) | Partido          | (1,1) | 1:N (Identificadora) |
| 7 | contiene_falta      | Partido      | (1,N) | Falta de Partido | (1,1) | 1:N (Identificadora) |
| 8 | anota_gol           | Jugador      | (1,N) | Gol de Partido   | (1,1) | 1:N                  |
| 9 | recibe_sentencia    | Sentenciable | (1,N) | Sentencias       | (1,1) | 1:N (Identificadora) |

---

### 5.2 Detalle de Relaciones

#### Relación: **participa_en**

**Entidades Involucradas:** `Equipo` ─── `Campeonato`

**Multiplicidad (Notación Chen):**

- Equipo: (1,N) = `(puede_estar_en_muchos, está_en_varios)`
- Campeonato: (1,N) = `(tiene_muchos, contiene_varios)`

**Tipo de Relación:**

- [ ] 1:1 | [x] 1:N | [ ] N:N

**Descripción:**
Un equipo participa en múltiples campeonatos a lo largo del tiempo. Un campeonato tiene múltiples equipos participantes.

**Atributos de la Relación:** [Si existen]

**Restricciones:**

- UNIQUE: [Si aplica]
- Otras: [FK, ON DELETE CASCADE, etc.]

**Justificación de Decisiones:**
[Explicar el modelado]

---

#### Relación: **[Nombre Relación]**

**Entidades Involucradas:**

**Multiplicidad:**

**Tipo de Relación:**

- [ ] 1:1 | [ ] 1:N | [ ] N:N

**Descripción:**

---

## 6. Tabla Resumen: Decisiones de Diseño

### 6.1 Decisiones de Normalización

| Aspecto                      | Decisión          | Justificación |
| ---------------------------- | ------------------ | -------------- |
| Nivel de Normalización      | [x] 3NF            | [ ] BCNF       |
| Denormalización Intencional | [ ] Sí            | [x] No         |
| Atributos Multivaluados      | [x] Tabla Separada | [ ] JSON       |
| Atributos Compuestos         | [ ] Separados      | [x] Integrados |

---

### 6.2 Decisiones sobre Especialización

| Jerarquía   | Estrategia                    | Justificación |
| ------------ | ----------------------------- | -------------- |
| Sancionable  | Single Table / Joined / Class | [Por qué]     |
| Sentenciable | Single Table / Joined / Class | [Por qué]     |

---

### 6.3 Decisiones sobre Agregaciones

| Agregación          | Razón de Agregación             | Implementación              |
| -------------------- | --------------------------------- | ---------------------------- |
| Cuerpo Técnico      | Permitir relación con campeonato | Tabla intermedia + relación |
| Plantel Jugadores    | [Completar]                       | [Completar]                  |
| Equipo de Campeonato | [Completar]                       | [Completar]                  |

---

## 7. Restricciones y Reglas de Negocio

### 7.1 Restricciones de Integridad Referencial

```sql
-- FK Constraint ejemplo
ALTER TABLE Partido 
ADD CONSTRAINT fk_partido_campeonato 
FOREIGN KEY (id_campeonato) 
REFERENCES Campeonato(id_campeonato)
ON DELETE CASCADE
ON UPDATE RESTRICT;
```

[Completar con otras FK]

---

### 7.2 Restricciones de Dominio

| Atributo     | Tabla    | Restricción   | Descripción              |
| ------------ | -------- | -------------- | ------------------------- |
| nacionalidad | Técnico | VARCHAR(50)    | Nacionalidad del técnico |
| posición    | Jugador  | VARCHAR(30)    | Posición en el campo     |
| [atributo]   | [tabla]  | [CHECK/UNIQUE] | [Especificar]             |

---

### 7.3 Reglas de Negocio Implementadas

1. **Regla:** Un equipo debe tener al menos un técnico

   - **Implementación:** [En BD / Aplicación / Trigger]
   - **Ejemplo:** [Caso de uso]
2. **Regla:** Un jugador no puede pertenecer a múltiples equipos simultáneamente

   - **Implementación:** [Completar]
   - **Ejemplo:** [Completar]
3. **Regla:** Un partido solo puede existir dentro de un campeonato

   - **Implementación:** Entidad Débil (relación identificadora)
   - **Ejemplo:** [Completar]

---

## 8. Diagrama ER Conceptual

**Descripción textual del diagrama:**
El diagrama se organiza en dos secciones principales:

1. **Entidades base:** Personas (Técnico, Jugador, Dirigente, Árbitro, Integrantes Tribunal), Infraestructura (Equipo, Estadio), Competición (Campeonato)
2. **Estructuras complejas:** Partidos con sus detalles (faltas, goles), Relaciones N:N como participación en campeonatos, sanciones

```
Diagrama ASCII simplificado:

    ┌──────────────┐
    │  Campeonato  │
    └────────┬─────┘
             │ (1,N) Identificadora
             │
    ┌────────▼─────────┐
    │     Partido      │ (Débil)
    │  (Agregación)    │
    └────────┬─────────┘
             │
        ┌────┴─────┐
        │           │
    ┌───▼──┐   ┌───▼──────┐
    │Falta │   │Gol Partido│ (Débil)
    │(Débil)   │(Débil)    │
    └──────┘   └────┬──────┘
                    │ (anota)
              ┌─────▼──────┐
              │   Jugador  │
              └────────────┘
```

---

## 9. Notas de Implementación SQL

### 9.1 Índices Recomendados

```sql
-- Por búsqueda frecuente
CREATE INDEX idx_equipo_campeonato ON Equipo_Campeonato(id_campeonato);
CREATE INDEX idx_partido_fecha ON Partido(fecha);
CREATE INDEX idx_jugador_equipo ON Jugador(equipo);
CREATE INDEX idx_tecnico_equipo ON Cuerpo_Tecnico(id_equipo);
```

---

### 9.2 Vistas Útiles

```sql
-- Vista: Jugadores por equipo en un campeonato
CREATE VIEW Jugadores_por_Equipo_Campeonato AS
SELECT e.nombre AS equipo, c.nombre AS campeonato, j.nombre_completo AS jugador
FROM Plantel_Jugadores pj
JOIN Equipo e ON pj.id_equipo = e.id_equipo
JOIN Equipo_Campeonato ec ON e.id_equipo = ec.id_equipo
JOIN Campeonato c ON ec.id_campeonato = c.id_campeonato
JOIN Jugador j ON pj.rut_jugador = j.rut_pasaporte;
```

---

### 9.3 Consideraciones de Rendimiento

- [Volumen esperado de datos - partidos, jugadores, etc.]
- [Consultas frecuentes que necesitan optimización]
- [Particionamiento de tablas grandes si es necesario]
- [Desnormalización para ciertos reportes]

---

## 10. Cambios Futuros y Extensiones

| Cambio Potencial                   | Descripción                        | Impacto           |
| ---------------------------------- | ----------------------------------- | ----------------- |
| Agregar estadísticas de jugadores | Minutos jugados, goles, asistencias | Medio             |
| Incluir público/asistencia        | Registrar número de espectadores   | Bajo              |
| [Otro cambio]                      | [Descripción]                      | [Alto/Medio/Bajo] |

---

## 11. Referencias y Documentación

- [Referencia a documentos de requisitos]
- [Referencia a decisiones de arquitectura]
- [Estándares aplicados - ER Chen]

---

**Documento Elaborado por:** [Nombre]

**Revisado por:** [Nombre]

**Aprobado por:** [Nombre]

**Última Actualización:** [DD/MM/YYYY]
