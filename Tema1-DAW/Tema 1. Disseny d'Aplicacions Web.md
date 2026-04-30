# **L'ecosistema integrat del disseny de producte modern: de la lògica de baixa fidelitat als sistemes de disseny empresarials**

El panorama digital contemporani exigeix un enfocament altament sofisticat per al desenvolupament de productes, on les fronteres tradicionals entre el disseny i l'enginyeria es desdibuixen cada cop més per l'aparició de sistemes de disseny robustos i eines col·laboratives. A mesura que les organitzacions s'esforcen per aconseguir una escalabilitat ràpida i una consistència multiplataforma, les metodologies utilitzades per conceptualitzar, modelar i documentar les interfícies d'usuari han evolucionat cap a una disciplina rigorosa. Aquest informe proporciona una anàlisi exhaustiva de les capes arquitectòniques del disseny modern, des de la lògica fundacional dels wireframes i el disseny atòmic fins a les complexitats tècniques de l'orquestració a Figma, els design tokens i la implementació de sistemes líders en la indústria com Material UI, Atlassian i Finastra.

## **Arquetips estructurals: Diferenciant Wireframes, Mockups i Prototips**

La progressió d'un producte digital des d'un concepte naixent fins a una interfície preparada per a la producció es categoritza per diferents fases de fidelitat. Cada fase serveix com una fita crítica en la presa de decisions, assegurant que els aspectes estructurals, visuals i funcionals de l'experiència de l'usuari es validin abans de destinar recursos significatius al desenvolupament.1

### **El plànol de la funcionalitat: Wireframes**

Un wireframe serveix com el plànol arquitectònic d'una aplicació digital. Es caracteritza per una baixa fidelitat visual, utilitzant habitualment tons d'escala de grisos, formes geomètriques simples i text de farciment per definir l'estructura esquelètica d'una interfície.3 L'objectiu principal del wireframing és establir l'arquitectura de la informació, la jerarquia del contingut i el flux de navegació sense la distracció d'elements estètics com el color, la tipografia o el branding.3  
En els fluxos de treball de disseny professional, el wireframing aborda preguntes fonamentals sobre la interacció de l'usuari: la intenció específica de l'usuari en una pantalla determinada i la lògica de la interacció posterior.6 En representar components complexos de la interfície d'usuari (UI) amb cercles per als avatars, caixes per a les targetes de dades i fletxes per a les transicions, els dissenyadors poden traçar el "flux d'usuari" —el camí seqüencial que segueix un usuari per completar una tasca—.6 Aquesta fase és essencial per identificar defectes de disseny de manera prematura, mitigant així el risc de revisions costoses durant la fase de codificació.6 A més, el wireframing permet considerar restriccions específiques per a mòbils, com la mida mínima de l'objectiu tàctil (de 44pt a 48dp) i les directrius específiques de les plataformes com les *Human Interface Guidelines* d'Apple o el *Material Design* d'Android.6

### **El model visual d'identitat: Mockups**

La transició de la lògica estructural d'un wireframe al refinament estètic d'un mockup representa un canvi significatiu en la fidelitat. Un mockup és una representació estàtica d'alta fidelitat del producte final que incorpora tota la carta gràfica, incloent colors, tipografia, imatges i branding.1 Mentre que els wireframes es centren en "com funciona", els mockups es centren en "com es veu".4  
Els mockups són indispensables per a la comunicació amb les parts interessades (*stakeholders*) i la validació de la marca. Proporcionen una vista prèvia realista del producte final esperat, permetent als clients i als membres de l'equip avaluar l'impacte visual i la ressonància emocional del disseny sense haver d'interpretar marcadors de posició abstractes.7 Per als desenvolupadors, el mockup actua com una guia visual definitiva, especificant valors exactes per a les mides dels botons, l'espaiat i l'alineació del disseny.5 La transició de wireframe a mockup sovint es compara amb el pas del plànol d'un edifici a un model arquitectònic acabat.4

### **La simulació de l'experiència: Prototips**

