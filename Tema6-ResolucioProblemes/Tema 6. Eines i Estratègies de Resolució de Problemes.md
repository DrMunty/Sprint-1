# **Estratègies Arquitectòniques en la Depuració Moderna i Resolució de Problemes Algorísmics**

L'evolució de l'enginyeria de programari moderna es caracteritza per una complexitat creixent que sovint supera les limitacions cognitives de la ment humana. Per navegar en aquesta complexitat, la indústria ha adoptat un marc de pensament computacional que serveix de base per identificar, aïllar i rectificar defectes. Aquest informe explora la intersecció entre les estratègies teòriques de resolució de problemes i les capacitats de diagnòstic dels entorns de desenvolupament contemporanis.

## **1\. Fonaments del Pensament Computacional en la Resolució d'Errors**

La depuració és un exercici de pensament computacional que organitza les dades de manera lògica i modela sistemes complexos mitjançant l'abstracció.1 La dificultat de la programació prové del fet que els humans només podem mantenir una visió simultània d'uns pocs elements alhora.2

### **El mecanisme de la descomposició i l'abstracció**

* **Descomposició:** És el procés d'agafar un problema complex i dividir-lo en subproblemes més petits i manejables.2 En depuració, això permet verificar la integritat de mòduls individuals (com un gestor d'API o un component d'interfície) sense la interferència del soroll de la resta del sistema.2  
* **Abstracció:** Implica eliminar detalls superficials per centrar-se en la lògica essencial que governa el comportament del sistema.1 En crear un model generalitzat, els desenvolupadors poden identificar patrons de fallada (com una condició de carrera o "race condition") que es repeteixen en diferents mòduls.1

## **2\. Transformació de Problemes Reals a Passos Algorísmics**

Un algorisme és una seqüència finita, ordenada i precisa de passos per realitzar una tasca.3 La traducció de requeriments reals a estructures algorísmiques és un pas previ imprescindible abans de codificar.2

### **Exemples de modelatge de procediments**

* **Processos quotidians:** Fregir un ou es pot modelar amb passos finits: comprar ingredients (entrada), encendre la cuina, esperar que l'oli s'escalfi (condició), trencar l'ou i esperar que es fregi (procés), girar-lo i servir (sortida).3  
* **Algorismes matemàtics i de negoci:**  
  * **Promig de notes:** Rebre ![][image1] números, sumar-los, dividir la suma per ![][image1] i mostrar el resultat.5  
  * **Càlcul d'interessos:** El guany (![][image2]) es calcula mitjançant el capital (![][image3]) multiplicat per la taxa (![][image4]), on ![][image5].4  
  * **Càlcul de canvi:** Sumar els preus dels objectes comprats i restar-ho del pagament rebut. L'algorisme ha de preveure la condició de si el pagament és suficient per cobrir el total.6  
* **Cerca de dades:**  
  * **Cerca lineal:** Revisa cada element fins a trobar l'objectiu; senzill però ineficient en conjunts grans.7  
  * **Cerca binària:** En un conjunt ordenat, divideix l'interval de cerca a la meitat repetidament, reduint dràsticament el temps necessari.7

## **3\. Funcionalitats Clau del Panell "Sources"**

Quan la lògica falla, els desenvolupadors utilitzen el panell **Sources** (Chrome) o **Debugger** (Firefox) per realitzar un examen clínic del codi.8

### **Breakpoints i suspensió de l'execució**

* **Punts de ruptura de línia:** Aturen el motor just abans d'executar una línia específica.8  
* **Breakpoints condicionals:** S'activen només si una expressió és certa (ex: i \=== 99), estalviant temps en bucles llargs.8  
* **Event Listener Breakpoints:** Pausen l'execució quan ocorre un esdeveniment específic (com un click), ideal quan sabem què causa l'error però no on està el codi.8  
* **DOM Mutation Breakpoints:** Aturen el programa quan un element de la pàgina canvia, s'elimina o es modifiquen els seus atributs.9

### **Call Stack i Watch Expressions**

* **Call Stack (Pila de crides):** Mostra el camí d'execució que ha portat al punt actual, permetent veure quina funció ha disparat la funció present.8  
* **Watch Expressions (Expressions de vigilància):** Permeten monitorar valors de variables o expressions personalitzades (com typeof sum) en temps real cada vegada que el codi s'atura.8

