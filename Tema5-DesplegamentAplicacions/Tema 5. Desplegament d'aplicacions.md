# **Paradigmes moderns en el desplegament de programari: una anàlisi exhaustiva de riscos, infraestructura i automatització**

El desplegament de programari ha deixat de ser una activitat perifèrica per convertir-se en el nucli de l'estratègia operativa de qualsevol organització tecnològica. La transició des dels lliuraments manuals i esporàdics cap a fluxos de treball automatitzats i continus ha permès una agilitat sense precedents, però també ha introduït complexitats estructurals que requereixen una comprensió profunda de la infraestructura, la seguretat i els processos de construcció. Aquest informe analitza de manera integral els pilars del desplegament modern, des de la gestió de riscos i l'elecció de l'arquitectura d'allotjament fins a l'automatització mitjançant pipelines i la contenidorització, proporcionant una base teòrica i pràctica per a la presa de decisions en entorns de producció crítics.

## **Riscos i conseqüències del desplegament directe a producció**

L'absència d'un entorn de prova o "staging" abans del desplegament a producció és un dels majors riscos que una organització pot assumir. L'entorn de staging actua com una rèplica exacta de l'entorn de producció, servint com un camp de proves on es validen les noves funcionalitats, les actualitzacions de seguretat i les integracions de tercers sota condicions que imiten la realitat sense exposar els usuaris finals a fallades sistèmiques.1 El desplegament directe, sovint anomenat "deploying to production", sense aquests passos intermedis, és comparable a realitzar una actuació en directe sense cap assaig previ, on qualsevol error té un impacte immediat i sovint devastador en la continuïtat del negoci.

### **Impacte en la continuïtat operativa i la reputació**

El risc més immediat d'ignorar els entorns de prova és la inestabilitat del sistema. Cada minut d'inactivitat o "downtime" en producció pot representar pèrdues econòmiques massives, especialment per a empreses emergents i plataformes de comerç electrònic on la disponibilitat és el factor crític d'èxit.1 Més enllà de la pèrdua directa d'ingressos, la inestabilitat genera una erosió de la confiança dels usuaris. La percepció d'una plataforma com a "fràgil" o plena de "bugs" pot forçar els clients a buscar alternatives més fiables, el que es tradueix en una pèrdua de valor de marca a llarg termini.1 El desplegament directe impedeix la verificació de si el codi funciona com s'esperava, convertint els usuaris finals en subjectes de prova involuntaris.

### **Fragilitat de la infraestructura i vulnerabilitats de seguretat**

L'entorn de staging no només serveix per provar la lògica del codi, sinó per validar la configuració de la infraestructura. Sense aquesta etapa, no es pot confirmar si la connectivitat de xarxa, les polítiques d'accés o les regles del firewall estan correctament establertes.2 Això és especialment perillós quan s'actualitzen dispositius de seguretat com encaminadors o sistemes de detecció d'intrusions; un canvi no provat podria deixar la xarxa vulnerable a atacs externs o filtracions de dades.2 A més, el staging permet provar els procediments de recuperació en cas de desastre i els plans de "rollback" (retorn a una versió anterior). Si un desplegament a producció falla i no hi ha un pla de rollback prèviament validat, la resolució del problema pot ser extremadament lenta i complexa, agreujant la crisi operativa.2

### **El problema de la fidelitat de l'entorn i la deriva de dades**

Un dels arguments més complexos en la gestió d'entorns és la "fidelitat". Sovint es produeix l'anomenat "mismatch" de configuració, on el codi funciona en staging però falla en producció a causa de petites diferències en les versions de les llibreries, les configuracions del servidor o els volums de dades.3 Tot i que alguns experts suggereixen que l'objectiu hauria de ser el "testing in production" amb les proteccions adequades (com el request isolation o els feature flags), el staging continua sent la xarxa de seguretat fonamental per a la majoria de les organitzacions.4 L'ús de dades reals en entorns de prova és una pràctica de risc que pot violar normatives com el GDPR; per tant, el staging ha d'utilitzar dades sintètiques o anonimitzades que mantinguin la complexitat de la producció sense comprometre la privadesa.1

| Tipus de Risc | Descripció Tècnica | Conseqüència de Negoci |
| :---- | :---- | :---- |
| **Downtime Operatiu** | Fallada crítica del sistema per codi no verificat. | Pèrdua d'ingressos immediata i cessament de serveis.1 |
| **Erosió de Confiança** | Aparició de regressions i errors visuals o funcionals. | Pèrdua de clients i degradació de la imatge de marca.1 |
| **Bretxa de Seguretat** | Configuracions de xarxa o permisos incorrectes. | Filtració de dades sensibles i sancions legals.2 |
| **Fallada d'Integració** | Incompatibilitat amb serveis externs o APIs. | Interrupció de fluxos de treball crítics.2 |
| **Dificultat de Rollback** | Absència de proves en els mecanismes de recuperació. | Prolongació del temps mitjà de resolució (MTTR).2 |

## **Comparativa de models d'allotjament: Shared Hosting, VPS i Serverless**

