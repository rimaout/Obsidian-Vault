---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-12T19:07
updated: 2025-04-13T16:09
---
## Esercizio 1

**Domanda:** Si vuole aggiungere un nuovo protocollo nel livello applicazione: quali modifiche è necessario apportare agli altri livelli?

**Risposta:** Non dobbiamo apportare modifiche ad altri liveli perche il livello di applicazione non offere servizi ad altri livelli.

## Esercizio 2

**Domanda:** Quando si dice che il livello di trasporto effettua il multiplexing e il demultiplexing dei messaggi a livello applicazione, si intende che il protocollo di livello applicazione può combinare più messaggi del livello applicazione in un pacchetto?

**Risposta mia:** No, il multiplexing si occupa di effettuare l'incapsulamento ovvero di creare un pacchetto aggiungendo al messaggio del livello applicazione il giusto header. Il demultiplexing si occupa di effettuare il decapsulamento dei pacchetti ricevuti.

**Risposta prof:** No, significa che il livello di trasporto può incapsulare (uno alla volta) i
pacchetti provenienti dal livello superiore includendo delle
informazione nell’intestazione che poi consentono di effettuare
correttamente il demultiplexing

## Esercizio 3

**Domanda:** Spiegare il motivo per cui, nel contesto del paradigma client/server, il server
debba essere permanentemente in esecuzione mentre il client possa essere
eseguito solo quando necessario

**Risposta:** Il server deve essere sempre pronto a ricevere richieste dai client che
possono arrivare in qualsiasi momento. Il client invece deve essere attivo solo
mentre l’utente vuole usare l’applicazione.

## Esercizio 4

**Domanda:** Un client FTP deve prelevare due file dal server e depositarvi un altro file: quante connessioni di controllo e quante connessioni di trasferimento dati sono necessarie?

**Risposta:** 
- 1 connessione di controllo (per l'associazione del client sever)
- 3 concessioni di trasferimento (1 per ogni file)

## Esercizio 5

**Domanda:** È possibile per un server FTP ottenere l’elenco dei file o directory dal client?

**Risposta:** No, il serve non può inviare richieste al client, può solo rispondere alle richieste dei client


## Esercizio 6

**Domanda:** Quali tipi di resource record sono memorizzati in un server DNS radice? Dare un esempio.

**Risposta:** NS, A
- `[NS, edu, a.edu.servers.net.]`
- `[A, a.edu.servers.net., 192.5.6.30]`

## Esercizio 7

**Introduzione:** Un file contiene 2 milioni di byte.

**Domanda 1:** Quanto si impiega a trasmettere il file usando un canale a 56 kbps?

$$
\begin{align*}
&-\ \text{Rate} = 56 \cdot 10^{3} \text{ bps}\\
&-\ \text{D} = 2 \cdot 10^{6} \text{ byte} = 2 \cdot  8 \cdot 10^{6} \text{ bit} = 16 \cdot  10^{6} \text{ bit }\\
\end{align*}
$$

$$
\text{tempo} = \frac{\text{D}}{\text{Rate}} = \frac{16 \cdot  10^{6} \text{ bit}}{56 \cdot  10^{3} \text{ bps}} = \frac{16 \cdot 10^{3}}{56} \text{ s} \approx 285 \text{ s}
$$

**Domanda 2:** E usando un canale a 1Mbps?
 
$$
\begin{align*}
&-\ \text{Rate} = 10^{6} \text{ bps}\\
&-\ \text{D} = 2 \cdot 10^{6} \text{ byte} = 2 \cdot  8 \cdot 10^{6} \text{ bit} = 16 \cdot  10^{6} \text{ bit }\\
\end{align*}
$$

$$
\text{Tempo} = \frac{\text{D}}{\text{Rate}} = \frac{16 \cdot  10^{6} \text{ bit}}{10^{6} \text{ bps}} = 16\text{ s}
$$

## Esercizio 8

Si consideri un Host A che vuole inviare un file molto grande a un Host B. Il percorso tra A e B ha 3 link, con rate $R_{1} = 500 \text{ kbps}$, R2=2Mbps R3=1Mbps.


**Domanda 1:** Assumendo l’assenza di ulteriore traffico nella rete, qual è il throughput per il file transfer?

- $\text{Throughput} = 500 \text{ kbps}$

**Domanda 2:** Si supponga che il file sia grande 4 milioni di byte. Dividendo la grandezza del file per il throughput, quanto impiegherebbe all’incirca trasferire il file all’host B?

- $\text{Rate} = 500\text{ kbps} = 5\cdot 10^{5} \text{ kbps}$
- $D = 4 \cdot 10^{6} \text{ byte} = 4\cdot 8 \cdot 10^{6} \text{ byte} = 32 \cdot 10^{6} \text{ bit}$

$$
\text{Tempo} = \frac{D}{\text{Rate}} = \frac{32 \cdot 10^{6} \text{ bit}}{5\cdot 10^{5} \text{ kbps}} = \frac{32 \cdot  10}{5} \text{ s} = 64 \text{ s}$$

**Domanda 3:** Ripetere le domande 1) e 2) con $R_{2} = 100 \text{ kbps}$

