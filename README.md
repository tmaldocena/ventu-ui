# VentuUI

Sistema de diseño de Ventu. Este repositorio reúne los design tokens (colores, tipografía y sombras) como variables CSS, tomados de las variables de Figma.

> Tema disponible: **Light**. El modo oscuro todavía no está definido.

## Contenido

| Archivo | Qué es |
| --- | --- |
| `ventu-tokens.css` | Variables en `:root` y las clases de texto `.text-*` |

## Empezar

### 1. Cargá las fuentes

El archivo declara las familias pero no las descarga. Nunito se usa en la interfaz y JetBrains Mono en datos como distancias, horarios y precios.

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500&family=Nunito:wght@400;500;600&display=swap">
```

### 2. Incluí los tokens

Cargá `ventu-tokens.css` antes del resto de tus estilos.

```html
<link rel="stylesheet" href="ventu-tokens.css">
```

### 3. Usá variables, no valores

```css
.tarjeta {
  background: var(--color-container-lowest);
  color: var(--color-on-surface);
  border-bottom: 1px solid var(--color-outline);
  box-shadow: var(--shadow-card);
}
```

Para el texto, aplicá una de las clases `.text-*`. Cada una define familia, peso, tamaño, interlineado y espaciado de letras.

```html
<h2 class="text-headline-md">Taller de cerámica</h2>
<p class="text-body-md">Piezas hechas a mano.</p>
<span class="text-label-mono">350 m · 09:00–18:00</span>
```

## Colores

Hay 47 tokens de color en siete grupos, derivados de cinco colores base.

| Color base | Hex | Rol |
| --- | --- | --- |
| Marino | `#0f2742` | `secondary` |
| Celeste | `#5b87a6` | `tertiary` |
| Terracota | `#c26745` | `primary` |
| Gris | `#dad7d0` | `outline` |
| Crema | `#f7f2ea` | `surface` y `background` |

| Grupo | Tokens | Uso |
| --- | --- | --- |
| `surface` | 14 | Fondos de pantallas y contenedores, y el texto que va encima |
| `primary` | 9 | Terracota. Acciones principales, links y estados activos |
| `secondary` | 8 | Azul marino. Acciones secundarias, navegación y texto de peso |
| `tertiary` | 8 | Celeste. Acento para información y detalles de apoyo |
| `error` | 4 | Errores y acciones destructivas |
| `outline` | 2 | Bordes y divisores |
| `background` | 2 | Fondo general y su texto |

Todos siguen el patrón `--color-<nombre>`, por ejemplo `--color-primary` o `--color-on-surface-variant`.

### Cómo leer los nombres

| Nombre | Significado |
| --- | --- |
| `primary` | El color del rol, para fondos de acciones y elementos principales |
| `on-primary` | Texto e íconos que van encima del color del rol |
| `primary-container` | Versión suave para chips, banners y botones tonales |
| `on-primary-container` | Texto e íconos sobre el container |
| `primary-fixed`, `primary-fixed-dim` | Valores pensados para no cambiar entre temas |
| `on-primary-fixed`, `on-primary-fixed-variant` | Texto sobre los valores fixed |
| `inverse-*` | Superficies invertidas, como snackbars |

La escala `container-lowest`, `container-low`, `container`, `container-high` y `container-highest` marca la jerarquía de superficies. Cuanto más alto el nivel, más oscuro el fondo.

## Tipografía

| Clase | Fuente | Tamaño | Interlineado | Espaciado |
| --- | --- | --- | --- | --- |
| `.text-display-lg` | Nunito SemiBold | 44px | 115% | −2% |
| `.text-display-md` | Nunito Medium | 32px | 120% | −1.5% |
| `.text-display-sm` | Nunito Regular | 24px | 125% | −1% |
| `.text-headline-lg` | Nunito SemiBold | 28px | 125% | −1% |
| `.text-headline-md` | Nunito Medium | 22px | 130% | 0% |
| `.text-headline-sm` | Nunito Regular | 18px | 135% | 0% |
| `.text-body-lg` | Nunito Regular | 17px | 160% | 0.5% |
| `.text-body-md` | Nunito Regular | 15px | 155% | 1% |
| `.text-body-sm` | Nunito Regular | 13px | 150% | 1.5% |
| `.text-label-lg` | Nunito SemiBold | 15px | 130% | 2% |
| `.text-label-md` | Nunito Medium | 13px | 130% | 3% |
| `.text-label-sm` | Nunito Medium | 11px | 130% | 4% |
| `.text-label-mono` | JetBrains Mono Medium | 12px | 130% | 4% |
| `.text-body-mono` | JetBrains Mono Regular | 13px | 150% | 2% |

Las escalas base también están disponibles como variables: `--font-size-0` a `--font-size-10`, `--line-height-0` a `--line-height-13`, `--letter-spacing-0` a `--letter-spacing-9` y `--font-weight-*`.

## Sombras

| Token | Uso |
| --- | --- |
| `--shadow-card` | Cards y fichas |
| `--shadow-flyout` | Modales y diálogos |

## Conversión desde Figma

Los valores del JSON de Figma se convirtieron así:

| En Figma | En CSS |
| --- | --- |
| Tamaño de fuente en px | `rem`, con base de 16px |
| Interlineado en % | Valor sin unidad (115% pasa a `1.15`) |
| Letter-spacing en % | `em` (−2% pasa a `-0.02em`) |
| SemiBold, Medium, Regular | 600, 500, 400 |
| Sombras | Valores de `box-shadow` |

## Accesibilidad

Los contrastes se calcularon con la fórmula de WCAG 2.1. Todos los pares `on-*` superan 4.5:1 salvo estos casos:

| Combinación | Contraste | Qué hacer |
| --- | --- | --- |
| `primary` con `on-primary` | 3.95:1 | Usarlo solo en texto grande (desde 24px, o 18.7px en negrita) |
| `tertiary` con `on-tertiary` | 3.85:1 | Igual que el anterior |
| `background` con `outline` | 1.29:1 | Usar `outline` solo en divisores. Para bordes de campos y controles usar `on-surface-variant` |

Para texto chico sobre un acento, combiná `primary-container` con `on-primary-container`.

## Tailwind

Los prefijos `--color-*`, `--shadow-*` y `--font-*` coinciden con los que Tailwind v4 lee dentro de `@theme`. Moviendo las variables ahí deberías obtener clases como `bg-primary` o `text-on-primary` sin renombrar nada. Probalo en el proyecto antes de dar el cambio por hecho.

```css
@import "tailwindcss";

@theme {
  --color-primary: #c26745;
  --color-on-primary: #ffffff;
  --color-secondary: #0f2742;
  /* resto de las variables de ventu-tokens.css */
}
```

## Actualizar los tokens

Los tokens se mantienen en Figma. Cuando cambien, exportá las variables como JSON y actualizá `ventu-tokens.css` aplicando las reglas de la sección de conversión.

## Limitaciones conocidas

- Solo existe el tema Light.
- No hay tokens de espaciado ni de radios. Los componentes de ejemplo usan valores fijos.
