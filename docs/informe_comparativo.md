# Informe comparativo

**Grupo**: grupoXX

**Integrantes**:
- David Alexander Zambrano B. - R1 (Terraform)
- [Nombre Completo 2] - R2 (Pulumi)
- [Nombre Completo 3] - R3 (Platform Lead)

## 7.1 Matriz de Comparación Empírica

<table border="1" cellpadding="8" style="border-collapse: collapse; width: 100%;">
  <thead>
    <tr>
      <th style="border: 1px solid;">Criterio de comparación</th>
      <th style="border: 1px solid;">Terraform (HCL)</th>
      <th style="border: 1px solid;">Pulumi (Python)</th>
      <th style="border: 1px solid;">Análisis del Grupo con Evidencia Observada</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid;">1. Curva de aprendizaje y sintaxis</td>
      <td style="border: 1px solid;">DSL declarativo especializado</td>
      <td style="border: 1px solid;">Lenguaje general orientado a objetos</td>
      <td style="border: 1px solid;">(¿Quién tardó menos en configurar el contenedor y por qué?)</td>
    </tr>
    <tr>
      <td style="border: 1px solid;">2. Líneas de código efectivas (LOC)</td>
      <td style="border: 1px solid;">____ líneas</td>
      <td style="border: 1px solid;">____ líneas</td>
      <td style="border: 1px solid;">(Contar líneas excluyendo comentarios y comparar boilerplate)</td>
    </tr>
    <tr>
      <td style="border: 1px solid;">3. Manejo del Estado (State)</td>
      <td style="border: 1px solid;">Archivo <code>terraform.tfstate</code></td>
      <td style="border: 1px solid;">Metadatos de Stack local en <code>~/.pulumi</code></td>
      <td style="border: 1px solid;">(Comparar facilidad para inspeccionar qué recursos existen)</td>
    </tr>
    <tr>
      <td style="border: 1px solid;">4. Validación de variables y tipos</td>
      <td style="border: 1px solid;">Bloque <code>validation { condition = ... }</code></td>
      <td style="border: 1px solid;">Lógica en Python (<code>if ... raise ValueError</code>)</td>
      <td style="border: 1px solid;">(¿Cuál detecta errores más rápido y con mensajes más claros?)</td>
    </tr>
    <tr>
      <td style="border: 1px solid;">5. Detección y corrección de Drift</td>
      <td style="border: 1px solid;"><code>terraform plan</code></td>
      <td style="border: 1px solid;"><code>pulumi preview --refresh</code></td>
      <td style="border: 1px solid;">(Explicar la reacción de cada herramienta al borrar el contenedor)</td>
    </tr>
    <tr>
      <td style="border: 1px solid;">6. Multiplicidad y ciclos</td>
      <td style="border: 1px solid;">Meta-argumento <code>count</code> / <code>for_each</code></td>
      <td style="border: 1px solid;">Bucle estándar <code>for</code> en listas Python</td>
      <td style="border: 1px solid;">(¿Qué sintaxis resulta más legible para crear 10 réplicas?)</td>
    </tr>
    <tr>
      <td style="border: 1px solid;">7. Ecosistema de Linters / Shift-Left</td>
      <td style="border: 1px solid;"><code>terraform fmt</code>, <code>terraform validate</code></td>
      <td style="border: 1px solid;"><code>ruff</code>, <code>flake8</code></td>
      <td style="border: 1px solid;">(Comparar velocidad de chequeo en el pipeline de CI)</td>
    </tr>
  </tbody>
</table>

## 7.2 Evidencias del Experimento de Drift
(Pegar aquí los fragmentos de terminal donde Terraform y Pulumi detectaron la eliminación manual del contenedor)

## 7.3 Conclusión Arquitectónica
(Responder en 2 párrafos: Si tuvieran que desplegar una arquitectura de microservicios en una empresa donde todos los desarrolladores son de Python pero no saben DevOps, ¿cuál herramienta elegirían y qué precauciones tomarían?)
