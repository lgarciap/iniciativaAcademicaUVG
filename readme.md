# 📘 Plantilla de programas de iniciativa académica en LaTeX — Universidad del Valle de Guatemala

Esta plantilla permite crear programas institucionales de la **Facultad de Ingeniería de la Universidad del Valle de Guatemala (UVG)**.  
El proyecto está dividido en archivos modulares para facilitar su edición, comprensión y mantenimiento.

---

## 🎯 Propósito

Facilitar la generación de programas académicos normalizados, con:
- Tablas estructuradas (identificación, competencias, evaluación, cronograma).
- Variables centralizadas para cambiar información del curso una sola vez.
- Diseño limpio, claro y con formato institucional.

---

## ⚙️ Cómo usar la plantilla

### 1️⃣ Clona o descarga este repositorio
```bash
git clone https://github.com/tuusuario/plantilla-silabo.git
```

### 2️⃣ Compila el archivo principal
Compila **`main.tex`** con **XeLaTeX** (no con pdfLaTeX).  
Esto garantiza compatibilidad con la fuente Calibri.

- En VS Code → selecciona receta `latexmk (xelatex)`
- O en terminal:
  ```bash
  xelatex main.tex
  ```

El resultado será `main.pdf` — tu sílabo completo.

---

## 🧩 Estructura del proyecto

```
├── main.tex             # Archivo principal: ensambla todo el sílabo.
├── variables.tex        # Información editable del curso.
├── estructuras.tex      # Comandos y tablas reutilizables.
├── competencias.tex     # Competencias genéricas y específicas.
├── evaluacion.tex       # Tablas de evaluación por competencia.
├── cronograma.tex       # Cronograma del curso.
├── encabezado.tex       # Encabezado institucional con logo UVG.
└── README.md            # Guía de uso (este documento).
```

---

## 🧱 Instrucciones por archivo

### 📄 `main.tex`
Archivo **principal** que arma todo el documento.  
Aquí **no se edita contenido**, solo se controla el orden de las secciones.

```latex
\input{variables}     % Carga información general
\input{estructuras}   % Carga las macros de tablas y comandos
\input{encabezado}    % Define el encabezado del documento
```

Cada sección del sílabo se inserta con:
```latex
\section*{2. Competencias a desarrollar}
\input{competencias}  % Llama el archivo competencias.tex
```

> 💡 **Si una tabla aparece antes del título**, agrega `\FloatBarrier` antes de la `\section*`.

---

### 🧾 `variables.tex`
Aquí editas **la información básica del curso**:

```latex
\newcommand{\facultad}{Facultad de Ingeniería}
\newcommand{\departamento}{Ciencia de la Computación y TI}
\newcommand{\nombreCurso}{Introducción a la Programación}
\newcommand{\codigoCurso}{CC1001}
\newcommand{\creditos}{4}
\newcommand{\anio}{2025}
\newcommand{\ciclo}{1}
```

Además, define **tablas y secciones reutilizables**:
- `\metodologiasActivas` → Tabla de metodologías sugeridas.  
- `\listaDocentes` → Tabla de docentes.  
- `\bibliografia` → Bibliografía dentro de un cuadro.  
- `\responsabilidadesEstudiantes` y `\recomendacionesEstudiantes` → Listas con estilo uniforme.

> ✏️ **Edita este archivo** cuando cambien los datos del curso, pero **no modifiques las estructuras**.

---

### 🧠 `competencias.tex`
Contiene las competencias **genéricas y específicas**.

#### 🟩 Instrucciones de uso
— Sección 2.2.1 Específicas de la carrera
1. Elimina las competencias que **no apliquen** al curso.  
2. Mantén máximo **3 competencias genéricas**.  
3. Usa numeración manual (`[1.]`, `[2.]`, etc.) para que **no se reordenen automáticamente**.  
4. Las listas están divididas en dos columnas:

```latex
\begin{multicols}{2}
\begin{enumerate}[label={}]
  \item[1.] Piensa de manera crítica y analítica.
  \item[2.] Se comunica con efectividad.
  ...
\end{enumerate}
\end{multicols}
```
> 💡 Usa `\setlength{\columnsep}{1.5cm}` para ajustar el espacio entre columnas.

