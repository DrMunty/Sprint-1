# **L'Arquitectura de les Interfícies Web Modernes: Integritat Semàntica, Maquetació Fluida i Accessibilitat Universal**

L'evolució de les tecnologies web ha passat d'una preocupació purament visual a una èmfasi sofisticada en la semàntica estructural, l'optimització del rendiment i l'accés inclusiu. Aquest informe analitza els fonaments tècnics i les estratègies arquitectòniques essencials per al desenvolupament d'interfícies web modernes, abordant la convergència de l'HTML5 semàntic, els sistemes avançats de maquetació CSS i la implementació de patrons de disseny accessibles i adaptatius.

## **El Paradigma Semàntic: Més enllà del Contenidor Genèric**

El canvi fonamental de les maquetacions genèriques basades en l'element \<div\> cap a estructures semàntiques que utilitzen etiquetes com \<header\>, \<nav\> i \<article\> representa la pedra angular de l'accessibilitat web moderna i la llegibilitat per a màquines.1 Històricament, el web depenia dels elements no semàntics \<div\> i \<span\> per agrupar contingut, utilitzant noms de classe i identificadors per proporcionar pistes contextuals als desenvolupadors. Tanmateix, aquestes pistes són invisibles per als navegadors i les tecnologies de suport. La introducció d'elements semàntics HTML5 va establir un vocabulari estandarditzat que descriu la intenció i el propòsit dels blocs de contingut.1  
Per als usuaris que depenen de lectors de pantalla, les etiquetes semàntiques serveixen com a punts de referència (*landmarks*) crítics per a la navegació. Les tecnologies de suport analitzen el Model d'Objectes del Document (DOM) per construir un arbre d'accessibilitat, que proporciona una representació simplificada de la jerarquia estructural de la pàgina.2 Quan un desenvolupador utilitza \<header\> o \<nav\> en lloc d'un \<div\> amb estils, el navegador mapeja automàticament aquests elements a rols de referència ARIA (*Accessible Rich Internet Applications*), com banner o navigation.2 Els usuaris de lectors de pantalla poden llavors invocar comandes especialitzades per saltar entre aquests punts de referència, evitant contingut redundant i arribant directament al contingut principal.1  
L'element \<article\> exemplifica la profunditat de la intenció semàntica, identificant una composició autònoma que es pot distribuir o reutilitzar de manera independent, com una entrada de blog o una notícia.1 En definir aquests límits, el marcatge permet que el programari identifiqui amb precisió regions específiques d'una pàgina, assegurant que el context es conservi en diversos entorns de visualització.1

| Element Semàntic | Mapeig al Rol ARIA | Propòsit Principal i Valor d'Accessibilitat |
| :---- | :---- | :---- |
| \<header\> | banner | Defineix contingut introductori; proporciona un punt de referència global. |
| \<nav\> | navigation | Denota un bloc de navegació; permet oferir dreceres al menú de navegació. |
| \<main\> | main | Identifica el contingut principal; permet la funcionalitat de "saltar al contingut". |
| \<article\> | article | Agrupa contingut autònom; senyala un bloc d'informació independent. |
| \<section\> | region | Representa un agrupament temàtic; si té etiqueta, crea una regió cercable. |
| \<footer\> | contentinfo | Conté metadades/copyright; identifica la regió terminal del document. |

## **Dinàmica Fluida en la Navegació: Flexbox i la Lògica de l'Espaiat**

