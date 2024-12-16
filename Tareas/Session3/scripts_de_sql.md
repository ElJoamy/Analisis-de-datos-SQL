# Actividad: Exploración de Tablas y Consultas en SQL

## Instrucciones

1. **Explorar las 6 tablas**:
   - `ofertas`
   - `clientes`
   - `agencias`
   - `colaboradores`
   - `gestion`
   - `gestion_detalle`

2. **Realizar 2 consultas por tabla**:
   - Cada consulta debe incluir un alias para la tabla.
   - Debe contener al menos dos condiciones combinadas con operadores lógicos (`AND`, `OR`).
   - Mostrar el conteo de resultados con `COUNT(*)`.

3. **Entregar resultados**:
   - Consultas SQL completas.
   - Contar el total de registros que cumplen las condiciones especificadas.

## Consultas SQL

## **Tabla `ofertas`**
```sql
-- Consulta 1
SELECT COUNT(*) AS TotalOfertas
FROM ofertas o
WHERE TRY_CAST(o.Tasa AS FLOAT) > 15 
  AND (o.PeriodoVigencia = '202109' OR o.PeriodoVigencia = '202110');
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta1_ofertas.png</strong></p>
  <img src="consulta1_ofertas" alt="consulta1_ofertas" style="width: 50%; cursor: pointer;" onclick="openModal('consulta1_ofertas')">

  <!-- Modal -->
  <div id="modal_consulta1_ofertas" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta1_ofertas')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta1_ofertas" src="consulta1_ofertas" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta1_ofertas" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta1_ofertas', this.value)">
  </div>
</div>


- **Descripción**: Cuenta las ofertas con una `Tasa` mayor a 15 y `PeriodoVigencia` en '202109' o '202110'.  
- **Objetivo**: Identificar ofertas de alta tasa de interés en períodos específicos.

```sql
-- Consulta 2
SELECT COUNT(*) AS OfertasRiesgoModerado
FROM ofertas o
WHERE TRY_CAST(o.NivelRiesgo AS FLOAT) BETWEEN 0.2 AND 0.5
  AND TRY_CAST(o.Linea AS FLOAT) > 10000;
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta2_ofertas.png</strong></p>
  <img src="consulta2_ofertas" alt="consulta2_ofertas" style="width: 50%; cursor: pointer;" onclick="openModal('consulta2_ofertas')">

  <!-- Modal -->
  <div id="modal_consulta2_ofertas" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta2_ofertas')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta2_ofertas" src="consulta2_ofertas" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta2_ofertas" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta2_ofertas', this.value)">
  </div>
</div>


- **Descripción**: Filtra ofertas con `NivelRiesgo` entre 0.2 y 0.5 y `Linea` mayor a 10,000.  
- **Objetivo**: Detectar ofertas con nivel de riesgo moderado y líneas de crédito altas.

## **Tabla `clientes`**
```sql
-- Consulta 1
SELECT COUNT(*) AS TotalClientesFemeninos
FROM clientes c
WHERE c.sexo = 'F'
  AND c.numdoc IS NOT NULL
  AND c.telefono IS NOT NULL;
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta1_clientes.png</strong></p>
  <img src="consulta1_clientes" alt="consulta1_clientes" style="width: 50%; cursor: pointer;" onclick="openModal('consulta1_clientes')">

  <!-- Modal -->
  <div id="modal_consulta1_clientes" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta1_clientes')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta1_clientes" src="consulta1_clientes" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta1_clientes" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta1_clientes', this.value)">
  </div>
</div>


- **Descripción**: Cuenta clientes de sexo femenino con `numdoc` y `telefono` no nulos.  
- **Objetivo**: Validar clientes femeninos con información completa.

```sql
-- Consulta 2
SELECT COUNT(*) AS ClientesConApellidosYNumDoc
FROM clientes c
WHERE c.apellidoPaterno IS NOT NULL 
  AND (c.numdoc LIKE '0%' OR c.numdoc LIKE '%7');
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta2_clientes.png</strong></p>
  <img src="consulta2_clientes" alt="consulta2_clientes" style="width: 50%; cursor: pointer;" onclick="openModal('consulta2_clientes')">

  <!-- Modal -->
  <div id="modal_consulta2_clientes" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta2_clientes')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta2_clientes" src="consulta2_clientes" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta2_clientes" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta2_clientes', this.value)">
  </div>
</div>


- **Descripción**: Identifica clientes con `apellidoPaterno` no nulo y documentos que empiezan con '0' o terminan en '7'.  
- **Objetivo**: Filtrar clientes con características específicas en sus documentos.