L'últim nivell de l'espectre de fidelitat és el prototip. A diferència dels wireframes i mockups estàtics, un prototip és una simulació interactiva que demostra el comportament operatiu de la interfície.4 Els prototips enllacen múltiples pantalles d'alta fidelitat mitjançant transicions i animacions, permetent als usuaris provar la usabilitat real del producte.5 Aquesta etapa és crítica per a la validació del producte, ja que permet als equips realitzar proves d'usabilitat i identificar possibles errors o punts de fricció en el recorregut de l'usuari abans d'escriure qualsevol línia de codi.4

| Atribut | Wireframe | Mockup | Prototip |
| :---- | :---- | :---- | :---- |
| **Nivell de fidelitat** | Baix | Alt | Alt |
| **Enfocament principal** | Estructura, Lògica, Jerarquia | Estètica, Branding, Detall UI | Interactivitat, Usabilitat, Flux |
| **Elements visuals** | Caixes, línies, escala de grisos | Color complet, tipografia, imatges | Animacions, transicions, variables |
| **Interactivitat** | Estàtic | Estàtic | Simulació funcional |
| **Fase de disseny** | Inicial (Ideació) | Mitjana (Disseny visual) | Final (Validació/Proves) |

4

## **La filosofia atòmica: Construint arquitectures de components escalables**

Per assolir l'escalabilitat requerida per les plataformes digitals modernes, els dissenyadors han deixat de dissenyar pàgines individuals en favor de la creació de sistemes de disseny complets. La metodologia predominant en aquest espai és el Disseny Atòmic (*Atomic Design*), introduït per Brad Frost el 2013\.9 Inspirat en la química, aquest marc proporciona una estructura jeràrquica per organitzar els components de la interfície d'usuari, assegurant que els sistemes siguin modulars, reutilitzables i fàcils de mantenir.11

### **Els cinc nivells de la jerarquia atòmica**

El Disseny Atòmic categoritza els elements de la interfície en cinc etapes diferents que treballen conjuntament per crear un tot cohesionat 9:

1. **Àtoms:** Els àtoms són els blocs bàsics de construcció de la interfície que no es poden desglossar més sense perdre la seva funcionalitat.9 En són exemples un botó individual, un camp d'entrada, una etiqueta o un codi hexadecimal de color específic. Individualment, els àtoms són abstractes, però defineixen els estils fundacionals de tot el sistema.9  
2. **Molècules:** Les molècules són grups d'àtoms units per realitzar una funció simple i específica.9 Per exemple, combinar un àtom d'entrada, un àtom d'etiqueta i un àtom de botó crea una molècula de "barra de cerca". Aquesta modularitat fomenta el Principi de Responsabilitat Única, on cada component fa una sola cosa bé.9  
3. **Organismes:** Els organismes són assemblatges complexos de molècules i àtoms que formen una secció diferenciada d'una interfície.9 Un organisme de "capçalera" podria incloure un àtom de logotip, una molècula de menú de navegació i una molècula de cerca. Els organismes proporcionen el context en què operen les molècules.9  
4. **Plantilles:** Les plantilles canvien l'enfocament de la construcció de components al disseny a nivell de pàgina. Defineixen l'estructura de contingut subjacent —com sistemes de quadrícula i col·locació d'organismes— sense la distracció del contingut final.9  
5. **Pàgines:** Les pàgines són l'etapa més tangible, on s'injecta contingut real a les plantilles per crear l'experiència final de l'usuari.9 Això permet als dissenyadors provar com el sistema gestiona les variables dinàmiques, com ara diferents longituds de text o relacions d'aspecte d'imatge.9

### **Impacte estratègic en l'escalabilitat i la reutilització**

El Disseny Atòmic servei com un marc estratègic que estableix un llenguatge compartit entre el disseny i el desenvolupament.9 En desglossar la interfície en parts reutilitzables, els equips poden mantenir un sistema unificat que creix amb les necessitats del producte.10 Els canvis realitzats en un àtom —per exemple, actualitzar un color de marca principal— es propaguen automàticament per cada molècula, organisme i plantilla que utilitzi aquest àtom, reduint significativament la redundància i el risc d'inconsistències visuals.9 Aquest enfocament modular garanteix que les empreses centrades en el disseny puguin aconseguir una major eficiència i un temps de llançament al mercat més ràpid.11

