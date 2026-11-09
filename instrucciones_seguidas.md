# Instrucciones seguidas

`Instala el mcp de playwright localmente`

`Utiliza playwright, abre http://localhost:3000 y revisa la consola`

`Utiliza playwright, abre http://localhost:3000 y genera una screenshot`

Se agregó `/.playwright-mcp` en el .gitignore

Para instalar el mcp de playwright
`npx ctx7 setup`
Y luego se cambio el Authorization con el token mio

`Necesito que investigues cuál es la manera de protección de rutas en Next.js. Usa el Context7 MCP`

Instalación de las skills de Fernando Herrera para SDD
`npx skills add klerith/fernando-skills` 

Añadimos en el agents.md:
`
Context 7 Usaremos este MCP para obtener documentación actualizada del framework.
`

Y luego ejecutamos 
`\init` 


Para empezar con el desarrollo, usando los skills de F. Herrera: 
`/spec Ocupamos implementar la plantilla @references/pantallas/feed.dc.html como nuestro home / . Aún no tenemos autenticación, ni base de datos. Solo necesito que el estilo luzca idéntico al proporcionado.`
Se fueron respondiendo a todas las preguntas y se generó el 01-home-feed.md


Implementamos los descrito en 01-home-feed.md, primero cambiamos a "**Estado:** Aprobado" y luego ejecutamos
`/spec-impl @specs/01-home-feed.md` 



Creación de un agente para verificar las pantallas creadas, con playwright. ( Solo se va a poder ejecutar con modelos que soporten imagenes como qwen3.6-plus ). Primero en modo plan: 

``` 
Necesito que creemos un agente personalizado :

Eres un agente verificador de los criterios de aceptación de un archivo de especificación (spec).

Tu labor es revisar, corregir y marcar los checks del "Acceptance criteria" de un spec.

Usa Context7 Para asegurarte de que se usaron las recomendaciones de next.js

Usa el MCP de Playwright para verificar cuando tiene que ver con pantallas creadas.

Debe de funcionar a nivel de proyecto y usar el modelo con visión [ejemplo: Qwen3.6 Plus], ya que soporta visión para comparar screenshots.

Este agente tiene que estar a nivel de proyecto, no global.
```

Respondemos las preguntas que nos pongan. Escogimos qwen3.6-plus; en cuanto a que agentes pueden verlo, respondimos  all (agente primario y subagente), en cuanto a "que significa corregir" especificamos una respuesta a mano indicando que spec + código, pero que tiene que estar a nivel de proyecto (que revise y pueda hacer cambios, pero a nivel de proyecto), a la pregunta si queremos que compruebe si está lanzada la aplicación dijimos que sí (y con esto crea `.opencode/command/verify-spec.md` )

Al teminar pusimos a modo build:
`sí, implementalo` 

Con esto creó `.opencode/agent/spec-verifier.md` y colateralmente el `.opencode/command/verify-spec.md`


Ejecutamos el agente, que verifique el spec 01 (el del home, creado antes):
`@spec-verifier @specs\01-home-feed.md` 
Con esto, en el md se marcarán con una "x" los criterios de aceptación (en mi caso ya los marcara antes)



Y al terminar le pusimos que
`Actualiza el AGENTS.md con el agente que nosotros acabamos de crear y el comando de /verify-spec".`




