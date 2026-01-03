---
created: 2025-04-12T21:10
updated: 2025-09-23T19:30
related:
  - "[[My Quartz Setup Process]]"
  - "[[Quartz]]"
---
the image of some normal callouts and on the right, the grid layout version.

![[callouts_grid_layout.webp|1000]]

To do this we need to write some custom css code, this is the process:
- [[#Create column-callout.scss]]
- [[#Add custom style]]

## Create column-callout.scss

1. go in to `quartz/styles`
2. if doesn’t already exists crate a new directory naming it `custom`
3. enter in the new `custom` directory and create a file called `column-callout.scss`.
4. in side this file write this:

```css
@use "../base.scss";

/* Multi Column Callout */

/* Basic variables (in English) */
:root {
  --callout-min-width: 200px;
  --callout-gap: 1em;
}

/* Style for the multi-column callout */
.callout[data-callout="column"] {
  display: flex;
  flex-wrap: wrap;
  gap: var(--callout-gap);
  background: transparent;
  border: none;
  padding: 0;
}

/* Removes the Title */
.callout[data-callout="column"] > .callout-title {
  display: none;
}

/* Make the main callout content occupy full width */
.callout[data-callout="column"] > .callout-content {
  display: flex;
  flex-wrap: wrap;
  gap: var(--callout-gap);
  width: 100%;
}

/* Style for internal callouts */
.callout[data-callout="column"] > .callout-content > .callout {
  flex: 1 1 var(--callout-min-width);
  margin: 0;
}

/* Variation for fixed 2 columns */
.callout[data-callout="column"][data-callout-metadata*="col2"] > .callout-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

/* Variation for fixed 3 columns */
.callout[data-callout="column"][data-callout-metadata*="col3"] > .callout-content {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

/* Width options for sub-callouts */
div[data-callout="column"].callout > .callout-content > div[data-callout-metadata*="wide-2"] { 
  flex-grow: 2; 
}

div[data-callout="column"].callout > .callout-content > div[data-callout-metadata*="wide-3"] { 
  flex-grow: 3; 
}
```

This code automatically adjust the number of columns depending on the screen size, if we want to set the number of columns to a fixed number we can use the option `col2` or `col3` to have receptively 2 or 3 columns. se [[#How to add grid layouts]] section for more informations.

## Add custom style

Now we need to tell quartz to use this code we have written so:
1. go in to `quartz/styles`
2. open the `custom.scss` file
3. add at the begging of the file `@use "./custom/column-callout.scss";`

This for example is my `custom.scss`:

```css
@use "./base.scss";

/* Custom Modules */
@use "./custom/column-callout.scss";

...

```

## How to add grid layouts

This how to make the "basic version used in the image at the to of the page"

```md
>[!column]
>
>>[!note] First Year, First Semester
>>
>>- [[Progettazione Sistemi Digitali (class)|Progettazione di Sistemi Digitali]]
>>- [[Calcolo Differenziale (class)|Calcolo Differenziale]]
>>- [[Metodi matematici per l'informatica (class)|Metodi matematici per l'informatica]]
>>- [[Programmazione Calcolatori (Class)|Programmazione dei Calcolatori]]
>
>>[!note] First Year, Second Semester
>>
>>- [[Calcolo Integrale (class)|Calcolo Integrale]]
>>- [[Architettura (class)|Architettura dei Calcolatori]]
>>- [[Introduzione agli Algoritmi (class)|Introduzione agli Algoritmi]]
>>- [[Metodologie di Programmazione (class)|Metodologie di Programmazione]]
```

add immage

This is a variant that uses the option `col2`, in this case a line with 2 collums and a third with only one

```md
>[!column | col2]
>
>>[!note] First Year, First Semester
>>
>>- [[Progettazione Sistemi Digitali (class)|Progettazione di Sistemi Digitali]]
>>- [[Calcolo Differenziale (class)|Calcolo Differenziale]]
>>- [[Metodi matematici per l'informatica (class)|Metodi matematici per l'informatica]]
>>- [[Programmazione Calcolatori (Class)|Programmazione dei Calcolatori]]
>
>>[!note] First Year, Second Semester
>>
>>- [[Calcolo Integrale (class)|Calcolo Integrale]]
>>- [[Architettura (class)|Architettura dei Calcolatori]]
>>- [[Introduzione agli Algoritmi (class)|Introduzione agli Algoritmi]]
>>- [[Metodologie di Programmazione (class)|Metodologie di Programmazione]]
>  
>>[!note] First Year, Projects
>>
>>- [[BubbleBobble Game]]
>>- [[Python Homeworks]]

```

add immage