La navegació adaptativa continua sent un dels reptes més visibles en l'enginyeria d'interfícies. El sistema Flexbox (*Flexible Box Layout*) proporciona un mecanisme robust per crear menús que s'adapten a les dimensions de la finestra visual (*viewport*). Un requisit arquitectònic comú és un menú que es mostri horitzontalment en pantalles grans i passi a una pila vertical en dispositius mòbils. Això s'aconsegueix manipulant la propietat flex-direction.3 Per defecte, un contenidor flex disposa els seus fills en una fila horitzontal (flex-direction: row). Mitjançant consultes multimèdia (*media queries*), els desenvolupadors poden pivotar aquest eix cap a una columna vertical (flex-direction: column) per a finestres més estretes.3  
Un avenç significatiu en el CSS modern és l'adopció de la propietat gap dins de Flexbox. Històricament, l'espaiat entre elements es gestionava mitjançant declaracions manuals de margin. Tanmateix, els marges en elements flex sovint requerien solucions complexes, com l'ús del selector :last-child o marges negatius al contenidor pare, per evitar espais no desitjats a les vores de la maquetació.3 La propietat gap ofereix una alternativa declarativa que defineix l'espai exclusivament *entre* els elements, ignorant automàticament els límits exteriors del contenidor.3  
La superioritat de gap sobre els marges manuals arrela en la seva lògica interna: mentre que els marges són propietats dels elements fills, gap és una propietat del contenidor pare, centralitzant el control de la maquetació.3 Això redueix el deute tècnic i elimina l'efecte de "doble espaiat" que es produeix quan els marges adjacents s'encavalquen. A més, gap actua com una separació mínima que assegura que els elements mai estaran més a prop que el valor especificat.3

## **Inicialització Arquitectònica: CSS Reset versus Normalize.css**

Un obstacle important en el desenvolupament entre navegadors és la variació en els estils per defecte dels navegadors. Els desenvolupadors aborden això mitjançant dos mètodes principals: CSS Resets i llibreries de normalització. Un CSS Reset adopta un enfocament de "taula rasa", eliminant tots els estils definits pel navegador per establir un punt d'inici uniforme posant a zero els marges, els farciments (*padding*) i les vores.4  
En canvi, Normalize.css busca la consistència en lloc de l'eliminació.4 Preserva els valors per defecte útils del navegador mentre suavitza les inconsistències entre plataformes.5 Per exemple, Normalize.css assegura que elements com \<sup\> i \<sub\> funcionin de manera predictible en tots els navegadors, mentre que un Reset típic els faria visualment idèntics al text estàndard.5

| Estratègia | Objectiu Filosòfic | Impacte en Elements de Formulari |
| :---- | :---- | :---- |
| **CSS Reset** | Crear un "full en blanc" eliminant tots els estils de l'agent d'usuari. | Elimina totes les aparences; requereix estils complets des de zero. |
| **Normalize.css** | Mantenir valors útils i assegurar consistència entre navegadors. | Corregeix errors (ex: herència de font) i garanteix una base uniforme. |

Per a un projecte modern, l'elecció depèn del nivell de control desitjat. Un CSS Reset és ideal per a dissenys altament personalitzats, mentre que Normalize.css es prefereix per a projectes que volen aprofitar els comportaments estàndard del navegador.4 Molts desenvolupadors actuals opten per un enfocament híbrid, utilitzant un "Modern Reset" que combina el millor d'ambdós mons.6

## **Lògica de la Finestra Visual: Consultes Multimèdia i Escalat d'Arrel**

L'orquestració d'una maquetació adaptativa requereix una comprensió de la lògica de les *media queries*. La diferència entre min-width i max-width és fonamental: min-width és el motor del disseny *Mobile-first*, activant-se quan la finestra té *almenys* l'amplada especificada, mentre que max-width s'utilitza en enfocaments *Desktop-first*.7  
Per implementar un contenidor que ocupi el 90% de la finestra en mòbil i el 70% en escriptori utilitzant unitats rem, cal realitzar un escalat de la mida de font de l'arrel (html). La unitat rem és relativa a la mida de font de l'element arrel.9 Ajustant la mida de font de l'arrel mitjançant *media queries*, els desenvolupadors poden escalar tota una maquetació de manera proporcional.9

CSS

/\* Enfocament Mobile-first \*/  
html { font-size: 100%; } /\* Generalment 16px \*/

.container {  
  width: 90vw; /\* 90% de l'amplada de la finestra \*/  
  margin-inline: auto;  
}

@media (min-width: 64rem) { /\* Breakpoint per a escriptori (\~1024px) \*/  
 .container {  
    width: 70vw; /\* 70% de l'amplada de la finestra \*/  
  }  
}

## **El Paradigma Mobile-First: Rendiment i Priorització de Contingut**