L'elecció de l'entorn on s'executarà l'aplicació és una decisió d'arquitectura amb implicacions profundes en el cost, el rendiment i la càrrega operativa de l'equip de desenvolupament. Els models han evolucionat des de la compartició rígida de recursos fins a l'abstracció total de la infraestructura.

### **Allotjament Compartit (Shared Hosting): Simplicitat i Baix Cost**

El Shared Hosting representa el model d'entrada per a la presència web. En aquesta arquitectura, múltiples llocs web comparteixen els recursos d'un mateix servidor físic, incloent-hi la CPU, la memòria RAM i l'amplada de banda.5

* **Costos**: És l'opció més econòmica del mercat, amb preus que poden ser de pocs dòlars al mes, ja que el cost del servidor es divideix entre centenars d'usuaris.6  
* **Control**: El control és extremadament limitat. L'usuari no té accés a l'arrel (root) i ha de dependre del programari i les versions que el proveïdor hagi decidit instal·lar. No és possible realitzar configuracions a nivell de sistema operatiu ni instal·lar serveis personalitzats.5  
* **Escenaris idonis**: Projectes personals, blogs, llocs web de petites empreses amb poc trànsit o qualsevol aplicació on el cost sigui el factor determinant i la simplicitat de gestió sigui preferible a la potència.5  
* **Riscos**: El principal inconvenient és l'anomenat "veí sorollós"; si un altre lloc web al mateix servidor consumeix massa recursos o és atacat, el vostre lloc web es veurà afectat en rendiment i seguretat.6

### **Servidor Privat Virtual (VPS): Control i Recursos Dedicats**

Un VPS és una instància virtualitzada dins d'un servidor físic que ofereix recursos dedicats i aïllament mitjançant un hipervisor. És l'evolució natural quan es necessita més potència i flexibilitat que la que ofereix l'allotjament compartit.5

* **Costos**: Moderats i predictibles. Es paga una quota mensual fixa per una quantitat específica de vCPU, RAM i emmagatzematge, independentment de si s'utilitzen o no.8  
* **Control**: Total. L'usuari té accés root, el que permet instal·lar qualsevol sistema operatiu, configurar el servidor web a mida, gestionar el firewall i optimitzar el stack tecnològic segons les necessitats de l'aplicació.5  
* **Escenaris idonis**: Aplicacions empresarials en creixement, plataformes de comerç electrònic amb trànsit estable, bases de dades persistents i aplicacions que requereixen processos de llarga durada o WebSockets.5  
* **Càrrega Operativa**: L'usuari és responsable del manteniment, les actualitzacions de seguretat, les còpies de seguretat i l'escalat manual de recursos, el que requereix coneixements avançats d'administració de sistemes.7

### **Serverless (FaaS): Abstracció i Escalabilitat Automàtica**

El model serverless permet als desenvolupadors executar codi (funcions) en resposta a esdeveniments sense haver de gestionar cap servidor. El proveïdor de núvol s'encarrega de tot el cicle de vida de la infraestructura.7

* **Costos**: Pagament per ús. Es factura segons el nombre de crides a la funció, el temps d'execució i la memòria consumida. Això elimina els costos de servidor inactiu, però pot esdevenir molt car amb trànsit elevat i constant.8  
* **Control**: Molt limitat pel que fa a l'entorn. El desenvolupador només controla el codi de la funció; no té accés al sistema operatiu subjacent ni pot configurar paràmetres de xarxa profunds.7  
* **Escenaris idonis**: Microserveis, processament de fitxers, APIs amb trànsit molt variable o esporàdic, i projectes on es vulgui reduir al màxim el "time to market" eliminant les tasques de DevOps.7  
* **Limitacions**: El problema de l'"arrencada en fred" (cold start) pot introduir latència en la primera crida després d'un període d'inactivitat. A més, existeix un cert grau de "vendor lock-in" a causa de les APIs específiques de cada proveïdor.7

| Característica | Shared Hosting | VPS Hosting | Serverless |
| :---- | :---- | :---- | :---- |
| **Model de Cost** | Fix mensual molt baix. | Fix mensual moderat. | Pagament per execució/consum. |
| **Accés a Root** | No. | Sí. | No. |
| **Gestió de Seguretat** | Proveïdor. | Usuari (OS) / Proveïdor (Hardware). | Proveïdor (Full Management). |
| **Escalabilitat** | Molt limitada. | Manual / Vertical. | Automàtica / Horitzontal. |
| **Aïllament** | Baix (recursos compartits). | Alt (Virtualització). | Molt alt (Sandbox/Contenidor). |
| **Configuració** | Panell web simple. | Línia de comandes / SSH. | Basada en codi / Consola Cloud. |

## **Seguretat i confiança en el web: Certificats SSL i Let's Encrypt**

En l'actualitat, el xifratge de les comunicacions entre el client i el servidor no és una opció, sinó un estàndard obligatori per a qualsevol aplicació web professional. Els certificats SSL (Secure Sockets Layer), evolucionats actualment a TLS (Transport Layer Security), són el mecanisme que garanteix la integritat, la privadesa i l'autenticitat de les dades en trànsit.11

