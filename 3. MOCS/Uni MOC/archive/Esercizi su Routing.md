---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-29T15:24
updated: 2025-04-29T16:13
---
>[!note] Esercizio 1
>
>

>[!note] Esercizio 1
>
>Ognuno dei seguenti indirizzi appartiene a un blocco. Trovare il primo e l'ultimo indirizzo di ogni blocco:
>- `14.12.72.8/24`
>- `200.107.16.17/18`
>- `70.110.19.17/16`
>
>Ogni indirizzo è composto da 4 blocchi da 8 bit, questi 32 bit sono utilizzati per rappresentare due informazioni:
>- indirizzo di rete 
>- indirizzo dell'host
>
>***oss:*** l'indirizzo di rete rimane invariato per tutti gli host all'interno di quella rete
>
>Per determinare quali bit della indirizzo rappresentano l'indirizzo di rete e quali rappresentano l'indirizzo dell'host è utilizzata la netmask, ovvero un numero che rappresenta quanti dei bit iniziali sono dedicati alla rete e poi di conseguenza tutti gli altri sono dedicati all'host.
>
>Nel caso di `14.12.72.8/24` abbiamo che la netmask è 24 quindi i primi 3 byte (24 bit) sono per la rete ed il restante 1 byte (8 bit) è dedicato all'indirizzo del host.
>
>Quindi l'indirizzo di rete è `14.12.72` e non cambia per tutti gli host di quella rete, invece gli indirizzi di host vanno da: `14.12.72.0` a `14.12.72.255`.
>
>Questo caso è stato particolarmente semplice perché la netmask era un multiplo di 8. Ora vediamo con `200.107.16.17/18` la netmask è 18 questo vuol dire che i primi 2 byte e i seguenti i 2 bit rappresentano l'indirizzo di rete ed i restanti 14 bit rappresentano l'indirizzo dell'host.
>
>Quindi 
>- `200.107` (16 bit) fa parte della indirizzo di rete
>- gli otto bit `16` in binario sono `00010000` di questi i primi 2 (`00`) fanno parte del indirizzo del server e i restanti 6 (`010000`) fanno parte del indirizzo del host.
>  
>Per questo gli indirizzi disponibili agli host nella rete vanno da `200.107.00.00` a `200.107.63.255`
>
>il terzo byte va da `0` a `63` perché, in realtà, i primi due bit sono utilizzato dall'indirizzo di rete e per questo non possono variare quindi abbiamo soltanto 6 bit che possono rappresentare numeri da `0` a `63`.

>[!note] Esercizio 1
>
>

>[!note] Esercizio 1
>
>

>[!note] Esercizio 1
>
>

>[!note] Esercizio 1
>
>