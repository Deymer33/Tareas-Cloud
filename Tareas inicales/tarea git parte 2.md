1. Flujos de Trabajo con Git (Branching Strategies):

* Tarea: Investigar los diferentes flujos de trabajo y estrategias de branching en Git:
1. **Gitflow:** esta utiliza múltiples ramas específicas para diferentes propósitos:
    main: Contiene la versión estable lista para producción.
    develop: Contiene la versión en desarrollo, donde se integran las nuevas características antes de pasar a producción.
    Feature branches: Ramas dedicadas a nuevas características o mejoras. Se crean desde develop y se fusionan de vuelta al completarlas.
    Release branches: Se crean desde develop para preparar una nueva versión. Aquí se realizan pruebas finales y correcciones antes de fusionarse en main y develop.
    Hotfix branches: Ramas utilizadas para solucionar problemas críticos en producción. Se crean desde main y se fusionan tanto en main como en develop.

2.  **GitHub Flow:** es un flujo de trabajo simplificado y ligero, diseñado para proyectos que priorizan la entrega continua. Se basa principalmente en el uso de la rama main y ramas temporales para trabajar en cambios específicos:
    Todo comienza en la rama main, que siempre debe estar lista para producción.
    Para desarrollar una nueva característica o corregir un error, se crea una rama desde main (por ejemplo, feature/nueva-funcionalidad).
    Una vez que el trabajo en la rama está completo, se realiza un Pull Request para que otros revisen el código antes de fusionarlo de vuelta a main.
    Las ramas se eliminan después de fusionarse.

3.  **GitLab Flow:** combina elementos de Gitflow y GitHub Flow, enfocándose en integrar ramas con entornos de desarrollo y producción. Es ideal para proyectos que manejan múltiples entornos (por ejemplo, staging, pre-production, production).
    Se utiliza una rama main para producción y otras ramas específicas para integrar cambios con diferentes entornos.
    Incluye un concepto llamado environment branches, donde los cambios pueden ser fusionados en ramas asociadas a entornos antes de llegar a main.
    Promueve el uso de Merge Requests para revisión de código.

4.  **Trunk-Based Development:** en este flujo, los desarrolladores trabajan directamente sobre una única rama principal (trunk o main) y realizan integraciones frecuentes. Cualquier nueva funcionalidad o corrección se desarrolla en ramas de vida corta (short-lived branches), que se fusionan rápidamente en main.
    Los cambios son pequeños y se integran varias veces al día.
    Se apoya en herramientas de automatización, como pruebas continuas, para garantizar que el main siempre esté estable.

---

2.  Comandos Avanzados de Git:

    **cherry-pick** Este comando se utiliza para aplicar un commit específico de una rama a otra, sin necesidad de fusionar toda la rama.

```git
git cherry-pick <commit-hash>
```

**rebase:** se utiliza para mover o reescribir commits en una nueva base. Es útil para mantener un historial de commits limpio y lineal.

```git
git rebase <branch>

```
**stash:** guarda temporalmente los cambios no confirmados en un área de almacenamiento para permitir cambiar de rama sin perder el trabajo.
```git
git stach

```    
**reflog:** registra todos los cambios que ocurren en los punteros de las ramas locales, incluso aquellos que no están en el historial.
```git
git reflog
```
**tag:**  se utiliza para marcar puntos específicos en el historial, generalmente usados para identificar versiones.
```git
ggit tag <tag-name>
```

**blame:** muestra quién hizo qué cambio en cada línea de un archivo.
```git
git blame <file>
```
**bisect:** utiliza una búsqueda binaria para identificar el commit donde se introdujo un error.
```git
git bisect start
git bisect bad <bad-commit>
git bisect good <good-commit>

```