## **La constitució visual: Elements essencials de la carta gràfica**

Una carta gràfica, o manual d'identitat de marca, funciona com la guia definitiva per mantenir una imatge de marca coherent en tots els mitjans de comunicació.12 Assegura que la identitat visual sigui uniforme, tant si apareix en una aplicació mòbil com en una tanca publicitària física o un informe corporatiu.12

### **Pilars fonamentals d'una carta gràfica**

Una identitat gràfica robusta es construeix sobre diversos pilars clau que defineixen la signatura visual de la marca 12:

* **Logotips i signes gràfics:** El logotip és el principal identificador de la marca. La carta especifica les seves variacions, els marges de seguretat (l'espai buit necessari al seu voltant) i els usos prohibits per evitar distorsions.12 També inclou elements gràfics addicionals com icones i patrons que reforcen el vocabulari visual de la marca.12  
* **Paleta de colors:** Els colors s'escullen pel seu impacte psicològic i la seva capacitat per evocar emocions específiques.12 La carta defineix colors primaris i secundaris amb precisió tècnica utilitzant codis HEX (web), RGB (digital) i CMYK/Pantone (impressió) per garantir la consistència en diferents maquinari i suports.14  
* **Tipografia:** L'elecció de les famílies de fonts reflecteix la personalitat de la marca.12 Les directrius dicten com i on utilitzar tipografies específiques per a encapçalaments, text corporal i subtítols, incloent regles per als gruixos de lletra, l'interlineat i opcions de reserva per a l'accessibilitat web.14  
* **Imatgeria i to visual:** Aquesta secció descriu la direcció artística per a la fotografia i les il·lustracions.14 Defineix composicions acceptables, temes i fins i tot el to emocional que les imatges han de transmetre.13  
* **Maquetació i sistemes de quadrícula:** Regles precises per posicionar elements, formats de document i quadrícules de disseny asseguren la continuïtat visual.14 Això inclou l'ús de l'espai en blanc i els marges per mantenir una llegibilitat professional.12

## **Figma com a catalitzador tècnic: Frames, Auto-layout i lògica de components**

Figma ha revolucionat el flux de treball de disseny proporcionant eines que reflecteixen la lògica estructural de l'enginyeria front-end. Comprendre les seves característiques tècniques —frames, auto-layout, components i variants— és essencial per construir sistemes de disseny de nivell professional.16

### **La base arquitectònica: Frames**

A Figma, els *frames* (marcs) són més que simples contenidors; són les estructures fundacionals per a les quadrícules i dissenys.16 Els frames s'utilitzen per establir dimensions estàndard, com una àrea de 24x24 píxels per a les icones per garantir un farciment consistent.16 També serveixen com a base per aplicar propietats com guies de disseny i el sistema de quadrícula de 8 punts.16

### **Responsivitat dinàmica: Auto-layout**

L'*auto-layout* és una propietat potent que permet als frames mantenir un espaiat i un disseny consistents a mesura que el contingut canvia.16 Funciona de manera similar al Flexbox de CSS, permetent als dissenyadors definir la direcció del contingut (horitzontal o vertical), l'espai entre capes i valors específics per al farciment.16 L'auto-layout garanteix que cada propietat sigui un múltiple de l'increment de quadrícula escollit.16

### **El motor de reutilització: Components i Variants**

El model de components a Figma és la implementació digital de la filosofia del Disseny Atòmic. Distingeix entre el "component principal", que defineix les propietats i l'estil, i les "instàncies", que són còpies reutilitzables enllaçades al component principal.16

* **Component principal:** Actua com la definició mestra. Qualsevol actualització del seu estil es transmet automàticament a totes les instàncies del projecte.17  
* **Instàncies:** Són les unitats funcionals utilitzades en els dissenys. Tot i que hereten propietats del component principal, permeten "sobreescriptures" (*overrides*), on propietats específiques (com etiquetes de text o tipus d'icona) es poden personalitzar per a un context particular sense trencar l'enllaç amb l'estil mestre.17  
* **Variants:** Les variants permeten als dissenyadors agrupar components similars que representen diferents estats del mateix element, com ara "Actiu" versus "Desactivat" per a un interruptor.16 S'organitzen en "conjunts de components", on les propietats es gestionen mitjançant valors booleans o cadenes de text en el panell de propietats de Figma.16

## **La lògica de la interacció: Prototipatge avançat a Figma**

El prototipatge a Figma ha evolucionat de simples transicions de pantalla a simulacions complexes basades en la lògica.8 Això permet als dissenyadors crear proves d'usuari d'alta fidelitat que es comporten de manera gairebé idèntica al programari acabat.8

### **Creació de fluxos interactius**

Els prototips de Figma s'organitzen en **fluxos**, que representen la xarxa de frames i connexions en una pàgina.8 Els dissenyadors creen "connexions" arrossegant fletxes blaves des d'un punt interactiu (*hotspot*) fins a un frame de destí.8

| Funció | Descripció | Detall de la interacció |
| :---- | :---- | :---- |
| **Disparadors** (*Triggers*) | L'acció de l'usuari que inicia la interacció. | Tocar, Clicar, Arrossegar, Sobrevolar |
| **Accions** | El resultat del disparador. | Navegar a, Obrir superposició, Enrere |
| **Animacions** | Com ocorre visualment la transició. | Dissoldre, Moure's cap a, Smart Animate |
| **Superposicions** (*Overlays*) | Contingut mostrat per sobre de la pantalla actual. | Centrat, Inferior, o Posició manual |

8

### **Lògica avançada amb variables**

Les variables permeten emmagatzemar i manipular dades dins d'un prototip, reduint significativament el nombre de frames necessaris per a fluxos complexos.8 Figma admet quatre tipus de variables: **Cadena** (text), **Número** (dimensions/quantitats), **Booleà** (visibilitat/estats) i **Color**.8  
L'acció "Set Variable" permet als dissenyadors canviar aquests valors basant-se en els disparadors de l'usuari. A més, l'ús de **lògica condicional** (declaracions if/else) permet que el prototip prengui decisions.8

## **El pont semàntic: Design Tokens**

Els *design tokens* (tokens de disseny) representen l'abstracció màxima de les decisions de disseny. Són entitats amb nom que emmagatzemen valors d'estil visual —com un codi hexadecimal específic o un valor de píxel per a l'espaiat— actuant com una única font de veritat entre el disseny i el codi.18

### **La jerarquia d'abstracció**

Per gestionar eficaçment un sistema de disseny escalable, els tokens s'acostumen a categoritzar en tres nivells d'especificitat 18:

1. **Tokens primitius (Fonament):** Són els valors bruts i immutables. Per exemple, color-blue-400 apunta a \#40a9ff. Aquests no s'utilitzen directament en els components de la UI, sinó que serveixen com a capa base per a altres tokens.18  
2. **Tokens semàntics:** Aquests tokens descriuen la *intenció* o el *paper* d'un estil. En lloc de fer referència a un color, un dissenyador fa referència al seu propòsit: status-success-background. Aquest token podria apuntar de nou a color-green-100.18 Són crítics per a la tematització, com el mode fosc.18  
3. **Tokens contextuals (de component):** Són els més específics, aplicant tokens semàntics a un component o estat particular, com button-primary-hover-background.18

Els design tokens solucionen les "conjectures" en construir productes proporcionant un llenguatge compartit.19 Atès que els tokens es poden exportar a codi específic de la plataforma (com variables CSS o JSON), qualsevol canvi realitzat centralment actualitzarà automàticament tot l'ecosistema.18

## **Aïllament de l'enginyeria: Storybook per a la documentació**

**Storybook** és una eina essencial per al flux de treball de desenvolupament modern, proporcionant un entorn aïllat —un "taller"— on els components de la UI es construeixen, es visualitzen i es documenten independentment de la lògica de negoci de l'aplicació principal.21

### **Documentar mitjançant "Stories"**

A Storybook, els desenvolupadors capturen estats específics dels components com a "stories" (històries). Aquestes històries serveixen com a documentació viva, mostrant com es veu i es comporta un component sota diverses condicions, com ara diferents propietats (*props*), dades simulades o casos límit de longitud de text.21 Storybook ajuda els equips a trobar i reutilitzar patrons de UI existents, actuant com un índex centralitzat per a la part de l'enginyeria d'un sistema de disseny.21 Pot generar automàticament documentació a partir de les històries escrites, assegurant que el manual mai quedi desincronitzat amb el codi de producció.21

## **Estàndards empresarials: Material UI, Atlassian i Finastra**

Les organitzacions líders han desenvolupat els seus propis sistemes de disseny per mantenir la consistència en les seves suites de productes globals.2

### **Material UI (MUI)**

Material UI és una robusta biblioteca de components basada en React que implementa la filosofia Material Design de Google.2 És fonamentalment "*mobile-first*", on els components estan dissenyats per a la interacció tàctil i finestres de visualització petites abans de ser escalats.23 Utilitza CssBaseline per normalitzar les inconsistències dels navegadors i utilitza el sistema tipogràfic Roboto per defecte.23

### **Atlassian Design System (ADS)**

El sistema de disseny d'Atlassian està construït per potenciar els equips mitjançant un llenguatge de disseny unificat que se sent cohesionat en productes com Jira i Confluence.24

* **Fonaments i Primitives:** ADS es basa en gran mesura en design tokens per als seus fonaments i utilitza "primitives" —components de baix nivell per al disseny (*Box*, *Inline*, *Stack*)— per compondre dissenys complexos.25  
* **Patrons d'IA:** Un aspecte únic d'ADS són els seus patrons especialitzats per a la intel·ligència artificial, anomenats "Rovo", que inclouen etiquetes distintives, vores de colors per al contingut generat per IA i botons especialitzats com "Ask Rovo".24  
* **Accessibilitat:** L'accessibilitat és un requisit bàsic, amb principis específics i "anotacions d'accessibilitat" integrades a les biblioteques de Figma.24

### **Finastra Design System (Fusion)**

Finastra proporciona un sistema de disseny especialitzat per a la indústria dels serveis financers, integrat dins del seu ecosistema FusionFabric.cloud.26

* **Enfocament industrial:** El sistema està optimitzat per a quadres de comandament financers i aplicacions amb gran quantitat de dades, oferint elements de UI especialitzats com gràfics complexos i taules dinàmiques.28  
* **Ecosistema de desenvolupadors:** Consta de tres components clau: **FusionCreator** (portal de desenvolupadors i catàleg d'API), **FusionOperate** (entorn de producció segur) i **FusionStore** (mercat per a aplicacions bancàries).30  
* **Personalització:** El sistema està dissenyat per ser altament flexible, permetent que les fintechs i els bancs personalitzin els components per ajustar-los al seu branding.28

| Sistema | Stack tecnològic principal | Tematització | Punt fort principal |
| :---- | :---- | :---- | :---- |
| **Material UI** | React, TypeScript | Mode fosc | Eficiència mobile-first i normalització de navegadors |
| **Atlassian ADS** | React 18, TypeScript | Tokens, Mode fosc | Patrons d'interacció d'IA (Rovo) i treball en equip |
| **Finastra Fusion** | Angular, Web Components | Mode fosc | Visualització de dades financeres i economia d'APIs obertes |

2

#### **Obras citadas**

1. UI Design: Differences between Wireframes, Mockups & Prototyping \- Ventum Consulting, fecha de acceso: abril 30, 2026, [https://www.ventum-consulting.com/en/news/ui-design/](https://www.ventum-consulting.com/en/news/ui-design/)  
2. Design Systems For Figma, fecha de acceso: abril 30, 2026, [https://www.designsystemsforfigma.com/](https://www.designsystemsforfigma.com/)  
3. Wireframe vs. Mockup: Essential Tools for Designers & Stakeholders \- Miro, fecha de acceso: abril 30, 2026, [https://miro.com/wireframe/wireframe-vs-mockup/](https://miro.com/wireframe/wireframe-vs-mockup/)  
4. Wireframe vs Mockup vs Prototype: What Each One Is (and When to Use It) \- Magic Patterns, fecha de acceso: abril 30, 2026, [https://www.magicpatterns.com/blog/wireframe-vs-mockup-vs-prototype](https://www.magicpatterns.com/blog/wireframe-vs-mockup-vs-prototype)  
5. Wireframes, Mockups, and Prototypes: Differences and Characteristics | Conflux, fecha de acceso: abril 30, 2026, [https://www.weareconflux.com/en/blog/wireframes-mockups-and-prototypes-differences-and-characteristics](https://www.weareconflux.com/en/blog/wireframes-mockups-and-prototypes-differences-and-characteristics)  
6. What is Wireframing in Mobile App Development? | Codecademy, fecha de acceso: abril 30, 2026, [https://www.codecademy.com/article/mobile-app-wireframing](https://www.codecademy.com/article/mobile-app-wireframing)  
7. Understanding The Difference Between Wireframes, Mockups, and Prototypes \- Tech.us, fecha de acceso: abril 30, 2026, [https://tech.us/blog/understanding-the-difference-between-wireframes-mockups-and-prototypes](https://tech.us/blog/understanding-the-difference-between-wireframes-mockups-and-prototypes)  
8. Guide to prototyping in Figma – Figma Learn \- Help Center, fecha de acceso: abril 30, 2026, [https://help.figma.com/hc/en-us/articles/360040314193-Guide-to-prototyping-in-Figma](https://help.figma.com/hc/en-us/articles/360040314193-Guide-to-prototyping-in-Figma)  
9. Atomic Design Methodology Explained: A Complete Guide \- Figr, fecha de acceso: abril 30, 2026, [https://figr.design/blog/atomic-design-methodology-explained](https://figr.design/blog/atomic-design-methodology-explained)  
10. Atomic Design Methodology, fecha de acceso: abril 30, 2026, [https://atomicdesign.bradfrost.com/chapter-2/](https://atomicdesign.bradfrost.com/chapter-2/)  
11. Atomic Design and Modern Design Systems | by Dan Balaban, fecha de acceso: abril 30, 2026, [https://www.designsystemscollective.com/atomic-design-and-modern-design-systems-104d981fe183](https://www.designsystemscollective.com/atomic-design-and-modern-design-systems-104d981fe183)  
12. Graphic Charter: Usefulness and Definition, fecha de acceso: abril 30, 2026, [https://www.sevengoldagency.com/us/blog/graphic-charter-usefulness-and-definition](https://www.sevengoldagency.com/us/blog/graphic-charter-usefulness-and-definition)  
13. Creating a graphic charter for a luxury brand \- Sup de Luxe, fecha de acceso: abril 30, 2026, [https://www.supdeluxe.com/en/luxury-news/creating-graphic-charter-luxury-brand](https://www.supdeluxe.com/en/luxury-news/creating-graphic-charter-luxury-brand)  
14. Mastering the art of brand guidelines (with examples) \- Nulab, fecha de acceso: abril 30, 2026, [https://nulab.com/learn/design-and-ux/brand-guidelines/](https://nulab.com/learn/design-and-ux/brand-guidelines/)  
15. The Complete Guide to Brand Identity Design \- Adobe Certified Professional, fecha de acceso: abril 30, 2026, [https://certifiedprofessional.adobe.com/blog/the-complete-guide-to-brand-identity-design](https://certifiedprofessional.adobe.com/blog/the-complete-guide-to-brand-identity-design)  
16. Lesson 3: Build your design system – Figma Learn \- Help Center, fecha de acceso: abril 30, 2026, [https://help.figma.com/hc/en-us/articles/14548865734679-Lesson-3-Build-your-design-system](https://help.figma.com/hc/en-us/articles/14548865734679-Lesson-3-Build-your-design-system)  
17. Guide to components in Figma – Figma Learn \- Help Center, fecha de acceso: abril 30, 2026, [https://help.figma.com/hc/en-us/articles/360038662654-Guide-to-components-in-Figma](https://help.figma.com/hc/en-us/articles/360038662654-Guide-to-components-in-Figma)  
18. Design Tokens in Design Systems: A Practical Guide | by Think Design \- Medium, fecha de acceso: abril 30, 2026, [https://medium.com/@marketingtd64/design-tokens-in-design-systems-a-practical-guide-9af174cd1350](https://medium.com/@marketingtd64/design-tokens-in-design-systems-a-practical-guide-9af174cd1350)  
19. Update 1: Tokens, variables, and styles – Figma Learn \- Help Center, fecha de acceso: abril 30, 2026, [https://help.figma.com/hc/en-us/articles/18490793776023-Update-1-Tokens-variables-and-styles](https://help.figma.com/hc/en-us/articles/18490793776023-Update-1-Tokens-variables-and-styles)  
20. Design tokens \- USWDS \- Digital.gov, fecha de acceso: abril 30, 2026, [https://designsystem.digital.gov/design-tokens/](https://designsystem.digital.gov/design-tokens/)  
21. Why Storybook? | Storybook docs, fecha de acceso: abril 30, 2026, [https://storybook.js.org/docs/get-started/why-storybook](https://storybook.js.org/docs/get-started/why-storybook)  
22. Overview \- About atlassian design system, fecha de acceso: abril 30, 2026, [https://atlassian.design/get-started/about-atlassian-design-system](https://atlassian.design/get-started/about-atlassian-design-system)  
23. Usage \- Material UI \- MUI, fecha de acceso: abril 30, 2026, [https://mui.com/material-ui/getting-started/usage/](https://mui.com/material-ui/getting-started/usage/)  
24. Design System \- Atlassian Design, fecha de acceso: abril 30, 2026, [https://atlassian.design/design-system](https://atlassian.design/design-system)  
25. Primitives \- index \- Components \- Atlassian Design System, fecha de acceso: abril 30, 2026, [https://atlassian.design/components/primitives/overview](https://atlassian.design/components/primitives/overview)  
26. fusionfabric.cloud \- a new platform for innovation and collaboration \- Finastra, fecha de acceso: abril 30, 2026, [https://www.finastra.com/sites/default/files/2019-08/brochure-fusionfabriccloud.pdf](https://www.finastra.com/sites/default/files/2019-08/brochure-fusionfabriccloud.pdf)  
27. fusionfabric.cloud \- a new platform for innovation and collaboration \- Finastra, fecha de acceso: abril 30, 2026, [https://www.finastra.com/sites/default/files/2019-06/brochure-fusionfabric-cloud.pdf](https://www.finastra.com/sites/default/files/2019-06/brochure-fusionfabric-cloud.pdf)  
28. Top 10 Figma Design Systems To Build Custom Design \- DhiWise, fecha de acceso: abril 30, 2026, [https://www.dhiwise.com/post/top-10-figma-design-systems-and-ui-toolkits-to-custom-design](https://www.dhiwise.com/post/top-10-figma-design-systems-and-ui-toolkits-to-custom-design)  
29. 12 Best Free Open Source Figma UI Kits and Design Systems For Your Next Project, fecha de acceso: abril 30, 2026, [https://medevel.com/12-figma-ui-ux-kit/](https://medevel.com/12-figma-ui-ux-kit/)  
30. fusionfabric.cloud \- open collaboration means faster innovation \- Finastra, fecha de acceso: abril 30, 2026, [https://www.finastra.com/sites/default/files/documents/2018/04/brochure-fusionfabric-cloud.pdf](https://www.finastra.com/sites/default/files/documents/2018/04/brochure-fusionfabric-cloud.pdf)