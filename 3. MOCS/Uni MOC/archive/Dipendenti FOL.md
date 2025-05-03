---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-29T10:33
updated: 2025-04-30T15:08
---
$D = \{  \}$ Dominio

$F = \{ \}$ Funzioni

$P = \{ \text{Persona/1, Telefono/1, Appartiene/2} \}$ Proposizioni
- `Persona(x)`: *true* se `x` è una persona
- `Telefono(x)`: *true* se `x` è un telefono
- `Nome(x)`: *true* se `x` è un nome
- `Dipendente(x)`: *true* se `x` è un dipendente
- `Dipartimento(x)`: *true* se `x` è un dipartimento
- `TelefonoAppartiene(a,b)`: *true* se `b` (telefono) appartiene a `a` (persona)
- `NomeAppartiene(a,b)`: *true* se `b` (nome) appartiene a `a` (persona)
- `Lavora(a,b)`: *true* se `b` (dipendente) lavora in `a` (dipartimento)
- `Dirige(a,b)`: *true* se `b` (persona) dirige `a` (dipartimento)

>[!note] Esercizio 1
>
>Tutte le persone hanno almeno un numero di telefono
>
>$$
>\forall x\ \text{Persona}(x) \implies \exists y\ \text{Telefono(y)} \wedge \text{TelefonoAppartiene(x,y)}
>$$

>[!note] Esercizio 2
>
>Ogni persona ha esattamente un nome
>
>$$
>\forall x\ \text{Persona}(x) \implies \exists y\ \text{Nome(y)} \wedge \text{NomeAppartiene(x,y)} \wedge \neg \big(\exists z\ \text{Nome(z)} \wedge (y \not = z) \wedge \text{NomeAppartiene}(x,z)\big)
>$$
>

>[!note] Esercizio 3
>
>Non ci sono dipendenti che lavorano in più di due dipartimenti
>

>[!note] Esercizio 4
>
>Ogni dipartimento ha esattamente un direttore che è una persona.
>
>$$
>\forall x\ \text{Dipartimento}(x) \implies \exists y \ \text{Persona}(y) \wedge \text{Dirigge}(x, y) \wedge \neg \big(\exists z \ \text{Persona}(y) \wedge  (z \not = y) \wedge \text{Dirigge}(x, z)\big)
>$$

## Soluzione Prof

scritta su nvim su DESK