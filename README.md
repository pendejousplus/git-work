# git-work — flujo colaborativo con Git

Repositorio de la AE1 del módulo DPL. La práctica consiste en crear y
documentar una página estática para una startup y recorrer un flujo de trabajo
colaborativo con GitHub: ramas, issues, pull requests, revisión, resolución de
conflictos, etiquetas y releases.

La página de ejemplo presenta **Guaridas S.L.**, una startup ficticia de
búsqueda de vivienda. No implementa un buscador funcional.

## Índice

- [Entorno e instalación](#entorno-e-instalación)
- [Estructura y configuración](#estructura-y-configuración)
- [Flujo colaborativo](#flujo-colaborativo)
- [Issues y pull requests](#issues-y-pull-requests)
- [Comprobaciones](#comprobaciones)
- [Problemas y soluciones](#problemas-y-soluciones)
- [Repositorio y publicación](#repositorio-y-publicación)

## Entorno e instalación

No se necesitan dependencias para ver la página. Clona el repositorio y abre
`index.html` en un navegador:

```bash
git clone https://github.com/pendejousplus/git-work.git
cd git-work
```

La documentación se genera con MkDocs. Para construirla localmente, instala
Python y MkDocs y ejecuta:

```bash
python -m pip install mkdocs
mkdocs build --strict
```

## Estructura y configuración

- `index.html`: portada de la startup.
- `css/cover.css`: estilos de la portada. Las reglas `.btn-secondary` controlan
  el color y la sombra del botón principal.
- `docs/index.md` y `mkdocs.yml`: portada y navegación de la documentación.
- `.github/workflows/ci.yml`: ejecuta `mkdocs build --strict` en cada push a
  `main`, pull request y ejecución manual.
- `.gitignore`: excluye archivos locales como `.env`, logs y `.DS_Store`.

Para cambiar el color del botón, edita `color` en el bloque `.btn-secondary`;
para cambiar su sombra, edita `text-shadow`. Es mejor localizar las propiedades
por selector que por número de línea, porque las líneas pueden cambiar.

## Flujo colaborativo

El historial del repositorio incluye la creación de la página y la
documentación, la personalización de la portada en la rama `custom-text` y su
integración mediante un commit de merge identificado como PR #3. También incluye
el cambio del botón a `darkgreen` y un commit posterior que añade la sombra y
referencia `Closes #4`.

La etiqueta anotada `0.1.0` apunta al commit de la sombra. La release pública
describe esta versión como la primera versión del sitio de la startup.

## Issues y pull requests

### Issues

| Issue | Estado | Resultado |
| --- | --- | --- |
| [#1 — Add custom text for startup contents](https://github.com/pendejousplus/git-work/issues/1) | Cerrada | El PR #3 personalizó el texto de la portada y se fusionó en `main`. |
| [#2 — Add custom text for startup contents](https://github.com/pendejousplus/git-work/issues/2) | Cerrada como duplicada | Repite la solicitud de personalizar la portada de la issue #1. |
| [#4 — Improve UX with cool colors](https://github.com/pendejousplus/git-work/issues/4) | Cerrada | El commit [8de0df5](https://github.com/pendejousplus/git-work/commit/8de0df593620da758b31d410b730e2bc42cfe153) añade la sombra al botón y contiene `Closes #4`. |

### Pull requests

| Pull request | Estado | Trabajo realizado |
| --- | --- | --- |
| [#3 — Personalizar portada de startup](https://github.com/pendejousplus/git-work/pull/3) | Fusionado en `main` | Integra la rama `custom-text` y atiende la personalización solicitada en la issue #1. La conversación incluye un comentario de revisión sobre el pie y el eslogan. |
| [#5 — Cambiar color de botón principal a verde oscuro](https://github.com/pendejousplus/git-work/pull/5) | Cerrado, no fusionado en GitHub | Propone `darkgreen` para la issue #4. El cambio se integró localmente al resolver el conflicto en favor de ese color y aparece en el commit [4e20e10](https://github.com/pendejousplus/git-work/commit/4e20e102d3fed77f10d6441a250af280f8f2086d). |

La resolución del conflicto del PR #5 se hizo localmente, no mediante el botón
de fusión de GitHub. Por eso el PR figura cerrado, pero no como fusionado en la
plataforma. El cambio resultante sí está en `main`.

## Comprobaciones

Ejecuta estos comandos desde la raíz del repositorio y guarda sus salidas reales
en `comprobaciones.txt`, como pide la práctica:

```bash
git log --oneline --graph --all
git status
git remote -v
git tag
git log --format='%an <%ae>' | sort -u
gh pr list --state all
gh issue list --state all
gh release list
```

## Problemas y soluciones

| Problema | Comprobación o solución |
| --- | --- |
| La página no carga los estilos | Abre `index.html` desde la raíz del repositorio y comprueba que existe `css/cover.css` en esa ruta. |
| El workflow de documentación falla | Revisa el detalle de la ejecución en Actions y ejecuta `mkdocs build --strict` localmente para reproducir el error. |
| Aparece un conflicto en `css/cover.css` | Consulta `git status`, resuelve las marcas de conflicto conservando el cambio acordado, ejecuta `git add css/cover.css` y confirma la resolución. |
| Una issue no se cierra automáticamente | Comprueba que el commit o la descripción del PR incluye una referencia válida, como `Closes #4`, y que llega a la rama principal. |

## Repositorio y publicación

- Repositorio principal: <https://github.com/pendejousplus/git-work>
- Repositorio espejo: <https://github.com/pendejousplus/git-work-espejo>
- Sitio publicado en GitHub Pages: <https://pendejousplus.github.io/git-work/>
- Release `0.1.0`: <https://github.com/pendejousplus/git-work/releases/tag/0.1.0>