### **La importància estratègica dels certificats SSL**

L'adopció d'HTTPS (la versió segura de HTTP que utilitza SSL/TLS) té múltiples dimensions. Des del punt de vista de la seguretat, protegeix les dades sensibles dels usuaris (claus de pas, dades bancàries) d'atacs de tipus "man-in-the-middle". Des del punt de vista del negoci, els navegadors moderns marquen els llocs sense SSL com a "no segurs", el que destrueix la confiança de l'usuari i augmenta la taxa de rebot.11 A més, el SEO (Search Engine Optimization) es veu directament afectat, ja que motors de cerca com Google prioritzen els dominis segurs en els seus resultats de cerca.11

### **Let's Encrypt: La revolució del xifratge gratuït**

Let's Encrypt és una autoritat de certificació (CA) gratuïta, automatitzada i oberta, impulsada per l'Internet Security Research Group (ISRG), una organització sense ànim de lucre.11 La seva missió és xifrar tot el web eliminant les barreres de cost i la complexitat tècnica associades tradicionalment als certificats SSL.  
Com s'obtenen els certificats mitjançant Let's Encrypt:

1. **Protocol ACME**: Let's Encrypt funciona mitjançant el protocol ACME (Automated Certificate Management Environment), que permet a un servidor web sol·licitar i renovar certificats sense intervenció humana.12  
2. **Validació del Domini**: El procés comença amb un repte que demostra que el sol·licitant té el control del domini. Això pot ser mitjançant la col·locació d'un fitxer en una ruta HTTP específica o mitjançant la creació d'un registre DNS.13  
3. **Clients d'automatització (Certbot)**: Per als usuaris que gestionen els seus propis servidors (com un VPS), s'utilitza una eina anomenada Certbot. Aquest client interactua amb l'API de Let's Encrypt, supera els reptes de validació i configura automàticament el servidor web (Nginx o Apache) per utilitzar el nou certificat.14  
4. **Renovació Automàtica**: Els certificats de Let's Encrypt tenen una durada curta de 90 dies per augmentar la seguretat. No obstant això, el sistema està dissenyat per renovar-se automàticament cada 60 dies mitjançant tasques programades, garantint que el lloc mai quedi desprotegit.13  
5. **Integració en PaaS**: Plataformes com Vercel, Netlify o Cloudways integren Let's Encrypt de manera nativa, pel que l'usuari només ha d'activar una opció en el panell per obtenir el certificat de manera instantània i sense cost.11

## **El procés de construcció (Build Process) en l'ecosistema modern**

En el desenvolupament d'aplicacions web modernes, especialment les basades en JavaScript, el codi que escriu el desenvolupador no és el mateix que s'executa en el navegador. El "build process" és el conjunt de transformacions que preparen el codi per ser consumit de manera eficient.16

### **Per què és necessari un procés de construcció?**

El codi font sovint utilitza sintaxi moderna (ES6+), llenguatges com TypeScript o marcs de treball com React/Vue que els navegadors no entenen directament. A més, el codi està dividit en centenars de fitxers per facilitar el manteniment, però carregar tants fitxers petits en un navegador seria extremadament lent a causa de la sobrecarrega de les peticions HTTP.16  
Les tasques clau d'un procés de construcció inclouen:

* **Bundling (Empaquetament)**: Combinar molts fitxers petits en un o pocs paquets ("bundles") per minimitzar les peticions al servidor.16  
* **Transpilació**: Convertir codi nou (o TypeScript) en JavaScript antic compatible amb la majoria de navegadors.17  
* **Minificació**: Eliminar espais en blanc, comentaris i reduir els noms de les variables per fer que el fitxer sigui el més petit possible.16  
* **Tree Shaking**: Una tècnica d'optimització que elimina el codi que s'ha importat però que mai s'arriba a utilitzar realment en l'aplicació.20  
* **Gestió d'actius**: Processar i optimitzar imatges, CSS i altres recursos estàtics.16

### **Eines de construcció: Webpack i Vite**

L'evolució de les eines de construcció ha marcat el ritme del desenvolupament web.  
**Webpack** ha estat el pilar de la indústria des de 2012\. És un empaquetador extremadament flexible i configurable que pot gestionar gairebé qualsevol tipus d'actiu mitjançant "loaders" i "plugins".21 Tanmateix, a mesura que les aplicacions han crescut, Webpack s'ha tornat lent en entorns de desenvolupament, ja que ha de reconstruir grans parts del bundle en cada canvi.24  
**Vite** (pronunciat "veet") representa el canvi de paradigma cap a la velocitat. En lloc d'empaquetar tot el codi per al desenvolupament, Vite aprofita els mòduls ES natius (ESM) dels navegadors moderns per servir els fitxers sota demanda. Això resulta en un temps d'arrencada del servidor de desenvolupament instantani i una recàrrega en calent (HMR) extremadament ràpida.21 Per a producció, Vite utilitza Rollup, el que permet generar paquets altament optimitzats.24

