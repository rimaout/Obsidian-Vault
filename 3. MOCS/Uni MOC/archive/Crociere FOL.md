---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-23T14:06
updated: 2025-04-23T16:39
---
$D = \{  \}$

$F = \{ \text{nome/1} \}$
- `nome(i)` funziona che associa elemento del dominio il suo nome

$P = \{ \text{irociera/1, itinerario/1, segue/2} \}$
- `crociera(x)`è *true* se `x` è una crociera
- `itinerario(x)` è *true* se `x` è un itinerario
- `destinazione(x)` è *true* se `x` è una destinazione
- `segue(x,y)` è *true* se `x` (crociera) segue `y` (itinerario)
- `tocca(x,y)` è *true* se `x` (crociera) tocca `y` (destinazione)
- `lunamiele(x)` è *true* se `x` (crociera) è di tipo luna di miele
- `perfamiglie(x)` è *true* se `x` (crociera) è di tipo per famiglie

>[!note] Esercizio 2
>
>Ogni crociera segue esattamente un itinerario:
>
>$$
>\forall c\ \text{crociera} (c) \implies \big( \exists i_{1} \ \text{itinerario}(i_{1})\ \wedge \ \text{segue}(c,i_{1}) \wedge \not \exists i_{2}\ \text{itinerario}(i_{2}) \wedge (i_{1} \not =i_{2}) \wedge  \text{segue}(c,i_{2})\big)
>$$

>[!note] Esercizio 3
>
>Gli itinerari hanno un nome univoco (non esistono due o più itinerari cono lo stesso nome)
>
>$$
>\forall i_{1}, i_{2}\ \Big(\text{itinerario}(i_{1}) \wedge \text{tinerario}(i_{2}) \wedge  (i_{1} \not = i_{2}) \implies \text{nome}(i_{1}) \not= \text{nome}(i_{2}) \Big)
>$$

>[!note] Esercizio 4
>
>Ogni crociera tocca un certo insieme non vuoto di destinazioni.
>
>$$
\forall c\ \text{crociera}(c) \implies \exists d \ \text{destinazione}(d) \wedge \text{tocca}(c,d)
>$$

>[!note] Esercizio 5
>
>Le crociere si dividono in crociere di luna di miele e crociere per famiglia.
>
>$$
>\forall c\ \ \text{crociera(c)} \implies \big(\text{lunamiale}(c) \vee \text{perfamiglie}(c) \big) \wedge \neg \big(\text{lunamiale}(c) \wedge  \text{perfamiglie}(c) \big)
>$$