- $\text{Throughput} = 100 \text{ kbps}$
- $\text{Rate} = 100 \text{kbps} = 1 \cdot 10^{5} \text{ bps}$
- $D = 4 \cdot 10^{6} \text{ byte} = 4\cdot 8 \cdot 10^{6} \text{ byte} = 32 \cdot 10^{6} \text{ bit}$

$$
\text{Tempo} = \frac{D}{\text{Rate}} = \frac{32 \cdot 10^{6} \text{ bit}}{1\cdot 10^{5} \text{ kbps}} = {32 \cdot  10} \text{ s} = 320 \text{ s}
$$

## Esercizio 9

![[Pasted image 20250413131604.png]]

- **Riposta 1:** $30 \text{ Mbps}$
- **Riposta 2:** $R_{S}$
- **Risposta 3:** $100\%$
- **Riposta 4:** $\frac{30}{40} = 75\%$ 
- **Risposta 5:** $30 \cdot (300/4) = 40 \%$

## Esercizio 10

**Domanda:*** Si vuole inviare un file di 160000 bits dall’host A all’host B su una rete a
commutazione di circuito. I link hanno rate pari a 1536 kbps e usano il TDM
con 48 slot/sec. Il tempo per stabilire il circuito tra A e B è 500 ms.

Dati:
- $D = 160000 \text{ bit} = 16 \cdot 10^{4} \text{ bit}$
- $\text{Rate} = 1536 \text{ kbps} = 1536 \cdot 10^{3} \text{ bps}$

Informazioni:
- Rete a commutazione di circuiti con link TDM che a disposizione uno slot di 48 al secondo, questo significa che può tramestare per $\frac{1}{48}$ si secondo alla volta.
- Inoltre inizialmente stabilire il circuito tra l'host `A` e `B` richiede `500ms` ovvero `0.5s`.

$$
\text{Tempo Trasmissione} = \frac{{16 \cdot 10^{4} \text{ bit}}}{{1536 \cdot   10^{3}\text{ bps}} \cdot  \frac{1}{48}}= \frac{160}{1536} \text{ s} \cdot 48 = 5 \text{ s}
$$

$$
\text{Tempo Totale} = 5 + 0.5 = 5.5 \text{ s}
$$
## Esercizio 11

```
GET /kurose_ross_sandbox/interactive/quotation7.htm HTTP/1.1
Host: gaia.cs.umass.edu
Accept: text/plain, text/html, image/png, image/gif, audio/mp4, audio/mpeg, video/mp4, video/wmv,
Accept-Language: en-us, en-gb;q=0.8, en;q=0.2, fr, fr-ch, da, fi, ar, cs
If-Modified-Since: Wed, 10 Apr 2024 01:14:34 -0700
User Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko)
Chrome/17.0.963.56 Safari/535.11
```

**Domanda 1:** A quale protocollo appartiene?
- `HTTP/1.1`

**Domanda 2:** Che tipo di messaggio è?
- è una richiesta GET fatta la server `gaia.cs.umass.edu`.

**Domanda 3:** Qual è il file richiesto?
- `quotation7.html` con percorso `/kurose_ross_sandbox/interactive/quotation7.html`.

**Domanda 4:** Il client accetta immagini Jpeg?
- no, nella capo `Accept` non è presente `image/jpeg`.

**Domanda 5:** Il client ha già una copia del file in cache?
- si perché nella richiesta è presente il campo `If-Modified-Since: Wed, 10 Apr 2024 01:14:34` che indica che il file è già presente nella cache e che l'ultima volta che è stato aggiornato è Apr 2024 alle 01:14:34.

## Esercizio 12

![[Pasted image 20250413160218.png|700]]


**Domanda 1:** Quando viene usata la commutazione di circuito qual è il massimo numero di utenti che possono essere supportati?

- Per assicurare ad ogni utente un rate di `25 Mbps` il circuiti può avere al massimo 4 utenti.
  
**Domanda 2:** In caso di commutazione di pacchetto, qual è la probabilità che uno specifico utente stia trasmettendo e gli altri no?

$$
0.3 \cdot  (0.7)^{nps-1}
$$

**Domanda 3:** In caso di commutazione di pacchetto, qual è la probabilità che un utente (qualsiasi) stia trasmettendo e gli altri no?

![[Pasted image 20250413160940.png]]