| Característica | Webpack | Vite |
| :---- | :---- | :---- |
| **Arquitectura de Dev** | Bundling-first (empaqueta abans de servir). | ESM-first (serveix sota demanda). |
| **Velocitat d'Arrencada** | Lenta en projectes grans (segons o minuts). | Instantània (milisegons). |
| **Configuració** | Complexa i sovint farragosa. | Senzilla i minimalista. |
| **Ecosistema** | Immens i madur (des de 2012). | Modern i creixent (des de 2020). |
| **Cas d'ús ideal** | Aplicacions corporatives gegants amb requeriments antics. | Aplicacions modernes que prioritzen l'agilitat i la velocitat. |

## **Flux bàsic d'un pipeline CI/CD: Automatització total**

El pipeline de CI/CD (Continuous Integration / Continuous Deployment) és l'artèria que transporta el codi des del repositori del desenvolupador fins a l'usuari final de manera segura i repetible. L'objectiu és eliminar la intervenció manual, que és la font principal d'errors en els desplegaments.26

### **El cicle de vida del pipeline**

Un pipeline típic s'activa automàticament cada vegada que s'envia codi al repositori central (com GitHub, GitLab o Bitbucket).

#### **1\. Etapa de Testeig (Continuous Integration)**

L'objectiu és assegurar que el nou codi no introdueix regressions ni trenca la funcionalitat existent.

* **Linting**: Es verifica que el codi segueixi els estàndards d'estil de l'empresa.  
* **Unit Tests**: Es proven les unitats més petites de lògica de manera aïllada.  
* **Security Scanning**: S'analitzen les dependències a la recerca de vulnerabilitats conegudes.28

#### **2\. Etapa de Construcció (Build)**

Un cop els tests han passat, es procedeix a generar els artefactes que es desplegaran.

* En aplicacions web, s'executa el procés de construcció (per exemple, npm run build) per generar el codi minificat i optimitzat.16  
* En entorns basats en contenidors, s'empaqueta l'aplicació en una imatge de Docker i s'envia a un registre d'imatges.28

#### **3\. Etapa de Desplegament (Continuous Deployment)**

L'artefacte es mou a la infraestructura de producció o de staging.

* Es poden utilitzar estratègies com el "Blue-Green Deployment" o els "Rolling Updates" per minimitzar el temps d'inactivitat.  
* Eines com Flux CD apliquen el principi de GitOps: el clúster de producció monitoritza el repositori de Git i s'actualitza automàticament per reflectir l'estat definit en el codi, eliminant la necessitat d'executar ordres manuals com kubectl.26

### **Flux de treball exemplificat amb GitHub Actions**

GitHub Actions permet definir aquests fluxos mitjançant fitxers YAML. Un flux de treball bàsic inclou un disparador (com un push), un sistema operatiu d'execució (runner) i una sèrie de passos:

1. **Checkout**: Descarrega el codi al runner.  
2. **Setup Environment**: Instala la versió correcta de Node.js, Python o Java.  
3. **Install Dependencies**: Executa npm install o pip install.  
4. **Run Tests**: Executa la suite de proves.  
5. **Build and Push**: Genera l'artefacte i el desplega al proveïdor de núvol (Azure, AWS, Vercel, etc.).28

## **El paradigma dels contenidors Docker**

Docker ha revolucionat el desplegament de programari mitjançant la contenidorització, una forma lleugera de virtualització que permet empaquetar una aplicació amb totes les seves dependències, configuracions i entorn d'execució en una única unitat portàtil.32

### **Beneficis sobre els entorns tradicionals**

En els entorns tradicionals, els desenvolupadors instal·laven les dependències directament al sistema operatiu del servidor. Això portava sovint a conflictes de versions i a la impossibilitat de replicar l'entorn exactament entre diferents màquines.

* **Aïllament**: Cada contenidor s'executa de manera aïllada en el seu propi espai d'usuari. Això permet que una aplicació que necessita Python 3.8 i una altra que necessita Python 3.12 s'executin al mateix servidor físic sense conflictes.33  
* **Lleugeresa**: A diferència de les màquines virtuals (VM), els contenidors no inclouen un sistema operatiu complet. Comparteixen el nucli (kernel) de l'amfitrió, el que significa que arrenquen en segons i consumeixen molta menys RAM i CPU.35  
* **Consistència**: Una imatge de Docker és immutable. Si funciona a l'ordinador del desenvolupador, funcionarà exactament igual en el servidor de producció, eliminant per complet el problema de "funciona a la meva màquina".33

### **Com Docker resol la inconsistència d'entorns**

Docker utilitza un fitxer anomenat Dockerfile per definir pas a pas com s'ha de construir l'entorn. Això inclou el sistema operatiu base (com Alpine Linux per a la lleugeresa), les variables d'entorn, els permisos de fitxers i les comandes d'instal·lació. Quan un equip comparteix una imatge de Docker, està compartint no només el codi, sinó tot l'univers on aquest codi "viu", garantint que tots els membres de l'equip i tots els servidors utilitzin la mateixa configuració bit a bit.33