— Sección 2.2.1 Específicas de la carrera

Esta subsección relaciona las **competencias específicas de la carrera** con las **subcompetencias que desarrolla el curso**.  
Por ejemplo, muestra cómo cada competencia del curso contribuye a las competencias del perfil profesional.

#### 🧩 Instrucciones de uso
1. **No modifique el formato de la tabla**; solo edita el texto dentro de las celdas.  
2. Cada fila debe contener:
   - La **competencia específica de la carrera (CE)**, tomada del plan de estudios.  
   - La **subcompetencia** del curso que contribuye a desarrollarla.  
3. Si tu curso no contribuye a alguna competencia CE, puedes **eliminar esa fila**.  
4. Si tu curso contribuye a más competencias, puedes **duplicar una fila** manteniendo el formato.
---

### 🧮 `evaluacion.tex`
Define la **tabla de criterios de evaluación por competencia**.

#### 🟦 Instrucciones de uso
1. Edita los criterios y productos dentro de las celdas.  
2. Los porcentajes deben sumar **100%**.  
3. En  la columna de competencias debe ponerse cuales de las competencias se están evaluando en los productos y desempeños. Puede usar el número de la competencia. 

Ejemplo:
```latex
\begin{tabularx}{\textwidth}{|X|p{4cm}|c|}
  \hline
  \multicolumn{3}{|l|}{$\bullet$ \textbf{Competencia:}} \\ \hline
  \textbf{Criterios de evaluación} & \textbf{Productos y desempeños} & \textbf{\%} \\ \hline
  ...
\end{tabularx}
```

> 💡 Usa `\begin{table}[H]` (con `\usepackage{float}`) para forzar que la tabla aparezca **debajo del título**.

---

### 📅 `cronograma.tex`
Sección para detallar el **cronograma del curso**.

#### 🟨 Instrucciones de uso
1. Debes listar la competencia específica, la semama y la forma en la que se evaluará dicha competencia.  
2. Usa `tabularx` para mantener el ancho uniforme.  
3. Si el texto es largo, ajusta con `p{4cm}` o similar.  


---

### 📚 `bibliografía`
Encerrada en un **cuadro** para mantener formato institucional:

```latex
\noindent\fbox{%
  \parbox{\textwidth}{%
    \begin{enumerate}[label=\Alph*.]
      \item Canvas: \url{https://uvg.instructure.com}
      ...
    \end{enumerate}
  }
}
```

> 💡 Agrega nuevas fuentes en formato APA y usa `\url{}` para los enlaces.

---


## 🧩 Consejos generales de edición

| Necesidad | Solución |
|------------|-----------|
| Forzar que una tabla quede justo debajo del título | Usa `[H]` o quita el entorno `table` |
| Aumentar espacio entre columnas | `\setlength{\columnsep}{1cm}` |
| Aumentar espacio dentro de celdas | `\renewcommand{\arraystretch}{1.2}` |
| Evitar que las listas cambien numeración | Usa `enumerate[label={}]` y numera manualmente |
| Prevenir que flotantes se muevan | Inserta `\FloatBarrier` antes de cada sección |
| Espacio extra entre filas | `\setlength{\extrarowheight}{5pt}` |

---

## 📄 Compilación paso a paso

1. **Abrir el proyecto** en VS Code o TeXstudio.  
2. **Seleccionar motor:** `XeLaTeX`.  
3. **Compilar:**  
   - En VS Code: `Ctrl+Shift+P → LaTeX Workshop: Build with latexmk (xelatex)`  
   - O en terminal:  
     ```bash
     xelatex main.tex
     ```
4. Verifica el PDF generado: `main.pdf`.

---

## 👩‍💻 Autores

**Lynette García** y **Erick Marroquín**  
Facultad de Ingeniería — Universidad del Valle de Guatemala

---

## 🪶 Licencia

Este proyecto se distribuye bajo la licencia **MIT**.  
Puedes modificarlo, compartirlo y adaptarlo libremente citando la fuente original.