## **Tabla `agencias`**
```sql
-- Consulta 1
SELECT COUNT(*) AS TotalAgenciasNixonII
FROM agencias a
WHERE a.ZONAL_NOMBRE IS NOT NULL
  AND a.CLUSTER LIKE '%NIXON%'
  AND (a.AGENCIA LIKE 'AG.%' OR a.AGENCIA LIKE '%II');
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta1_agencias.png</strong></p>
  <img src="consulta1_agencias" alt="consulta1_agencias" style="width: 50%; cursor: pointer;" onclick="openModal('consulta1_agencias')">

  <!-- Modal -->
  <div id="modal_consulta1_agencias" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta1_agencias')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta1_agencias" src="consulta1_agencias" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta1_agencias" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta1_agencias', this.value)">
  </div>
</div>


- **Descripción**: Filtra agencias donde `CLUSTER` contiene 'NIXON' y `AGENCIA` comienza con 'AG.' o termina en 'II'.  
- **Objetivo**: Identificar agencias específicas con filtros avanzados.

```sql
-- Consulta 2
SELECT COUNT(*) AS AgenciasClusterBRNoCallao
FROM agencias a
WHERE (a.ZONAL_NOMBRE IS NULL OR a.CLUSTER LIKE 'BR%')
  AND a.AGENCIA NOT LIKE '%CALLAO%';
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta2_agencias.png</strong></p>
  <img src="consulta2_agencias" alt="consulta2_agencias" style="width: 50%; cursor: pointer;" onclick="openModal('consulta2_agencias')">

  <!-- Modal -->
  <div id="modal_consulta2_agencias" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta2_agencias')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta2_agencias" src="consulta2_agencias" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta2_agencias" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta2_agencias', this.value)">
  </div>
</div>


- **Descripción**: Filtra agencias donde el `CLUSTER` comienza con 'BR' o `ZONAL_NOMBRE` es nulo, excluyendo agencias con 'CALLAO'.  
- **Objetivo**: Excluir agencias de CALLAO y validar zonas incompletas.

## **Tabla `colaboradores`**
```sql
-- Consulta 1
SELECT COUNT(*) AS ColaboradoresActivosCarsa
FROM colaboradores c
WHERE (c.ESTADO = 'A' OR c.ESTADO = 'LICENCIA POST NATAL')
  AND (c.AGENCIA LIKE '%CARSA%' OR c.AGENCIA LIKE 'AG.%')
  AND c.NOMBRE NOT LIKE '%STAFF%'
  AND c.NOMBRE IS NOT NULL;
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta1_colaboradores.png</strong></p>
  <img src="consulta1_colaboradores" alt="consulta1_colaboradores" style="width: 50%; cursor: pointer;" onclick="openModal('consulta1_colaboradores')">

  <!-- Modal -->
  <div id="modal_consulta1_colaboradores" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta1_colaboradores')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta1_colaboradores" src="consulta1_colaboradores" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta1_colaboradores" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta1_colaboradores', this.value)">
  </div>
</div>


- **Descripción**: Filtra colaboradores activos o en licencia, con `AGENCIA` que contiene 'CARSA' o empieza con 'AG.', excluyendo STAFF.  
- **Objetivo**: Identificar colaboradores activos en agencias específicas.

```sql
-- Consulta 2
SELECT COUNT(*) AS ColaboradoresFiltrados
FROM colaboradores c
WHERE (c.NACIONALIDAD = 'peruano' OR c.NACIONALIDAD = 'extranjero')
  AND (c.AGENCIA IS NULL OR c.AGENCIA LIKE 'AG.%')
  AND c.ESTADO IS NOT NULL AND c.ESTADO != 'RENUNCIO'
  AND TRY_CAST(c.CODIGO_TRABAJADOR AS INT) > 10000
  AND TRY_CAST(c.CODIGO_TRABAJADOR AS INT) < 20000;
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta2_colaboradores.png</strong></p>
  <img src="consulta2_colaboradores" alt="consulta2_colaboradores" style="width: 50%; cursor: pointer;" onclick="openModal('consulta2_colaboradores')">

  <!-- Modal -->
  <div id="modal_consulta2_colaboradores" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta2_colaboradores')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta2_colaboradores" src="consulta2_colaboradores" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta2_colaboradores" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta2_colaboradores', this.value)">
  </div>
</div>


- **Descripción**: Cuenta colaboradores peruanos o extranjeros, con `CODIGO_TRABAJADOR` entre 10,000 y 20,000, y sin estado 'RENUNCIO'.  
- **Objetivo**: Filtrar colaboradores activos con condiciones avanzadas.

