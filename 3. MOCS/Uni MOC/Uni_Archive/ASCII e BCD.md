---
created: 2023-10-06
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related: 
completed: true
updated: 2024-05-27T13:29
---
---
## Sistema ASCII

Il **codice standard** per i caratteri alfanumerici è il codice **ASCII** che utilizza 7 bit per codificare 128 caratteri. I bit sono divisi in **due parti**, una formata dai 3 bit più significativi che indicato la **tipologia del valore** e l'altra dagli altri 4 bit restanti che indicano la sua **rappresentazione**. Siccome tutti i calcolatori utilizzano 8 bit, che prendono il nome di **1 byte**, è stata creata un'estensione del codice ASCII a 8 bit aggiungendone uno nella posizione più significativa di valore 0. Questo bit viene utilizzato per scopi specifici, ad esempio nelle stampanti abilita la stampa di simboli addizionali.  

## Bit di parità 
Per individuare errori nelle comunicazioni è stato aggiunto un bit al codice ASCII allo scopo di rendere il numero totale di 1 presenti nel codice pari o dispari  

| ASCII       | Parità Pari | Parità Dispari | 
| ----------- | ----------- | -------------- | 
| A = 1000001 | 01000001    | 11000001       |  
| B = 1010100 | 11010100    | 01010100       |  

---
## Sistema BCD 8421

Il sistema numerico **binario** è quello più **naturale per un computer** mentre quello **decimale** il più **naturale per un essere umano**, per far combaciare queste esigenze noi convertiamo i numeri decimali in binario, eseguiamo i calcoli e poi riconvertiamo in decimale. Questo richiede però che i numeri vengano memorizzati in modo che possano essere convertiti in binario. Abbiamo bisogno quindi di **un metodo per rappresentare** le cifre **decimali** in 0 ed 1 e che **permetta di eseguire le operazioni senza eseguire conversioni**. Con 4 bit posso rappresentare un massimo di 16 valori, da 0 a 15, quindi un codice binario non ambiguo, che deve codificare 10 elementi con 4 bit, 6 delle possibili combinazioni rimarranno scoperte dando luogo a numerose **alternative di codifica** che appartengono alla classe dei codici binario decimale, indicata con **BCD**. Il più utilizzato è il  *BCD 8421*, in questo sistema rappresentiamo con 4 bit le cifre da 0 a 9, quindi un numero con n cifre decimali, in BCD, richiederà *n ∗ 4 bit*. Ad esempio il numero 396 sarà: 0011 1001 0110, *ogni 4 bit rappresentano una cifra decimale*. 

| Cifra Decimale | BCD |
| ---- | ---- |
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |

---