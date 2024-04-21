---
Created: 2024-01-22
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Circuiti sequenziali]]"
Completed: true
---
>[!def] Definizione
 L'obbiettivo del [[Gated Latch]]  è quello di poter alterare la memoria soltanto quando il clock è 1, ma nonostante questo possono avvenire comunque variazione indesiderate degli input anche nel breve tempo in cui il clock è uno.
>
>Per risolvere questo problema sono stati inventati i flip flop, [[Circuiti sequenziali|circuiti sequenziali]] [[Circuiti Sincroni ed Asincroni#Circuiti Sincroni|sincroni]] capaci di memorizzare bit come i latch ma che si abilitano soltanto ai fronti d'onda, per questo di chiamano **edge triggered**.
>
>
>Tutti i flip flop sono **edge triggered** ovvero sono sensibile ai fronti d'onda del clock.
>- Positive edge triggered --> FF sensibile al fonte di salita
>- Negative edge triggered --> FF sensibile al fronte di discesa
>
>![[Pasted image 20240205175743.png|500]]

>[!Note] Indice
>- [[Flip Flop SR (master slave)]] 🟢
>- [[Flip Flop JK]] 🟢
>- [[Flip FLop Toggle]] 🟢
>- [[Flip Flop Delay]]
>
>- [[Flip Flop pre-set clear]]