## **Tabla `gestion_detalle`**
```sql
-- Consulta 1
SELECT COUNT(*) AS RegistrosValidosComplejos
FROM gestion_detalle gd
WHERE (gd.ResultadoTelefonoCRM IN ('Contacto Válido', 'Cliente no Contestable'))
  AND TRY_CAST(gd.CodigoResultadoCRM AS INT) > 2
  AND gd.NumeroOrdenColor < 5
  AND gd.GrupoEstadoGestion IN (
      SELECT DISTINCT GrupoEstadoGestion
      FROM gestion_detalle
      WHERE GrupoEstadoGestion IS NOT NULL AND GrupoEstadoGestion > 2
  )
  AND gd.DescripcionColor NOT LIKE '%ROJO%';
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta1_gestion_detalle.png</strong></p>
  <img src="consulta1_gestion_detalle" alt="consulta1_gestion_detalle" style="width: 50%; cursor: pointer;" onclick="openModal('consulta1_gestion_detalle')">

  <!-- Modal -->
  <div id="modal_consulta1_gestion_detalle" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta1_gestion_detalle')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta1_gestion_detalle" src="consulta1_gestion_detalle" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta1_gestion_detalle" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta1_gestion_detalle', this.value)">
  </div>
</div>


- **Descripción**: Filtra registros válidos con `ResultadoTelefonoCRM` en valores específicos, excluyendo colores 'ROJO' y validando subconjuntos.  
- **Objetivo**: Identificar registros válidos según estados y resultados.

```sql
-- Consulta 2
SELECT COUNT(*) AS RegistrosGestionAlternativos
FROM gestion_detalle gd
WHERE gd.GrupoEstadoGestion > 2
  AND gd.NumeroOrdenColor % 2 = 1
  AND TRY_CAST(gd.CodigoResultadoCRM AS INT) BETWEEN 1 AND 6
  AND gd.DescripcionColor IN ('NEGRO', 'AMARILLO')
  AND gd.ResultadoTelefonoCRM NOT IN ('Teléfono no existe', 'Teléfono Equivocado');
```

<!-- Imagen Interactiva -->
<div style="text-align: center;">
  <p><strong>../../imgs/Tareas/Tarea2/consulta2_gestion_detalle.png</strong></p>
  <img src="consulta2_gestion_detalle" alt="consulta2_gestion_detalle" style="width: 50%; cursor: pointer;" onclick="openModal('consulta2_gestion_detalle')">

  <!-- Modal -->
  <div id="modal_consulta2_gestion_detalle" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; 
                                     width: 100%; height: 100%; background-color: rgba(0,0,0,0.9);">
    <span onclick="closeModal('modal_consulta2_gestion_detalle')" 
          style="position: absolute; top: 20px; right: 30px; color: white; font-size: 35px; 
                 font-weight: bold; cursor: pointer;">&times;</span>
    <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
      <img id="zoom_img_consulta2_gestion_detalle" src="consulta2_gestion_detalle" style="max-width: 90%; max-height: 90%; transform-origin: center;">
    </div>
    <input type="range" min="100" max="300" value="100" id="slider_consulta2_gestion_detalle" 
           style="position: absolute; bottom: 20px; width: 50%;" 
           oninput="zoomImage('zoom_img_consulta2_gestion_detalle', this.value)">
  </div>
</div>


- **Descripción**: Filtra registros con `GrupoEstadoGestion` mayor a 2, números de orden impares y colores específicos.  
- **Objetivo**: Validar registros alternativos según criterios avanzados.


## Consideraciones
- Se utilizó un alias para cada tabla: `o`, `c`, `a`, `g`, `gd`.
- Las consultas incluyen múltiples condiciones combinadas con operadores lógicos (`AND`, `OR`) para mayor complejidad y flexibilidad.
- Los conteos permiten evaluar la cantidad de registros que cumplen las condiciones definidas.

## Link:
- Puedes acceder a la tarea en el classroom en el siguiente [enlace](https://classroom.google.com/c/NzM5NDcxNTYyMTMw/a/NzQxMjA1OTY0MzM3/details).

## ✍️ Autor
<div style="background-image: url('../../imgs/background.jpg'); background-size: cover; padding: 20px; text-align: center; border-radius: 10px;">
    <a href="https://github.com/ElJoamy" style="text-decoration: none; color: black; display: inline-block; text-align: center;">
        <img src="https://avatars.githubusercontent.com/u/68487005?v=4" width="100" alt="ElJoamy" style="border-radius: 50%; border: 2px solid #000;"/>
        <h1 style="margin: 10px 0 0; font-size: 1.5em; color: black; font-weight: bold;">Joseph Anthony Meneses Salguero</h1>
    </a>
    <br />
    <a href="https://linkedin.com/in/joamy5902" title="LinkedIn"><img src="https://img.shields.io/badge/-LinkedIn-blue?style=flat&logo=linkedin"></a>
    <a href="mailto:joamysalguero1@gmail.com" title="Email"><img src="https://img.shields.io/badge/-Email-red?style=flat&logo=gmail"></a>
    <a href="https://medium.com/@joamysalguero1" title="Medium"><img src="https://img.shields.io/badge/-Medium-black?style=flat&logo=medium"></a>
</div>

<script>
function openModal(img_id) {
  document.getElementById("modal_" + img_id.split("/").pop().split(".")[0]).style.display = "block";
}

function closeModal(modal_id) {
  document.getElementById(modal_id).style.display = "none";
}

function zoomImage(img_id, scale) {
  document.getElementById(img_id).style.transform = `scale(${scale / 100})`;
}
</script>
