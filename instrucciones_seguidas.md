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




Para agregar especificaciones para el desarrollo de las pantallas de "kids" (perfil y lista), usando los skills de F. Herrera: 
` /spec Necesitamos implementar únicamente el diseño como se ve en las pantallas de referencia @references/pantallas/perfil-nino.dc.html y @references/pantallas/ninos.dc.html . Solo quiero las interfaces y los componentes` 
En las respuestas:
- Debe de navegar a /kids /kids/[id], No quiero nombres de estas páginas en español.
- Reutilizar los componentes existentes
- Datos del mock en un archivo indepediente, si es posible
- Búsqueda en el lugar del frontend, todavía no quiero una conexión con el backend.
- Vamos a mantener una enumeración con ciertas alergias o ciertos tipos, y también sus colores. Por ahora todo ficticio.
- Los datos de Resumen del día y Padres vinculados son placeholders, es decir todo fictio, por ahora.

Implementamos los descrito en 02-kids-list-and-profile.md, primero cambiamos a "**Estado:** Aprobado" y luego ejecutamos
`/spec-impl @specs/02-kids-list-and-profile.md` 

Y luego verificamos usando el agente que creamos antes:
`@spec-verifier @specs/02-kids-list-and-profile.md` 



Con /spec se crearon las specificaciones de login, la modal de añadir un niño, el link de relacionar con un tutor/padre/madre y un nuevo modal para las publicaciones. Siguiendo el siguiente Flujo:


## Flujo de trabajo recomendado

1. **Describir el problema:**  
   Utiliza la skill `/spec` para crear el artefacto SDD.

2. **Revisión y aprobación:**  
   Revisa el artefacto generado y apruébalo si cumple los requisitos.

3. **Implementación:**  
   Ejecuta `/spec-impl` para comenzar la implementación guiada por el SDD.

4. **Revisión paso a paso:**  
   Verifica cada avance de la implementación de forma iterativa.

5. **Ajustes rápidos:**  
   Para cambios menores o correcciones, usa *one shot prompts*.

6. **Verificación automática:**  
   Apóyate en el agente `@spec-verifier` para validar la implementación.

7. **Marcar como implementado:**  
   Actualiza el estado del spec a **"implementado"**.

8. **Publicar cambios:**  
   Sube la rama al repositorio de Github y abre un *pull request*.

9. **Merge y limpieza remota:**  
   Haz *merge* en Github y elimina la rama en el repositorio remoto.

10. **Sincroniza tu entorno local:**  
    Cambia a la rama `main`, haz *pull* para traer los cambios y elimina la rama local si es necesario.



## Ejemplo Prompts para supabase y otros spec (recordar seguir el "Flujo de trabajo recomendado", recordando el @spec-verifier para validarlos )

/spec Vamos a crear la primera tabla de daycares

/spec Puedes ver la referencia en @docs. Y ocupamos aplicar el patrón de migraciones para impactar Supabase.

/spec Ocupamos implementar la tabla de usuarios y sus enumeraciones respectivas. Revisa @db-schema para tener las referencias de lo que tenemos que crear. Ocuparemos un usuario puede tener un daycare, pero un "daycare" puede tener muchos usuarios. Usaremos un usuario staff para poder probar, cuyo email será fernando@google.com y su password será Abc123456@

"Actualiza el AGENTS.md. Necesito que cualquier archivo de especificación creado si tiene que ver con la base de datos debe de ir en la carpeta de specs/database"


/spec Ocupamos implementar la parte de autenticación de nuestra aplicación, Recordando de que solo es email y password, Una vez creada la autenticación, también ocupamos hacer la protección de rutas. Usa el Context7 MCP para determinar cómo protegemos las rutas. Esto ya es real contra Supabase

/spec Vamos a implementar el mantenimiento de niños, (tabla children y rooms), ver @db-schema para las referencias recomendadas, Vamos a crear tres rooms por defecto. Uno de ellos tiene que ser la Sala Soles, Y no ocupamos ningún niño en la tabla. La pantalla a trabajar es /kids . Recuerda generar los archivos de migraciones.

/spec Vamos a trabajar en la vinculación de un padre a un niño, [Image 1], Vamos a generar un correo electrónico que va a ser enviado utilizando resend.com, el paquete de node, Necesitamos hacer la parte del registro de usuario utilizando el código y la invitación que vamos a enviar por correo. Recuerda generar los archivos de migraciones.

http://localhost:3000/activate?code=ZZRA2 Ese enlace debería de funcionar pero cuando ingreso a la pantalla de activar la cuenta. El problema es que la página /activate es pública (sin autenticación), pero la política RLS de invitations requiere auth.uid() para leer. Como el usuario no está logueado, auth.uid() es null y la consulta falla.