## **4\. Inspecció d'Estats i Flux d'Execució en Temps Real**

La depuració interactiva permet interrogar el sistema en estat de suspensió.8

* **Inline Previews:** Chrome mostra els valors actuals de les variables directament a l'editor de codi, al costat de la seva declaració.8  
* **Pestanya Scope:** Ofereix una llista jeràrquica de totes les variables locals i globals. Els valors es poden editar manualment per forçar canvis en la lògica durant la prova.8  
* **Integració amb la Consola:** Prement la tecla Esc, s'obre la consola dins del panell Sources, permetent executar codi en l'àmbit actual per testar correccions ràpides.8  
* **Control del flux:** Les comandes **Step Over** (saltar funció), **Step Into** (entrar a la funció), **Step Out** (sortir de la funció) i **Resume** (continuar) permeten navegar per l'execució pas a pas.9

## **5\. Mapatge d'Errors Comuns de JavaScript**

Els errors es divideixen principalment en dues fases: parseig (temps de compilació/lectura) i execució (runtime).10

| Tipus d'Error | Causa Subjacent | Fase |
| :---- | :---- | :---- |
| **SyntaxError** | Errors gramaticals: falta de claus }, parèntesis o cometes.10 | Parse-time (Compilació) |
| **ReferenceError** | Intent d'accedir a una variable no declarada o fora de l'àmbit actual.13 | Runtime (Execució) |
| **TypeError** | Operació incompatible: cridar una variable com si fos una funció o accedir a propietats de null.13 | Runtime (Execució) |
| **Logic Error** | El codi és sintàcticament correcte però la lògica és errònia (ex: ús de \= en lloc de \===).10 | Runtime (Execució) |

## **6\. L'error "Cannot read property X of null"**

Aquesta és l'excepció més freqüent en el desenvolupament web.13

