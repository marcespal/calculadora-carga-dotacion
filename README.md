# Calculadora de carga y dotación de personal

Herramienta de un solo archivo HTML para levantar cargas de trabajo y contrastar
escenarios de dotación en organizaciones deportivas (clubes con plantel profesional
y categorías formativas). Funciona sin servidor, sin instalación y sin conexión:
se abre el archivo en el navegador y todo el cálculo ocurre en la máquina de quien
la usa.

## Qué resuelve

La pregunta típica —«¿cuántas personas necesita este cargo?»— casi siempre se
responde con una sola fuente: o el inventario de actividades, o un ratio de
referencia, o la intuición del jefe de área. Esta calculadora obliga a sostener el
número por **tres vías distintas y a mostrar cuándo no coinciden**:

1. **Carga real** — inventario de actividades con minutos, frecuencia y multiplicador
   (por categoría, por jugador atendido, por partido, por bloque de entrenamiento),
   convertido a horas al mes y luego a FTE contra una jornada disponible neta.
2. **Piso operativo por simultaneidad** — si tres categorías entrenan a la misma
   hora en tres sedes distintas, hacen falta tres personas aunque las horas sumen
   una. El motor arma la malla de bloques (día × franja × sede × categoría) y
   calcula ese mínimo aparte de las horas.
3. **Ratios externos** — biblioteca de referencias con su tipo de sustento
   declarado: `NORMA` (exigible), `BENCHMARK` (dato de mercado), `RECOMENDACION`,
   `DERIVADO`, `INTERNO` y `ASPIRACIONAL` (criterio propio sin respaldo publicado).
   La distinción es deliberada: un requisito reglamentario y una aspiración interna
   no pueden pesar igual en una decisión de contratación.

El resultado no es un número único sino la brecha entre los tres, que es donde
está la conversación real.

## Lo que hace distinto

- **Jornada disponible, no jornada nominal.** 40 horas semanales no son 40 horas
  productivas: la herramienta descuenta vacaciones, feriados, ausentismo, traslado
  entre sedes y semanas inactivas antes de dividir.
- **Redundancia de cobertura separada de la carga.** El factor de respaldo (para
  que la ausencia de una persona no deje un bloque descubierto) se aplica solo a
  los cargos que sostienen presencia de campo, no a los administrativos.
- **Análisis parcial visible.** Si hay actividades excluidas del cálculo, la
  cabecera lo anuncia de forma permanente. Un resultado filtrado leído como
  definitivo es el peor desenlace posible de un estudio de cargas.
- **Oportunidades de mejora incorporadas al inventario.** Cada actividad puede
  llevar una propuesta (digitalizar, delegar, eliminar, estandarizar) con su
  ahorro estimado y su esfuerzo, y el sistema agrega el saldo: si el 60 % del
  ahorro es digitalización, el programa de mejora ya tiene nombre y dueño.
- **Naturaleza de la actividad.** Clasificación en tres bloques —directo (con el
  jugador), técnico y estructural— con sugerencia automática por nombre. Lo
  ambiguo queda sin clasificar a propósito y se declara como tal en lugar de
  repartirse.
- **Trazabilidad del número.** Cada cifra de horas se explica en texto: minutos ×
  frecuencia × multiplicador, con la fórmula desplegada en pantalla.
- **Metodología dentro de la herramienta.** Una pestaña documenta el orden del
  levantamiento, quién entrega cada insumo y cuál es el error frecuente en cada
  paso.

## Cómo se usa

1. Abre `calculadora-carga-dotacion.html` en Chrome o Edge (recomendado: usan la
   File System Access API y permiten vincular el archivo de trabajo en disco).
2. Pestaña **Estructura**: registra sedes, canchas, franjas horarias y categorías
   con su plantel y sus días de entrenamiento.
3. Pestañas **Cargos** y **Dotación actual**: ajusta el catálogo de cargos, el modo
   de cobertura (dedicada, compartida o ninguna) y reparte las personas que hoy
   existen por categoría.
4. Pestaña **Actividades**: levanta el inventario cargo por cargo. Se puede
   imprimir una hoja de revisión para que cada ocupante valide sus tiempos.
5. Pestañas **Ratios** y **Resultados**: elige la referencia externa de cada cargo
   y lee la brecha por las tres vías.

El estado se guarda en el navegador y, si vinculas un archivo, se escribe en un
JSON en disco que puedes versionar y compartir. `Descargar` exporta ese mismo JSON;
`Cargar copia` lo restaura.

## Datos

El archivo se publica **sin datos de ningún levantamiento**: sedes, categorías,
asignaciones y actividades arrancan vacías, y el catálogo de cargos viene con la
dotación en cero. Lo que sí trae cargado es la biblioteca de ratios con su fuente
y su enlace (FEF, UEFA, EFL, The FA, Premier League, NSCA, UKSCA y literatura
académica citada), porque son referencias públicas y verificables.

Las referencias con tipo `INTERNO` o `ASPIRACIONAL` son criterios de trabajo sin
respaldo externo publicado y están marcadas como tales: revísalas o elimínalas
antes de usarlas para sostener una decisión.

## Requisitos

Un navegador moderno. Nada más: sin dependencias, sin CDN, sin backend. El vínculo
con un archivo en disco requiere Chrome o Edge; en otros navegadores la herramienta
funciona igual, guardando en el navegador y exportando JSON a mano.