Primero se añadió la SUPABASE_SERVICE_ROLE_KEY en el .env, que he obtenido en el dashboard de Supabase -> Project Settings -> API Keys -> Pestaña Legacy anon, service_role API keys ->  service_role (secret). En Supabase, tambien fuimos a Autentication > Configuration > Sign In/ Providers > Deschequeamos el "Allow manual linking".  Y luego el prompt fue:
"Hay un error y es porque signUp envía email de confirmación y hay rate limit. Para el flujo de activación no necesitamos confirmación por email (ya se verificó con el código de invitación).
He añadido la SUPABASE_SERVICE_ROLE_KEY en el .env, para usar el Admin API y crear el usuario sin enviar email. Modifica el flujo de activación para solucionar el error."


"Hay un problema porque después de crear el usuario con el Admin API, no hay sesión activa todavía. El cliente normal (supabase) no tiene auth.uid(), así que la política RLS de parent_children falla. Soluciona el error."

"Actualiza el Readme para que explique como levantar el proyecto. Además recuerda que estamos usando MCP de Supabase, quiero que  en el Readme tambien expliques como se usa el CLI de Supabase para el login y autenticarse"



## Ejemplo Prompt para crear un agente secundario para revisar best practices de react

Con modo build :
```
Vamos a crear un nuevo agente

react-best-practices: Va a aplicar las mejores prácticas de React en todos los archivos que nosotros le indiquemos y vas a usar context-7 para verificar si está siguiendo las buenas prácticas y las últimas recomendaciones de la documentación
```

Ha realizado la pregunta:
Para crear el agente react-best-practices necesito escribir en .opencode/agent/, pero los permisos actuales bloquean edits ahí. ¿Cómo prefieres proceder?
Hemos respondido:
Agregar permisos para .opencode/


Luego para usarlo:
`Usa el subagente @react-best-practices para revisar el componente XYZ.ts y el component zYx.ts, puedes usar dos agentes para hacer la revisión más rápido`

Luego puedes usar las teclas de flechas para movernos por esos dos subagentes... y con ctrl+x flejaAbajo



## Ejemplo Prompt para crear un agente especializado para manejar la Base de datos

Con modo plan, para que pregunte lo que necesite:

```
Ocupamos crearnos un subagente llamado db-migrator. Este es un agente que se va a encargar de asegurarse de que existan las migraciones y de aplicarlas
```

Escogimos:
- subagente automático

- ¿De dónde saca el agente qué migraciones necesita crear? ¿De specs de base de datos, del reference db-schema, o ambos? Dijimos:
A todos los specs que involucren base de datos


- ¿El agente solo aplica migraciones existentes, o también las crea si faltan?     Validar + crear + aplicar


Luego para usarlo:
`/db-migrate revisa si hay alguna migración pendiente de crear`





## Ejemplo Prompt para crear un agente especializado en accesibilidad

Con modo plan, para que pregunte lo que necesite:
`Vamos a crear el siguiente agente @accessibility-checker La idea es que nos ayude con la accesibilidad y seguir las buenas prácticas de WCAG 2.2 AA, Yo te voy a indicar qué archivo es el que debes de revisar`

¿Solo React/TSX o también HTML/CSS puro? -> Dado que el proyecto es Next.js, ¿te enfoco en TSX + Tailwind?           Sí también

¿El agente debe poder aplicar fixes automáticamente o solo reportar?                                                 Sí debe de aplicar los fixes

¿Quieres que incluya verificación de colores del design system (#f6ecdf, #d9583c, etc.) contra contraste WCAG?    Sí que vaya con el contraste WCAG


Sí, Creemos el agente y el comando



Luego para usarlo:
`@accessibility-checker @app/(auth)/login/page.tsx`

Este agente tambien se puede usar pulsando Ctl+Tab, por ser un agente como Plan o Build , para que esto no pase hay que ir a su .md y en lugar de mode: all, hay que poner mode: subagent





## Ejemplo Prompt para crear un agente especializado en seguridad de la base de datos

Con modo plan, para que pregunte lo que necesite:

```
Necesitamos crear un agente nuevo el cual se va a llamar db-security-auditor , y que pueda invocar con @db-security-auditor. Este agente previene fugas de datos entre niños y padres por role of security mal configurado y demás buenas prácticas de base de datos especializadas en Supabase
```


Sí, Creemos el agente y el comando


Luego para usarlo:
`@db-security-auditor Revisa la tabla de usuarios, y solo la tabla de usuarios`

Finalmente en el curso no se aplicó.



## Ejemplo Prompt de creación de un cron job


```
Necesitamos ejecutar un cron job que haga opencode run /db-audit Todos los viernes a las 6:00 de la tarde.

Necesito ejemplos de cómo se implementaría con cada una de las siguientes opciones:

1 - Cron del sistema (macOS/Linux)

1.1 - Task Scheduler (recomendado - GUI)

1.2 - PowerShell (script + scheduled task)

1.3 - launchd (nativo macOS - recomendado)

2 - Supabase Cron (pg_cron) - si el agente hace tareas de base de datos

3 - GitHub Actions - si el repo está en GitHub

Si no puedes hacerlo con el de GitHub, no te preocupes, sáltatelo
```





## Ejemplo Prompt para actualizar los Agents.md con los agentes creados hasta el momento

`Actualiza el Agents.md con los agentes que actualmente tenemos creados, con una breve descripción de su labor`