* **Causes:** S'intenta accedir a un element del DOM que encara no existeix o el component renderitza abans que les dades asíncrones de l'API hagin arribat (l'estat inicial és null o undefined).13  
* **Estratègies d'identificació:** Revisar la pila de crides per trobar on s'assigna la variable. Comprovar si el selector de document.querySelector és correcte (ex: falta el punt per a una classe).10  
* **Prevenzió:** Utilitzar inicialitzacions per defecte (com ara \`\`), clàusules de guarda (if (obj)) o l'encadenament opcional (?.).13

## **7\. console.log vs. Breakpoints: Pros i Contres**

| Mètode | Avantatges | Desavantatges |
| :---- | :---- | :---- |
| **console.log** | Senzill, ràpid per a traces ràpides, bo per a esdeveniments d'alta freqüència (moviment de ratolí).14 | Embruta el codi, visió estàtica, pot fallar en navegadors antics si es deixa en producció.14 |
| **Breakpoints** | Interactiu, visió completa de la memòria, permet editar estats en viu, sense modificar el codi font.14 | Major corba d'aprenentatge, pot ocultar errors de sincronització (efecte Schrödinger).14 |

## **8\. Tècniques per a Errors Intermitents**

Els errors esporàdics solen deure's a condicions de carrera o variabilitat de la xarxa.18

* **Investigació científica:** Recollir dades de l'entorn (SO, navegador, hora exacta) i formular hipòtesis.18  
* **Entorns controlats:** Utilitzar eines com **JMeter** per simular càrrega o **Chaos Monkey** per introduir fallades forçades.18  
* **Registres (Logs):** Si un error no es pot reproduir, cal afegir logs detallats ("Smart Logging") que capturin l'estat del sistema quan la fallada torni a ocórrer en el futur.18

## **9\. Gestió de Dependències i Automatització amb NPM i Git**

* **NPM Essentials:** npm init per iniciar projectes, npm install per descarregar dependències (basant-se en el package.json), i npm audit per seguretat.22  
* **Git:** Ús de git submodule add per incloure repositoris externs i git submodule update \--init \--recursive per assegurar que el projecte estigui complet després del clonatge.23  
* **Scripts d'NPM:** Permeten automatitzar tasques repetitives.27 Per exemple, el script "debug": "node \--inspect server.js" permet arrencar el depurador fàcilment amb npm run debug.28

## **10\. Optimització de Codi i Recursos**

* **Flame Graph (Performance):** Aquesta gràfica mostra el temps (eix X) i la pila de crides (eix Y). Una barra ampla indica una funció lenta. Els triangles vermells marquen les "Long Tasks" (\>50ms) que causen pèrdua de fluïdesa a la interfície.30  
* **Panell Network:** Permet inspeccionar si els recursos (JS, CSS, imatges) es carreguen correctament, analitzar les capçaleres de memòria cau i simular connexions lentes per veure el rendiment sota estrès.31  
* **Lighthouse:** Proporciona auditories automàtiques de velocitat, accessibilitat i SEO amb recomanacions per optimitzar la càrrega.31

#### **Obras citadas**

1. Pensament computacional \- Viquipèdia, l'enciclopèdia lliure, fecha de acceso: mayo 3, 2026, [https://ca.wikipedia.org/wiki/Pensament\_computacional](https://ca.wikipedia.org/wiki/Pensament_computacional)  
2. Descomposició de problemes \- IOC, fecha de acceso: mayo 3, 2026, [https://ioc.xtec.cat/materials/FP/Recursos/fp\_asix\_m03\_/web/fp\_asix\_m03\_htmlindex/WebContent/u4/a1/continguts.html](https://ioc.xtec.cat/materials/FP/Recursos/fp_asix_m03_/web/fp_asix_m03_htmlindex/WebContent/u4/a1/continguts.html)  
3. Algorismes \- IOC, fecha de acceso: mayo 3, 2026, [https://ioc.xtec.cat/materials/FP/Recursos/fp\_asix\_m03\_/web/fp\_asix\_m03\_htmlindex/WebContent/u2/a1/continguts.html](https://ioc.xtec.cat/materials/FP/Recursos/fp_asix_m03_/web/fp_asix_m03_htmlindex/WebContent/u2/a1/continguts.html)  
4. Algoritmos y resolución de problemas \- YouTube, fecha de acceso: mayo 3, 2026, [https://www.youtube.com/watch?v=\_dRBM6FzsDc](https://www.youtube.com/watch?v=_dRBM6FzsDc)  
5. Aprende a resolver problemas con algoritmos paso a paso \- UCLM, fecha de acceso: mayo 3, 2026, [https://www.uclm.es/global/promotores/organos%20de%20gobierno/vicerrectorado%20de%20transformacion%20y%20estrategia%20digital/consejos-tic/cerosyunos125](https://www.uclm.es/global/promotores/organos%20de%20gobierno/vicerrectorado%20de%20transformacion%20y%20estrategia%20digital/consejos-tic/cerosyunos125)  
6. Desarrolla algoritmos para solucionar problemas | Universidad de Monterrey \- YouTube, fecha de acceso: mayo 3, 2026, [https://www.youtube.com/watch?v=B4v1SVElUBw](https://www.youtube.com/watch?v=B4v1SVElUBw)  
7. Algorithms in JavaScript with visual examples. \- DEV Community, fecha de acceso: mayo 3, 2026, [https://dev.to/swastikyadav/algorithms-in-javascript-with-visual-examples-gh3](https://dev.to/swastikyadav/algorithms-in-javascript-with-visual-examples-gh3)  
8. Cómo depurar JavaScript | Chrome DevTools | Chrome for Developers, fecha de acceso: mayo 3, 2026, [https://developer.chrome.com/docs/devtools/javascript?hl=es-419](https://developer.chrome.com/docs/devtools/javascript?hl=es-419)  
9. The Firefox JavaScript Debugger \- Firefox Source Docs documentation, fecha de acceso: mayo 3, 2026, [https://firefox-source-docs.mozilla.org/devtools-user/debugger/](https://firefox-source-docs.mozilla.org/devtools-user/debugger/)  
10. What went wrong? Troubleshooting JavaScript \- Learn web ..., fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Learn\_web\_development/Core/Scripting/What\_went\_wrong\#types\_of\_error](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/What_went_wrong#types_of_error)  
11. What is a Runtime Error? \- Airbrake Docs, fecha de acceso: mayo 3, 2026, [https://docs.airbrake.io/blog/software-development/runtime-error/](https://docs.airbrake.io/blog/software-development/runtime-error/)  
12. Difference between Compile Time Errors and Runtime Errors \- GeeksforGeeks, fecha de acceso: mayo 3, 2026, [https://www.geeksforgeeks.org/c/difference-between-compile-time-errors-and-runtime-errors/](https://www.geeksforgeeks.org/c/difference-between-compile-time-errors-and-runtime-errors/)  
13. Top 10 JavaScript errors from 1000+ projects (and how to avoid ..., fecha de acceso: mayo 3, 2026, [https://rollbar.com/blog/top-10-javascript-errors-from-1000-projects-and-how-to-avoid-them/](https://rollbar.com/blog/top-10-javascript-errors-from-1000-projects-and-how-to-avoid-them/)  
14. Breakpoint Debugger vs Console.log Statement: A Frontend Developer's Perspective, fecha de acceso: mayo 3, 2026, [https://dev.to/rio14/breakpoint-debugger-vs-consolelog-statement-a-frontend-developers-perspective-5cg5](https://dev.to/rio14/breakpoint-debugger-vs-consolelog-statement-a-frontend-developers-perspective-5cg5)  
15. Run/Debug configuration: XSLT | WebStorm Documentation \- JetBrains, fecha de acceso: mayo 3, 2026, [https://www.jetbrains.com/help/webstorm/run-debug-configuration-xslt.html](https://www.jetbrains.com/help/webstorm/run-debug-configuration-xslt.html)  
16. My co-worker told me to NEVER use the Chrome JavaScript debugger; instead, I should only use console.log(). Does anyone else feel this way? \- Quora, fecha de acceso: mayo 3, 2026, [https://www.quora.com/My-co-worker-told-me-to-NEVER-use-the-Chrome-JavaScript-debugger-instead-I-should-only-use-console-log-Does-anyone-else-feel-this-way](https://www.quora.com/My-co-worker-told-me-to-NEVER-use-the-Chrome-JavaScript-debugger-instead-I-should-only-use-console-log-Does-anyone-else-feel-this-way)  
17. Do you reach for console.log or breakpoints first? Why? : r/reactjs \- Reddit, fecha de acceso: mayo 3, 2026, [https://www.reddit.com/r/reactjs/comments/1o8bpk0/do\_you\_reach\_for\_consolelog\_or\_breakpoints\_first/](https://www.reddit.com/r/reactjs/comments/1o8bpk0/do_you_reach_for_consolelog_or_breakpoints_first/)  
18. Identifying and Reproducing Intermittent Bugs | by Olha Holota from TestCaseLab \- Medium, fecha de acceso: mayo 3, 2026, [https://medium.com/@case\_lab/identifying-and-reproducing-intermittent-bugs-efce4ffb5af3](https://medium.com/@case_lab/identifying-and-reproducing-intermittent-bugs-efce4ffb5af3)  
19. Intermittent Bug Debugging: How to Reproduce and Deal With Bugs | bugpilot.io, fecha de acceso: mayo 3, 2026, [https://bugpilot.io/2025/10/18/intermittent-bug-debugging-how-to-reproduce-and-deal-with-bugs/](https://bugpilot.io/2025/10/18/intermittent-bug-debugging-how-to-reproduce-and-deal-with-bugs/)  
20. The Art of Debugging: Bug Reproduction (Part 2\) | by Sopheak Hang | Medium, fecha de acceso: mayo 3, 2026, [https://medium.com/@hangsopheak.hod/the-art-of-debugging-bug-reproduction-part-2-2356b279dc08](https://medium.com/@hangsopheak.hod/the-art-of-debugging-bug-reproduction-part-2-2356b279dc08)  
21. How do you reproduce bugs that occur sporadically? \- Stack Overflow, fecha de acceso: mayo 3, 2026, [https://stackoverflow.com/questions/2515903/how-do-you-reproduce-bugs-that-occur-sporadically](https://stackoverflow.com/questions/2515903/how-do-you-reproduce-bugs-that-occur-sporadically)  
22. Package management basics \- Learn web development | MDN, fecha de acceso: mayo 3, 2026, [https://developer.mozilla.org/en-US/docs/Learn\_web\_development/Extensions/Client-side\_tools/Package\_management](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Client-side_tools/Package_management)  
23. How To Manage Dependencies in Git? \- GeeksforGeeks, fecha de acceso: mayo 3, 2026, [https://www.geeksforgeeks.org/git/how-to-manage-dependencies-in-git/](https://www.geeksforgeeks.org/git/how-to-manage-dependencies-in-git/)  
24. Essential npm Commands Every Developer Should Know \- OpenReplay Blog, fecha de acceso: mayo 3, 2026, [https://blog.openreplay.com/essential-npm-commands/](https://blog.openreplay.com/essential-npm-commands/)  
25. Git Submodules: It's a hidden gem | by Rohan Chandra Sen | Medium, fecha de acceso: mayo 3, 2026, [https://medium.com/@rohansen856/git-submodules-its-a-hidden-gem-2ff950062d17](https://medium.com/@rohansen856/git-submodules-its-a-hidden-gem-2ff950062d17)  
26. Managing Repositories with Git Submodules \- Aviator, fecha de acceso: mayo 3, 2026, [https://www.aviator.co/blog/managing-repositories-with-git-submodules/](https://www.aviator.co/blog/managing-repositories-with-git-submodules/)  
27. scripts | npm Docs, fecha de acceso: mayo 3, 2026, [https://docs.npmjs.com/cli/v8/using-npm/scripts](https://docs.npmjs.com/cli/v8/using-npm/scripts)  
28. How to debug using npm run scripts from VSCode? \- Stack Overflow, fecha de acceso: mayo 3, 2026, [https://stackoverflow.com/questions/34835082/how-to-debug-using-npm-run-scripts-from-vscode](https://stackoverflow.com/questions/34835082/how-to-debug-using-npm-run-scripts-from-vscode)  
29. Can I add a debug script to NPM? \- node.js \- Stack Overflow, fecha de acceso: mayo 3, 2026, [https://stackoverflow.com/questions/9633280/can-i-add-a-debug-script-to-npm](https://stackoverflow.com/questions/9633280/can-i-add-a-debug-script-to-npm)  
30. Referencia de las funciones de rendimiento | Chrome DevTools ..., fecha de acceso: mayo 3, 2026, [https://developer.chrome.com/docs/devtools/performance/reference?hl=es-419](https://developer.chrome.com/docs/devtools/performance/reference?hl=es-419)  
31. Cómo inspeccionar la actividad de red | Chrome DevTools | Chrome ..., fecha de acceso: mayo 3, 2026, [https://developer.chrome.com/docs/devtools/network?hl=es-419](https://developer.chrome.com/docs/devtools/network?hl=es-419)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAwAAAAXCAYAAAA/ZK6/AAAAlUlEQVR4XmNgGAWDCegC8Twg5obyeYG4AYgnADETVAwO2IF4KxBHA/F/IG4G4gVQuXqoGArYC6VhGhqR5EA2YWgohdLXGDAls7GIwQFIoh2L2GU0MTCQYIBIgpwAA3xQMQUofypCCsJBtxpZrBqIlZDkGP4C8VdkASAoYIBo0AfiS2hyDBZAzIouyACJHwN0wVFACAAA3qgdBAlcrcAAAAAASUVORK5CYII=>

[image2]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAYCAYAAAAlBadpAAAAyklEQVR4XmNgGJZAGogLgHgmECshiVshsTHAYiD+D8S3gdgbiFWBeBoQPwdiS6gcVgCS+A3E3OgSQFDJAJG/hC4BAn8Y8JgKBSD5IHTBD1AJZnQJNIBhuC5U8CG6BBaAofkvVJAXXYIYANKIYSKxAJ9mfyB2BmJ7IHYAYhcGtHABaXyNLIAEsoG4ngFhQTkQMyErwGczDIDkb6ELgsA1BogkO7oEFOQyQOTD0SVgAGY7ipOAQA5JDi/Yy4BQ+A5KN0Ll1sAUjYIhBwDP2zLKnm6VTgAAAABJRU5ErkJggg==>

[image3]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABUAAAAYCAYAAAAVibZIAAABCUlEQVR4XmNgGAW0BvVA/AWI/0PxWVRpDPCQAaEWpK8YVRoVwBSCMC6gB8S1DBA1xmhyWMETBoSLcYHHQHyMAb8aOPAC4hQg3sKAW8M6KE3IN3BwAkqDwgebBh4gzoWyQfKrkeRwAphBoHACsWWQ5EDgB5R2Z4DIayHJ4QRPkdggTXFI/Hwg5oayQT7C5hMMALI9DYkP0rQQiY/sVZLDEwZAmkCxDALPkCUYIHKr0MSwAnSbYa6xBWIdJHFvqLg2khhO8BKN/4YBovk2mjgop6E7AAMwAvFdBki2QwbLGbBrJhiePUD8AYjfAvFnIP6DJOcDxKFI/K8MCLWfgPg3EFciyY+CUUALAABbjUmZS+msywAAAABJRU5ErkJggg==>

[image4]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAYCAYAAAAlBadpAAAAy0lEQVR4Xu2SMQ8BURCER6XSqiVahd8gWr3/4g8olCqVH6KlUGkQnUonR0hEEGaz7708e+/UivuSSS4zs5fbzQElI+pMvZ1u1JF6RF7Dl4vwRcsM6jdtECOFuTVJB5qtbeDpQwtdG5AJNJsaP7BB+pOFonUCqUKbelJ74+eQQbnwklpRd+dV41IKv68cJmbr/J/skC4NoX7dBjGpfYUr1K/YIEYKC2ui+KWBAbTQswHyw+F5TF2oDHrlE/XyoaMFHThA//fad1zy53wAhPQ9J2j9tisAAAAASUVORK5CYII=>

[image5]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGQAAAAYCAYAAAAMAljuAAAC9ElEQVR4Xu2Yy8sPURjHH7csXP4BslDvxm3DAiUKvbmUKCzIAklJbgtR8tpYSEpKSUQWCiHJRrJwSS4bSS4pcs/9mkI8399zTvP8npkzv5kfZvR2PvVtZr7fM9Mzc2bOnBmiSCQS6TYMYq1m7WENVf54tR6pgEOsX6z7rBmsDtZu1nPWOJfVxWbWZ5IaoBvNcYpHlLTFfuua40p4yfpJSR3vWZ/U9rmkaRo0+M7qZwNmA0l+0wY14E8m7+YYxdpE0ma0yapmKUkdncbv7fwvxm/wg/JPECCfY80aeELJkxLiMesy5bepCow2oToybyw8RjB72cCQ2rEGppPccacpXM9xt8w82RxWWsMwxhoFyasjlY10BsbbVoQOWiVX3BLvg6x6+lNyYZEfVVkr1rAOW9Mxm3XemgVBHResyawlybq06V84A7T5H+M7Ae8FrA9WGfjmlhivkQ9TWRHwrjxhPAzTWRe0CPNI6phs/B3OR0c3kXpk/hDM0kI6yDrA2s/ax9rL6tvYqzhP1TrqXqS2V1EyIcGT1O55bWSddOvojEsqK8ttkjqusq6x7rjtYAfndcgskp6dyJrEmkKt3zP/Etz1y9Q26kYne/TwlHdeRUCnYFLgh8h2yaqjj/N2Gb8BglfWdKwgmfv7g65n9WxqUS324qAmzKbAMx2QZEeMV4YlrLusMzYoCeq4aE3K7qgGwUCB/J41A2wrqYGyWyFsnb72CawRyscHLfzhyisDOsMPKctZp1RWhoUkdUw1vv/+wDdfCj/GhcZyzFiQz7dBDeCrV/OapDbM8zX4gredV5TFlB7f0Sn+nVKGh5RdB4ZD+HgCM/F3mh2OhqisTnqwHlB6ao4palZt7da8gHXWmg68u45ZswWhOjC9hn9LbY9NYgH/VPwB3rrlFpeVLeRvsp3kw/UNyT8g/FHwzGTNVdv4BeHbfiQZEjCNLcpWaximWSMA6vhAUsc71lfWzqYWRC9IrjFuqusmi0QikUgkEolEuiu/ASO42wiFr0IDAAAAAElFTkSuQmCC>