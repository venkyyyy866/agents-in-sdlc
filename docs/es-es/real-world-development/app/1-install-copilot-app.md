---
title: "Lección 1 - Instala la aplicación GitHub Copilot"
description: "Instala la aplicación GitHub Copilot, conecta el repositorio creado a partir de la plantilla, conoce el espacio de trabajo y prueba un chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La **[aplicación GitHub Copilot][about-copilot-app]** es una aplicación de escritorio para el desarrollo con agentes. Está basada en GitHub Copilot CLI y se integra de forma nativa con GitHub, por lo que los repositorios, las ramas y las canalizaciones de CI funcionan desde el principio. Está diseñada para flujos de trabajo en los que diriges varios agentes en paralelo, cada uno en su propio espacio de trabajo aislado, en lugar de realizar todo el trabajo por tu cuenta y automatizar tareas repetitivas. Ahora que Node.js está instalado y tienes una copia del proyecto preparada, el siguiente paso es instalar la aplicación y conectar el repositorio.

En esta lección:

- instalarás la aplicación GitHub Copilot e iniciarás sesión.
- añadirás a la aplicación tu proyecto desde su repositorio de GitHub.
- conocerás el espacio de trabajo y el backlog que ha creado la plantilla.
- probarás un chat rápido para conocer mejor la aplicación.

## Escenario

Tu equipo está empezando a utilizar agentes de IA para abordar un backlog cada vez mayor. La aplicación Copilot permite dirigir todo ese trabajo desde un mismo lugar: seleccionar incidencias, ejecutar agentes, revisar cambios y combinar solicitudes de incorporación de cambios. En esta lección instalarás y conectarás la aplicación y aprenderás a iniciar una conversación sobre el proyecto.

> [!NOTE]
> Necesitas un plan de Copilot compatible: Copilot Free, Copilot Student o cualquier plan de pago (Pro, Pro+, Business o Enterprise). Si utilizas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva **GitHub Copilot app**.

## Instala y configura la aplicación GitHub Copilot

Para utilizar la aplicación GitHub Copilot, primero hay que instalarla. Hay versiones para Windows, macOS y Linux. Vamos a instalarla, autenticarnos y añadir el repositorio de Tailspin Toys.

1. En un navegador, abre la [página de la aplicación GitHub Copilot][download-app].
2. Descarga la aplicación para tu plataforma e instálala siguiendo las instrucciones de la página.
3. Abre la aplicación una vez instalada.
4. Selecciona **Sign in to GitHub** y sigue las instrucciones para iniciar sesión con una cuenta de GitHub.com o GHE.com. Si utilizas GitHub Enterprise Cloud con residencia de datos, selecciona **GitHub Enterprise Cloud** y escribe el nombre de host `*.ghe.com` cuando se te solicite.

   Si utilizas GitHub Enterprise Server, primero completa la incorporación con tu cuenta en la nube. Después, abre **Settings**, selecciona **Accounts**, selecciona **Add account** y elige **GitHub Enterprise Server**. Sigue las instrucciones para autorizar la aplicación en el navegador, tal como se explica en la [guía de inicio de sesión de Enterprise Server][ghes-sign-in].

5. Si durante la configuración se te pide que selecciones un repositorio, selecciona el repositorio de Tailspin Toys que has creado a partir de la plantilla. También puedes omitir este paso y añadir el proyecto más adelante.
6. Cuando se te solicite, elige un tema y completa la configuración.
7. Busca el repositorio en **Sessions**, en la barra lateral. Si ya aparece, no hace falta volver a añadirlo.
8. Si todavía no está conectado, selecciona **+** junto a **Sessions** para crear una sesión y, después, selecciona **Add GitHub repository**. Escribe el propietario y el nombre del repositorio que anotaste en la lección de requisitos previos.
9. Confirma que el repositorio aparece en la barra lateral. En esta vista, las carpetas de los repositorios, como `tailspin-toys`, aparecen agrupadas en **Sessions** y las sesiones individuales se muestran debajo de cada repositorio.

## Familiarízate con el espacio de trabajo

Con el proyecto conectado, dedica un momento a conocer la aplicación. La barra lateral organiza el espacio de trabajo en varias áreas:

