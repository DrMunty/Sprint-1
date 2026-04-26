# BEST PRACTICES RECOMMENDATIONS

Este documento está pensado para personas que empiezan desde cero.

> Ten en cuenta tambien esta documentación para que revises tu proyecto antes de entregar siempre https://github.com/IT-Academy-BCN/ita-sprint0/blob/main/instruccions_alumnes/bones_practiques.md


## 1) Naming classes & id

**Reglas simples:**
- Usa nombres en minúsculas y con guiones: `menu-principal`, `boton-primario`.
- Evita nombres genéricos como `caja` o `rojo`.
- Que el nombre describa la función, no el color: mejor `boton-principal` que `boton-azul`.

**Sugerencias:**
- Para clases, usa sustantivos o funciones: `card`, `hero`, `lista-productos`.
- Para id, úsalo solo si es único (uno por página) y realmente necesario.

**Ejemplo:**
```html
<section class="hero">
  <h1 class="hero__titulo">Bienvenido</h1>
</section>
```
> Si prefieres hacer uso de un standar de naming conventions, siempre puedes usar [BEM](https://en.bem.info/methodology/) 

## 2) Semantic Tags

Las etiquetas semánticas dicen qué es cada parte de la página.

**Ejemplos de etiquetas semánticas útiles:**
- `header`: cabecera principal
- `nav`: menú de navegación
- `main`: contenido principal
- `section`: sección de contenido
- `article`: contenido independiente
- `aside`: contenido lateral
- `footer`: pie de página

**Por qué importa:**
- Ayuda a los lectores de pantalla.
- Facilita el mantenimiento del código.
- Mejora el SEO.

## 3) Accesibility: ARIA y attributes

**Primero HTML, después ARIA.**
Si existe una etiqueta HTML correcta, úsala antes de añadir ARIA.

**Buenas prácticas básicas:**
- Imágenes informativas deben tener `alt`.
- Botones deben ser `button`, no `div`.
- Formularios deben tener `label` asociado.

**Ejemplos:**
```html
<img src="assets/img/logo.png" alt="Logo de la empresa" />

<button type="button">Enviar</button>

<label for="email">Correo</label>
<input id="email" type="email" />
```

**Cuándo usar ARIA:**
- Cuando no hay una etiqueta semántica adecuada.
- Para mejorar la información que reciben lectores de pantalla.

**Ejemplo:**
```html
<div role="alert">Mensaje de error</div>
```

## 4) WCAG (Web Content Accessibility Guidelines)

Son reglas internacionales para crear webs accesibles.

**Ideas clave (muy simples):**
- Contraste suficiente entre texto y fondo.
- Navegación con teclado.
- Textos claros y legibles.

## 5) Checking semantic HTML and design fidelity

**Herramientas recomendadas:**
- Validador HTML de W3C: https://validator.w3.org/
- Lighthouse (en Chrome DevTools)
- WAVE: https://wave.webaim.org/
- Perfect pixel (en Chrome DevTools)


## 6) About the project - README.md

El README que recibes en este boilerplate es **orientativo**, no es el definitivo.

**Qué debes hacer:**
- Léelo para entender la estructura del proyecto.
- **Personalízalo**: actualiza la información con detalles de tu proyecto.
- Añade tus propias instrucciones si necesitas algo especial.
- Explica qué hace tu proyecto, cómo usarlo, y cualquier cosa que creas importante.

**Un buen README incluye:**
- Título y descripción breve.
- Cómo descargar y usar el proyecto.
- Tecnologías utilizadas.
- Créditos o notas personales.

**Recuerda:** El README es la puerta de entrada a tu proyecto. Dedica tiempo a hacerlo claro y útil.

> Ten en cuenta esta documentación para que revises tu proyecto antes de entregar siempre https://github.com/IT-Academy-BCN/ita-sprint0/blob/main/instruccions_alumnes/bones_practiques.md


## 7) Checklist para revisar tu página
Te recomendamos que siempre mires la guía de buenas practicas https://github.com/IT-Academy-BCN/ita-sprint0/blob/main/instruccions_alumnes/bones_practiques.md

Pero puedes usar esta lista antes de presentar este proyecto pequeño:

- [ ] ¿Tengo un `<!DOCTYPE html>` al inicio?
- [ ] ¿Mi HTML tiene `<html>`, `<head>` y `<body>`?
- [ ] ¿El `<title>` describe mi página?
- [ ] ¿Todas mis imágenes tienen `alt`?
- [ ] ¿Todos mis botones usan `<button>`, no `<div>`?
- [ ] ¿Mis clases tienen nombres descriptivos?
- [ ] ¿Uso etiquetas semánticas (`header`, `nav`, `main`, `footer`)?
- [ ] ¿Mis formularios tienen `<label>` asociadas?
- [ ] ¿El HTML se valida sin errores en W3C?
- [ ] ¿La página se ve bien en móvil?
- [ ] ¿Pasé la página por Lighthouse?
- [ ] ¿Tengo un `.gitignore` con archivos irrelevantes?
- [ ] ¿Usé ramas en Git, no programé en `main`?
- [ ] ¿tengo el README.md con todas las instrucciones y documentación necesaria?


## 8) Consejos finales

- Mantén tu HTML limpio y ordenado.
- Un elemento = una responsabilidad.
- Controla el uso de comentarios.
- Usa siempre Git, aunque sea un proyecto pequeño.
- Intenta desplegar el proyecto con GitHub Pages.
- No tengas prisa: la calidad es más importante que la velocidad.

---