| Aspecte | Entorn Tradicional / VM | Contenidors Docker |
| :---- | :---- | :---- |
| **Abstracció** | Virtualització de Hardware. | Virtualització d'Espai d'Usuari (Kernel). |
| **Mida** | GBs (Sistema Operatiu sencer). | MBs (Només dependències de l'app). |
| **Velocitat** | Minuts per arrencar. | Milisegons per arrencar. |
| **Aïllament** | Total (Hypervisor). | Processos aïllats pel Kernel (Namespaces). |
| **Portabilitat** | Difícil entre proveïdors. | Total (Corre on corre el Docker Engine). |

## **Errors comuns en els desplegaments i com diagnosticar-los**

Identificar per què una aplicació falla en producció quan funcionava perfectament en l'entorn local és una de les habilitats més crítiques d'un enginyer de programari. Aquests problemes solen derivar de diferències ambientals subtils.38

### **1\. Variables d'entorn no configurades o incorrectes**

Les variables d'entorn (ENV vars) s'utilitzen per emmagatzemar dades sensibles (claus d'API, contrasenyes de BD) i paràmetres de configuració que canvien segons l'entorn.42

* **L'error**: El desenvolupador oblida afegir una variable al dashboard de producció (com el de Vercel o Render) que tenia localment en el seu fitxer .env.  
* **El síntoma**: L'aplicació cau en arrencar amb un error de tipus "ReferenceError" o "Undefined", o falla en intentar connectar-se a un servei extern.39  
* **La solució**: Utilitzar biblioteques de validació d'entorn (com Joi o Dotenv-safe) que impedeixin que l'aplicació s'inicii si falten variables obligatòries.43

### **2\. Dependències faltants o desajust de versions**

Aquest problema passa quan una llibreria s'ha instal·lat localment però no s'ha guardat correctament en el fitxer de manifest de dependències (package.json, requirements.txt).

* **L'error**: Pushing codi que importa un paquet que no està llistat a les dependències del projecte.  
* **El síntoma**: Errors durant la fase de construcció o en temps d'execució com "Module not found".38  
* **La solució**: Utilitzar fitxers de bloqueig (package-lock.json o yarn.lock) que garanteixin que la versió exacta utilitzada en desenvolupament sigui la que s'instal·la en producció.40

### **3\. Permisos de fitxers i sistemes operatius**

Les diferències entre desenvolupar en Windows o macOS i desplegar en un servidor Linux (que és l'estàndard) causen errors frustrants.

* **Majúscules i minúscules**: Linux és sensible a majúscules (case-sensitive). Si importes ./Fitxer.js però el fitxer es diu ./fitxer.js, el codi funcionarà a Windows però fallarà a Linux.38  
* **Permisos d'usuari**: En producció, els serveis s'executen sovint amb usuaris sense permisos d'administrador. Una aplicació que intenta escriure logs en una carpeta on no té permisos fallarà.38  
* **Separadors de rutes**: Windows utilitza backslashes (\\) mentre que Linux utilitza forward slashes (/). Hardcodar rutes pot trencar l'aplicació.38

### **4\. Gestió d'errors i silenci del servidor**

Molts errors en producció es registren en fitxers de logs interns del servidor i no es mostren al navegador per seguretat. Si un desenvolupador només mira la finestra del navegador, pot no adonar-se que l'aplicació ha fallat silenciosament a causa d'un límit de memòria o una mala configuració del proxy.38

## **Conclusió: La decisió estratègica de Vercel sobre Shared Hosting**

Per a un equip de desenvolupament modern, la tria entre un allotjament compartit tradicional i una plataforma com Vercel es redueix a una qüestió d'eficiència operativa i velocitat de lliurament.  
Mentre que en un Shared Hosting o un VPS l'equip ha de gestionar manualment el servidor, la seguretat, els certificats SSL i el procés de desplegament (sovint via FTP o scripts manuals), **Vercel automatitza tot el cicle de vida**. Ofereix desplegaments instantanis a cada "git push", entorns de previsualització per a cada branca (permetent que els stakeholders revisin el codi abans de fusionar-lo) i escalabilitat automàtica sense intervenció.9  
Aquesta visió integral permet concloure que:

1. **Seguretat**: SSL amb Let's Encrypt és el mínim irreductible; Let's Encrypt ho fa possible sense fricció ni cost.11  
2. **Robustesa**: L'ús de Docker i pipelines CI/CD elimina el factor de l'error humà i la variabilitat ambiental.26  
3. **Configuració**: Les variables d'entorn han de ser tractades com a configuració externa per mantenir el codi net, segur i portàtil entre entorns.43  
4. **Construcció**: Eines modernes com Vite estan desplaçant els empaquetadors tradicionals per oferir una experiència de desenvolupament radicalment més ràpida.21

El desplegament no és el final del desenvolupament, sinó l'inici del cicle de vida útil de l'aplicació, i la seva automatització és la millor inversió que una organització pot realitzar per garantir el seu èxit tècnic i comercial.

#### **Obras citadas**

1. Staging vs Production Environments: Best Practices for Startups \- KodekX \- Medium, fecha de acceso: mayo 3, 2026, [https://kodekx-solutions.medium.com/staging-vs-production-environments-best-practices-for-startups-7c3372e21fd1](https://kodekx-solutions.medium.com/staging-vs-production-environments-best-practices-for-startups-7c3372e21fd1)  
2. Skipping staging could be your biggest deployment mistake \- NTT DATA, fecha de acceso: mayo 3, 2026, [https://services.global.ntt/en-us/insights/blog/skipping-staging-could-be-your-biggest-deployment-mistake](https://services.global.ntt/en-us/insights/blog/skipping-staging-could-be-your-biggest-deployment-mistake)  
3. You might not need staging \- ivelum, fecha de acceso: mayo 3, 2026, [https://ivelum.com/blog/you-might-not-need-staging/](https://ivelum.com/blog/you-might-not-need-staging/)  
4. It's Time To Kill Staging: The Case for Testing in Production \- DEV Community, fecha de acceso: mayo 3, 2026, [https://dev.to/signadot/its-time-to-kill-staging-the-case-for-testing-in-production-521a](https://dev.to/signadot/its-time-to-kill-staging-the-case-for-testing-in-production-521a)  
5. Shared Hosting vs VPS Hosting: What to Chоose | StormWall, fecha de acceso: mayo 3, 2026, [https://stormwall.network/resources/blog/shared-hosting-vs-vps](https://stormwall.network/resources/blog/shared-hosting-vs-vps)  
6. VPS vs Shared Hosting: When to Switch & What to Know, fecha de acceso: mayo 3, 2026, [https://www.scalahosting.com/blog/vps-vs-shared-hosting/](https://www.scalahosting.com/blog/vps-vs-shared-hosting/)  
7. Pros And Cons Of Serverless App Hosting Vs VPS Hosting \- Rad Web Hosting Blog, fecha de acceso: mayo 3, 2026, [https://blog.radwebhosting.com/pros-and-cons-of-serverless-app-hosting-vs-vps-hosting/](https://blog.radwebhosting.com/pros-and-cons-of-serverless-app-hosting-vs-vps-hosting/)  
8. Serverless Functions Vs Classic VPS: Cost And Performance For Small Apps \- DCHost.com, fecha de acceso: mayo 3, 2026, [https://www.dchost.com/blog/en/serverless-functions-vs-classic-vps-cost-and-performance-for-small-apps/](https://www.dchost.com/blog/en/serverless-functions-vs-classic-vps-cost-and-performance-for-small-apps/)  
9. Vercel vs VPS Hosting: Features, Pricing & Performance (2026) | HostMyCode, fecha de acceso: mayo 3, 2026, [https://www.hostmycode.com/blog/vercel-vs-vps-hosting-features-pricing-performance-2026](https://www.hostmycode.com/blog/vercel-vs-vps-hosting-features-pricing-performance-2026)  
10. What's the difference in benefits between using a self-hosted VPS vs serverless compute from Cloudflare? : r/SaaS \- Reddit, fecha de acceso: mayo 3, 2026, [https://www.reddit.com/r/SaaS/comments/1od0n4z/whats\_the\_difference\_in\_benefits\_between\_using\_a/](https://www.reddit.com/r/SaaS/comments/1od0n4z/whats_the_difference_in_benefits_between_using_a/)  
11. How to Install Let's Encrypt SSL Certificate | Cloudways Help Center, fecha de acceso: mayo 3, 2026, [https://support.cloudways.com/en/articles/5129591-how-to-install-let-s-encrypt-ssl-certificate](https://support.cloudways.com/en/articles/5129591-how-to-install-let-s-encrypt-ssl-certificate)  
12. Let's Encrypt, fecha de acceso: mayo 3, 2026, [https://letsencrypt.org/](https://letsencrypt.org/)  
13. Free Let's Encrypt SSL: Out-of-Box Integration | Virtuozzo Blog, fecha de acceso: mayo 3, 2026, [https://www.virtuozzo.com/company/blog/free-ssl-certificates-with-lets-encrypt/](https://www.virtuozzo.com/company/blog/free-ssl-certificates-with-lets-encrypt/)  
14. Getting Started \- Let's Encrypt, fecha de acceso: mayo 3, 2026, [https://letsencrypt.org/getting-started/](https://letsencrypt.org/getting-started/)  
15. Free SSL Let's Encrypt Certificate for Your Website: A Guide | Swiss Made Host, fecha de acceso: mayo 3, 2026, [https://swissmade.host/en/blog/free-ssl-lets-encrypt-certificate-for-your-website-a-guide](https://swissmade.host/en/blog/free-ssl-lets-encrypt-certificate-for-your-website-a-guide)  
16. What is Front-End Bundling And Minification \- Startup House, fecha de acceso: mayo 3, 2026, [https://startup-house.com/glossary/what-is-front-end-bundling-and-minification](https://startup-house.com/glossary/what-is-front-end-bundling-and-minification)  
17. Understanding Sourcemaps: From Development to Production \- This Dot Labs, fecha de acceso: mayo 3, 2026, [https://www.thisdot.co/blog/understanding-sourcemaps-from-development-to-production](https://www.thisdot.co/blog/understanding-sourcemaps-from-development-to-production)  
18. Javascript Build Tools and Bundlers \- AlgoDaily, fecha de acceso: mayo 3, 2026, [https://algodaily.com/lessons/js-build-tools-and-bundlers](https://algodaily.com/lessons/js-build-tools-and-bundlers)  
19. Bundling and Minification | Microsoft Learn, fecha de acceso: mayo 3, 2026, [https://learn.microsoft.com/en-us/aspnet/mvc/overview/performance/bundling-and-minification](https://learn.microsoft.com/en-us/aspnet/mvc/overview/performance/bundling-and-minification)  
20. Modern Build Optimization Techniques for JavaScript Apps \- NamasteDev Blogs, fecha de acceso: mayo 3, 2026, [https://namastedev.com/blog/modern-build-optimization-techniques-for-javascript-apps/](https://namastedev.com/blog/modern-build-optimization-techniques-for-javascript-apps/)  
21. Webpack vs Vite: Choosing the Right Bundler for Modern Frontend Development | Syncfusion Blogs, fecha de acceso: mayo 3, 2026, [https://www.syncfusion.com/blogs/post/webpack-vs-vite-bundler-comparison](https://www.syncfusion.com/blogs/post/webpack-vs-vite-bundler-comparison)  
22. Vite vs. Webpack: A Head-to-Head Comparison \- Kinsta®, fecha de acceso: mayo 3, 2026, [https://kinsta.com/blog/vite-vs-webpack/](https://kinsta.com/blog/vite-vs-webpack/)  
23. Comparison of Build Tools \- Codecademy, fecha de acceso: mayo 3, 2026, [https://www.codecademy.com/article/comparison-of-build-tools](https://www.codecademy.com/article/comparison-of-build-tools)  
24. Vite vs. Webpack \- Key differences and use cases — Documentation \- App Generator, fecha de acceso: mayo 3, 2026, [https://app-generator.dev/docs/technologies/vite/vite-vs-webpack.html](https://app-generator.dev/docs/technologies/vite/vite-vs-webpack.html)  
25. Vite vs Webpack: Which Build Tool is Right for Your Project? \- DEV Community, fecha de acceso: mayo 3, 2026, [https://dev.to/get\_pieces/vite-vs-webpack-which-build-tool-is-right-for-your-project-1p08](https://dev.to/get_pieces/vite-vs-webpack-which-build-tool-is-right-for-your-project-1p08)  
26. Flux CD, fecha de acceso: mayo 3, 2026, [https://fluxcd.io/](https://fluxcd.io/)  
27. What is Flux CD? | CNCF, fecha de acceso: mayo 3, 2026, [https://www.cncf.io/blog/2023/09/15/what-is-flux-cd/](https://www.cncf.io/blog/2023/09/15/what-is-flux-cd/)  
28. Tutoriales para Acciones de GitHub \- GitHub Docs, fecha de acceso: mayo 3, 2026, [https://docs.github.com/es/actions/tutorials](https://docs.github.com/es/actions/tutorials)  
29. From Code to Kubernetes: Building a Full GitOps Pipeline with GitLab CI and FluxCD, fecha de acceso: mayo 3, 2026, [https://medium.com/@fenari.kostem/from-code-to-kubernetes-building-a-full-gitops-pipeline-with-gitlab-ci-and-fluxcd-aa6188ca517f](https://medium.com/@fenari.kostem/from-code-to-kubernetes-building-a-full-gitops-pipeline-with-gitlab-ci-and-fluxcd-aa6188ca517f)  
30. Tutorial: Implement CI/CD with GitOps (Flux v2) \- Azure Arc \- Microsoft Learn, fecha de acceso: mayo 3, 2026, [https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/tutorial-gitops-flux2-ci-cd](https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/tutorial-gitops-flux2-ci-cd)  
31. How to Build a Complete CI/CD Pipeline with Jenkins and Flux CD \- OneUptime, fecha de acceso: mayo 3, 2026, [https://oneuptime.com/blog/post/2026-03-13-cicd-pipeline-jenkins-flux-cd/view](https://oneuptime.com/blog/post/2026-03-13-cicd-pipeline-jenkins-flux-cd/view)  
32. Docker frente a VM \- Diferencia entre tecnologías de despliegue de aplicaciones \- AWS, fecha de acceso: mayo 3, 2026, [https://aws.amazon.com/es/compare/the-difference-between-docker-vm/](https://aws.amazon.com/es/compare/the-difference-between-docker-vm/)  
33. Get started | Docker Docs, fecha de acceso: mayo 3, 2026, [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)  
34. ¿Qué es Docker y cómo funciona? Ventajas de los contenedores Docker \- Red Hat, fecha de acceso: mayo 3, 2026, [https://www.redhat.com/es/topics/containers/what-is-docker](https://www.redhat.com/es/topics/containers/what-is-docker)  
35. ¿Alguien me puede explicar qué es Docker como si tuviera 5 años y en qué se diferencia de una máquina virtual? : r/learnprogramming \- Reddit, fecha de acceso: mayo 3, 2026, [https://www.reddit.com/r/learnprogramming/comments/vh2kgn/can\_someone\_eli5\_what\_docker\_is\_and\_how\_it/?tl=es-419](https://www.reddit.com/r/learnprogramming/comments/vh2kgn/can_someone_eli5_what_docker_is_and_how_it/?tl=es-419)  
36. Docker vs VM \- Difference Between Application Deployment Technologies \- AWS, fecha de acceso: mayo 3, 2026, [https://aws.amazon.com/compare/the-difference-between-docker-vm/](https://aws.amazon.com/compare/the-difference-between-docker-vm/)  
37. Contenedores (Docker) vs Máquinas Virtuales: ¿Qué es más seguro? \- YouTube, fecha de acceso: mayo 3, 2026, [https://www.youtube.com/watch?v=k0cijdaHMgY](https://www.youtube.com/watch?v=k0cijdaHMgY)  
38. Why Your Website Works Locally but Fails in Production | by Syn Ify | Medium, fecha de acceso: mayo 3, 2026, [https://medium.com/@emperorsyn/why-your-website-works-locally-but-fails-in-production-8f80d6632c22](https://medium.com/@emperorsyn/why-your-website-works-locally-but-fails-in-production-8f80d6632c22)  
39. Troubleshooting Your Deploy – Render Docs, fecha de acceso: mayo 3, 2026, [https://render.com/docs/troubleshooting-deploys](https://render.com/docs/troubleshooting-deploys)  
40. Why Does Your Code Break in Production but Work Perfectly Locally? \- DEV Community, fecha de acceso: mayo 3, 2026, [https://dev.to/nikhil\_sachapara/why-does-your-code-break-in-production-but-work-perfectly-locally-2jf3](https://dev.to/nikhil_sachapara/why-does-your-code-break-in-production-but-work-perfectly-locally-2jf3)  
41. Why Your Local Environment Doesn't Match Production: Solving the “It Works on My Machine” Syndrome \- AlgoCademy, fecha de acceso: mayo 3, 2026, [https://algocademy.com/blog/why-your-local-environment-doesnt-match-production-solving-the-it-works-on-my-machine-syndrome/](https://algocademy.com/blog/why-your-local-environment-doesnt-match-production-solving-the-it-works-on-my-machine-syndrome/)  
42. fecha de acceso: mayo 3, 2026, [https://medium.com/@elsy83853/environment-variables-in-deployment-best-practices-for-security-and-scalability-97fa9c3435d4\#:\~:text=Environment%20variables%20are%20indispensable%20in,vital%20for%20every%20aspiring%20developer.](https://medium.com/@elsy83853/environment-variables-in-deployment-best-practices-for-security-and-scalability-97fa9c3435d4#:~:text=Environment%20variables%20are%20indispensable%20in,vital%20for%20every%20aspiring%20developer.)  
43. Environment Variables in Deployment: Best Practices for Security and Scalability \- Medium, fecha de acceso: mayo 3, 2026, [https://medium.com/@elsy83853/environment-variables-in-deployment-best-practices-for-security-and-scalability-97fa9c3435d4](https://medium.com/@elsy83853/environment-variables-in-deployment-best-practices-for-security-and-scalability-97fa9c3435d4)  
44. Why do I need to store environment variables in a separate file when going to production?, fecha de acceso: mayo 3, 2026, [https://dev.to/doridoro/why-do-i-need-to-store-environment-variables-in-a-separate-file-when-going-to-production-1g6j](https://dev.to/doridoro/why-do-i-need-to-store-environment-variables-in-a-separate-file-when-going-to-production-1g6j)  
45. What Are Environment Variables? » ITU Online IT Training, fecha de acceso: mayo 3, 2026, [https://www.ituonline.com/tech-definitions/what-are-environment-variables/](https://www.ituonline.com/tech-definitions/what-are-environment-variables/)  
46. How to Fix Permissions Errors in Solutions \- DocJuris, fecha de acceso: mayo 3, 2026, [https://support.docjuris.com/hc/en-us/articles/13660100676365-How-to-Fix-Permissions-Errors-in-Solutions](https://support.docjuris.com/hc/en-us/articles/13660100676365-How-to-Fix-Permissions-Errors-in-Solutions)  
47. Vercel vs Netlify | Vercel Knowledge Base, fecha de acceso: mayo 3, 2026, [https://vercel.com/kb/guide/vercel-vs-netlify](https://vercel.com/kb/guide/vercel-vs-netlify)  
48. Heroku vs Vercel: comparison guide, fecha de acceso: mayo 3, 2026, [https://vercel.com/i/heroku-vs-vercel-comparison-guide](https://vercel.com/i/heroku-vs-vercel-comparison-guide)  
49. Vercel as a hosting platform: When It's the best choice and when it's not, fecha de acceso: mayo 3, 2026, [https://pagepro.co/blog/vercel-hosting-platform/](https://pagepro.co/blog/vercel-hosting-platform/)