---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-06-08T18:56
updated: 2026-01-31T13:32
---
## Introduzione

L'*IPv6* anche detto *IP New Generation* è nato con lo scopo di:
- aumentare lo spazio di indirizzi rispetto a [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding|IPv4]]
- ridisegnare il formato dei datagrammi
- rivedere protocolli ausiliari come [[Internet Control Message Protocol (ICMP)]]

I principali cambiamenti con [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding|IPv4]] sono:
- Indirizzi IP lunghi 128 bit
- Nuovo formato header IP
- Nuove opzioni
- Possibilità di estensione
- Opzioni di sicurezza
- Maggiore efficienza
	- No frammentazione nei nodi intermedi
	- Etichette di flusso per traffico audio/video

>[!note] Formato Datagramma
>
>![[Pasted image 20250608202518.png|900]]

## Adozione

Si pensava di migrare completamente all’IPv6 nel 2020, ma altre soluzioni come [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding#Nat|NAT]], [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding#DHCP|DHCP]] e [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding#Indirizzamento senza Classi|indirizzamento senza classi]] hanno tamponato la crescente richiesta di indirizzi IP rallentato il passaggio.

La transizione a IPv6 è però già iniziata, per permettere il funzionamento di IPv6 e IPv4 ci sono diverse tecniche.

## Dual Stack

Durante la transizione gli host devono avere un doppia pila di protocolli per la comunicazione in rete
- IPv4
- IPv6

Per determinare quale versione utilizzare l’host interroga il DNS e si usa il protocollo relativo all’indirizzo ritornato (se IPv4 o 6).

![[Pasted image 20250608204510.png|750]]

## Tunneling

Tecnica da utilizzare quando due host IPv6 che vogliono comunicare devono passare attraverso una regione IPv4.

Si incapsula il datagramma IPv6 nel payload di un datagramma IPv4, e si inseriscono come IP sorgente e destinazione gli estremi del tunnel.

![[Pasted image 20250608204636.png|1000]]

## Traduzione dell'intestazione

Un mittente IPv6 comunica con un destinatario IPv4, il datagramma viene tradotto prima di arrivare a destinazione:

![[Pasted image 20250608204726.png|800]]