- **New**: inicia una sesión de chat con Copilot.
- **Pull requests**: muestra las solicitudes de incorporación de cambios mediante la integración nativa con GitHub. Puedes explorarlas, filtrarlas, consultar el estado de CI y revisarlas sin salir de la aplicación.
- **Issues**: muestra las incidencias de la misma forma. Puedes explorarlas, filtrarlas e iniciar una sesión a partir de una incidencia.
- **Automations**: tareas guardadas del agente que se ejecutan según una programación o cuando las inicias. Son útiles para gestionar listas de tareas, el mantenimiento periódico del proyecto u otras tareas rutinarias. Se mencionan como posible paso siguiente en el resumen; no forman parte de otro ejercicio del taller.
- **Customize**: añade funciones a la aplicación Copilot mediante servidores MCP, complementos, aptitudes y otros componentes. La utilizarás para configurar Playwright MCP.
- **Chats**: conversaciones sencillas para hacer preguntas o intercambiar ideas sin necesitar una rama ni un espacio de trabajo propios. Esta sección aparece después del primer chat. Si no está visible, selecciona **+** junto a **Sessions** para iniciar el primer chat.
- **Sessions**: agrupa las carpetas de los repositorios y las sesiones de agente. Selecciona un repositorio, como `tailspin-toys`, para abrir su vista, o selecciona una sesión debajo para volver a la conversación. Cada sesión se ejecuta en su propio espacio de trabajo aislado, por lo que puedes ejecutar varias sin que interfieran entre sí. Iniciarás la primera sesión cuando añadas las valoraciones con estrellas.

A medida que avances en el taller, explorarás el espacio de trabajo.

> [!TIP]
> Si tienes dudas, pregunta a Copilot. Si no sabes cómo hacer algo o si una opción está disponible, Copilot puede orientarte.

### Busca el backlog precargado

Es probable que todos los proyectos tengan un backlog, y Tailspin Toys no es una excepción. Vamos a explorar el backlog que se creó al generar el proyecto a partir de la plantilla.

1. En **Sessions**, en la barra lateral, selecciona la carpeta del repositorio de Tailspin Toys, no una sesión individual. Después, selecciona **Issues** en la navegación superior del repositorio.
2. Busca estas incidencias por su título; no des por hecho que sus números coinciden:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecciona una incidencia y lee sus detalles. Cada incidencia también permite iniciar una sesión de agente. Después de hacer un primer cambio rápido, partirás de la incidencia de filtrado.

> [!NOTE]
> Las listas de **Issues** y **Pull requests** se filtran automáticamente para mostrar únicamente los elementos de los repositorios que has añadido a la aplicación Copilot. Para ver trabajo de otros repositorios, añádelos a la aplicación.

## Prueba un chat rápido

Una buena manera de familiarizarte con la aplicación es utilizarla para conocer la propia aplicación. Para eso sirve un **chat rápido**: puedes hacer una pregunta o intercambiar ideas sin crear una rama o un árbol de trabajo. Es ideal para preguntas breves y temporales, sin necesidad de iniciar una sesión.

1. En la barra lateral, selecciona **+** junto a **Chats** para abrir un chat. Si **Chats** todavía no aparece, selecciona **+** junto a **Sessions** para iniciar tu primer chat; después aparecerá la sección **Chats**.
2. Pregunta cómo funcionan las sesiones de la aplicación:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. Lee la respuesta en la vista de conversación. Cada sesión se ejecuta en su propio árbol de trabajo de Git aislado, lo que permite ejecutar varios agentes en paralelo sin que sus cambios interfieran entre sí. Puedes continuar la conversación o iniciar otra en cualquier momento.

## Resumen y pasos siguientes

¡Enhorabuena! Has instalado la aplicación GitHub Copilot, conectado el proyecto y explorado el espacio de trabajo. Has aprendido a:

- instalar la aplicación e iniciar sesión en GitHub.
- añadir un proyecto desde su repositorio de GitHub.
- conocer el espacio de trabajo y buscar el backlog precargado en **Issues**.
- utilizar un chat rápido para hacer una pregunta breve y temporal.

A continuación, [iniciarás tu primera sesión de agente][next-lesson] y la utilizarás para mostrar las valoraciones con estrellas en las tarjetas de juegos.

## Recursos

- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Primeros pasos con la aplicación GitHub Copilot][getting-started]
- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
[ghes-sign-in]: https://docs.github.com/enterprise-server@3.22/copilot/copilot-on-ghes/sign-in-on-copilot-app