El disseny *Mobile-first* comença dissenyant per a l'entorn més restringit i després millora progressivament la maquetació per a pantalles més grans.11 Això obliga a centrar-se en el contingut essencial i en el rendiment, evitant la càrrega d'actius innecessaris que sovint es produeix en el disseny *Desktop-first* (on s'amaguen elements mitjançant display: none però es descarreguen igualment).7  
Les estratègies clau inclouen l'ús d'elements centrats en el tacte (zones tàctils més grans) i l'evitació d'interaccions basades en el pas del ratolí (*hover*), que no funcionen en dispositius tàctils.12

## **Semàntica Visual: El Rol Crític del Text Alternatiu**

L'atribut alt és vital per oferir informació visual als usuaris de lectors de pantalla.13 El seu principi clau és el context: l'alternativa textual ha de proporcionar la mateixa informació o funció que la imatge.13

* **Imatges Informatives:** Aporten significat i requereixen una descripció breu i precisa a l'atribut alt.13  
* **Imatges Decoratives:** Han de ser ignorades utilitzant un atribut alt buit (alt="") per evitar la sobrecàrrega cognitiva.16

Exemple:  
\<img src="grafic.png" alt="Gràfic de barres que mostra un augment del 15% en vendes."\> (Informativa)  
\<img src="separador.png" alt=""\> (Decorativa)

## **Enginyeria de Formularis: Semàntica i Integració ARIA**

L'estructuració de formularis complexos requereix els elements \<fieldset\> i \<legend\> per garantir que els lectors de pantalla identifiquin correctament les relacions entre grups de camps.17 Un \<fieldset\> actua com a contenidor i el \<legend\> proporciona un nom accessible per a aquest grup.17  
Si no es pot utilitzar \<fieldset\>, es pot recórrer al rol role="group" i l'atribut aria-labelledby per associar el grup amb un títol o etiqueta existent.17  
Exemple amb ARIA:

HTML

\<div role="group" aria-labelledby="titol-grup"\>  
  \<p id="titol-grup"\>Preferències de contacte:\</p\>  
  \<input type="checkbox" id="email"...\> \<label for="email"\>Email\</label\>  
\</div\>

## **Arquitectura Bidimensional: CSS Grid i Accessibilitat**

CSS Grid proporciona un sistema bidimensional que separa la maquetació visual de l'ordre de la font del document, permetent transformacions complexes sense trencar l'accessibilitat.20 La propietat grid-template-areas permet definir un "mapa" visual de la maquetació, millorant la llegibilitat del codi.22  
L'ús de la funció clamp() per a l'espaiat (gap: clamp(1rem, 5vw, 2.5rem)) assegura que l'espai entre elements sigui adaptatiu i mantingui una estètica equilibrada en qualsevol dispositiu.24

## **Contrast i Solucions CSS Modernes**

El CSS modern ofereix eines com la propietat accent-color, que permet aplicar colors de marca als controls de formulari natius (caselles, ràdios, etc.) de manera accessible.26 El navegador calcula automàticament el color de l'indicador per garantir un contrast suficient seguint les pautes WCAG 2.1.27  
WCAG 2.1 exigeix una ràtio mínima de 3:1 per a components d'interfície d'usuari i objectes gràfics.28

## **Direcció d'Art: L'Element \<picture\>**

L'element \<picture\> permet la "direcció d'art", servint diferents versions d'una imatge segons el context (ex: una versió vertical per a mòbil i una panoràmica per a escriptori).30 L'atribut alt es defineix a l'etiqueta \<img\> interna com a única font de veritat per al significat de la imatge.31

## **Temes i Preferències: prefers-color-scheme**

El mode fosc s'implementa amb la consulta prefers-color-scheme i variables CSS.32 Per mantenir el contrast de manera dinàmica, es poden utilitzar ajustos amb calc() sobre valors HSL o la funció light-dark().34  
A més, l'ús de :focus-visible assegura que els usuaris de teclat tinguin un feedback visual clar, millorant l'accessibilitat sense afectar l'estètica per als usuaris de ratolí.26

#### **Obras citadas**

1. Semantic HTML5 Elements Explained \- freeCodeCamp, fecha de acceso: mayo 3, 2026, [https://www.freecodecamp.org/news/semantic-html5-elements/](https://www.freecodecamp.org/news/semantic-html5-elements/)  
2. ARIA Roles Explained: A Practical Guide for Web Developers \- Level Access, fecha de acceso: mayo 3, 2026, [https://www.levelaccess.com/blog/aria-roles-explained-a-practical-guide-for-web-developers/](https://www.levelaccess.com/blog/aria-roles-explained-a-practical-guide-for-web-developers/)  
3. A Complete Guide to CSS Flexbox | CSS-Tricks, fecha de acceso: mayo 3, 2026, [https://css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)  
4. Difference between reset vs normalize CSS \- GeeksforGeeks, fecha de acceso: mayo 3, 2026, [https://www.geeksforgeeks.org/css/difference-between-reset-vs-normalize-css/](https://www.geeksforgeeks.org/css/difference-between-reset-vs-normalize-css/)  
5. What is the difference between Normalize.css and Reset CSS? \- Stack Overflow, fecha de acceso: mayo 3, 2026, [https://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css](https://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css)  
6. Unintended Consequences of CSS Resets and Normalization \- PixelFreeStudio Blog, fecha de acceso: mayo 3, 2026, [https://blog.pixelfreestudio.com/unintended-consequences-of-css-resets-and-normalization/](https://blog.pixelfreestudio.com/unintended-consequences-of-css-resets-and-normalization/)  
7. Mobile-First vs Desktop-First: The Design Mistake 90% of Developers Still Make \- Medium, fecha de acceso: mayo 3, 2026, [https://medium.com/@manaswinisasmal5597/mobile-first-vs-desktop-first-the-design-mistake-90-of-developers-still-make-a5afebbbdeed](https://medium.com/@manaswinisasmal5597/mobile-first-vs-desktop-first-the-design-mistake-90-of-developers-still-make-a5afebbbdeed)  
8. Mobile First vs. Desktop First — Web Design \- Noble Desktop Blog, fecha de acceso: mayo 3, 2026, [https://blog.nobledesktop.com/learn/web-design/mobile-first-vs-desktop-first](https://blog.nobledesktop.com/learn/web-design/mobile-first-vs-desktop-first)  
9. Width set in rem not scaling responsively as expected \- Stack Overflow, fecha de acceso: mayo 3, 2026, [https://stackoverflow.com/questions/77382285/width-set-in-rem-not-scaling-responsively-as-expected](https://stackoverflow.com/questions/77382285/width-set-in-rem-not-scaling-responsively-as-expected)  
10. font-size CSS property \- MDN Web Docs, fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/font-size)  
11. What is Mobile First Design? \- GeeksforGeeks, fecha de acceso: mayo 3, 2026, [https://www.geeksforgeeks.org/websites-apps/mobile-first-design/](https://www.geeksforgeeks.org/websites-apps/mobile-first-design/)  
12. Mobile-First vs. Desktop-First: Which Approach is Right for Your Website? \- Spinutech, fecha de acceso: mayo 3, 2026, [https://www.spinutech.com/digital-agency-expertise/website-development-process/mobile-first-vs-desktop-first-which-approach-is-right-for-your-website/](https://www.spinutech.com/digital-agency-expertise/website-development-process/mobile-first-vs-desktop-first-which-approach-is-right-for-your-website/)  
13. Quick tip: Using alt text properly \- The A11Y Project, fecha de acceso: mayo 3, 2026, [https://www.a11yproject.com/posts/alt-text/](https://www.a11yproject.com/posts/alt-text/)  
14. Authoring Meaningful Alternative Text | Section508.gov, fecha de acceso: mayo 3, 2026, [https://www.section508.gov/create/alternative-text/](https://www.section508.gov/create/alternative-text/)  
15. An alt Decision Tree | Web Accessibility Initiative (WAI) \- W3C, fecha de acceso: mayo 3, 2026, [https://www.w3.org/WAI/tutorials/images/decision-tree/](https://www.w3.org/WAI/tutorials/images/decision-tree/)  
16. Image ALT Tag Tips for HTML \- Penn State | Accessibility, fecha de acceso: mayo 3, 2026, [https://accessibility.psu.edu/images/imageshtml/](https://accessibility.psu.edu/images/imageshtml/)  
17. Foundations: grouping forms with \`\` and \`\` \- TetraLogical, fecha de acceso: mayo 3, 2026, [https://tetralogical.com/blog/2025/01/31/foundations-fieldset-and-legend/](https://tetralogical.com/blog/2025/01/31/foundations-fieldset-and-legend/)  
18. Using the fieldset and legend elements \- Accessibility in government, fecha de acceso: mayo 3, 2026, [https://accessibility.blog.gov.uk/2016/07/22/using-the-fieldset-and-legend-elements/](https://accessibility.blog.gov.uk/2016/07/22/using-the-fieldset-and-legend-elements/)  
19. Fieldsets, Legends and Screen Readers again \- Vispero, fecha de acceso: mayo 3, 2026, [https://vispero.com/resources/fieldsets-legends-and-screen-readers-again/](https://vispero.com/resources/fieldsets-legends-and-screen-readers-again/)  
20. Grid layout and accessibility \- CSS \- MDN Web Docs, fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid\_layout/Accessibility](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Accessibility)  
21. CSS Grid Layout Module Level 1 \- W3C, fecha de acceso: mayo 3, 2026, [https://www.w3.org/TR/css-grid-1/](https://www.w3.org/TR/css-grid-1/)  
22. Grid template areas \- CSS \- MDN Web Docs, fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid\_layout/Grid\_template\_areas](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Grid_template_areas)  
23. CSS Grid and Flexbox: Complete Layout Reference 2026, fecha de acceso: mayo 3, 2026, [https://www.digitalapplied.com/blog/css-grid-flexbox-complete-layout-reference](https://www.digitalapplied.com/blog/css-grid-flexbox-complete-layout-reference)  
24. Making Color Usage Accessible | Section508.gov, fecha de acceso: mayo 3, 2026, [https://www.section508.gov/create/making-color-usage-accessible/](https://www.section508.gov/create/making-color-usage-accessible/)  
25. Container Query Units and Fluid Typography | Modern CSS Solutions, fecha de acceso: mayo 3, 2026, [https://moderncss.dev/container-query-units-and-fluid-typography/](https://moderncss.dev/container-query-units-and-fluid-typography/)  
26. accent-color \- CSS-Tricks, fecha de acceso: mayo 3, 2026, [https://css-tricks.com/almanac/properties/a/accent-color/](https://css-tricks.com/almanac/properties/a/accent-color/)  
27. Simplifying Form Styles With accent-color \- Smashing Magazine, fecha de acceso: mayo 3, 2026, [https://www.smashingmagazine.com/2021/09/simplifying-form-styles-accent-color/](https://www.smashingmagazine.com/2021/09/simplifying-form-styles-accent-color/)  
28. Color Contrast Checker | Free WCAG Testing Tool \- Level Access, fecha de acceso: mayo 3, 2026, [https://www.levelaccess.com/color-contrast-checker-new/](https://www.levelaccess.com/color-contrast-checker-new/)  
29. Understanding WCAG 2 Contrast and Color Requirements \- WebAIM, fecha de acceso: mayo 3, 2026, [https://webaim.org/articles/contrast/](https://webaim.org/articles/contrast/)  
30. HTML picture element \- MDN Web Docs \- Mozilla, fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/picture](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/picture)  
31. Relationship of grid layout to other layout methods \- CSS \- MDN Web Docs, fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid\_layout/Relationship\_with\_other\_layout\_methods](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Relationship_with_other_layout_methods)  
32. Adding Dark Mode via CSS Variables \- Reddit, fecha de acceso: mayo 3, 2026, [https://www.reddit.com/r/css/comments/124xwqx/adding\_dark\_mode\_via\_css\_variables/](https://www.reddit.com/r/css/comments/124xwqx/adding_dark_mode_via_css_variables/)  
33. Managing light and dark modes \- Accessibility Theme Builder, fecha de acceso: mayo 3, 2026, [https://a11y-theme-builder.finos.org/developers/managing-modes/](https://a11y-theme-builder.finos.org/developers/managing-modes/)  
34. light-dark() CSS function \- MDN Web Docs \- Mozilla, fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color\_value/light-dark](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color_value/light-dark)  
35. \[v4\] Improve the usage of CSS variables for dark/light mode · tailwindlabs tailwindcss · Discussion \#15083 \- GitHub, fecha de acceso: mayo 3, 2026, [https://github.com/tailwindlabs/tailwindcss/discussions/15083](https://github.com/tailwindlabs/tailwindcss/discussions/15083)  
36. Modern CSS Solutions, fecha de acceso: mayo 3, 2026, [https://moderncss.dev/](https://moderncss.dev/)