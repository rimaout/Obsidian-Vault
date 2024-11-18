---
created: 2024-01-20
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[HDL (hardware description language)]]"
completed: true
updated: 2024-11-18T20:21
---

>[!abstract] Related
>- [[Progettazione Sistemi Digitali (class)]]

>[!abstract] Index
>1. [[#Obbiettivi HDL]]
>2. [[#Definizione Modulo]]
>3. [[#Sintassi Modulo]]
>4. [[#Variabili logiche]]
>5. [[#Bus multipli]]
>6. [[#Numeri in verilog]]
>7. [[#Operatori]]
>	- [[#Operatori Logici]]
>	- [[#Operatori assegnazione continua]]
>	- [[#Operatore condizionale]]
>	- [[#Operatore always]]
>	- [[#Operatore case]]
>8. [[#Modellazione Strutturale]]

---
## Obbiettivi HDL 

2 principali obbiettivi:
- **Simulazione:**  si forniscono gli input e controllando gli output si osserva se il modulo si comporta correttamente 
- **Sintesi:** La descrizione del modulo viene tradotta in un circuito

>[!warning] oss
> *HDL* = hardware description language 

---
##  Definizione Modulo

Esistono due "stili" per descrivere un modulo:
- *Comportamentale:* descrive cosa fa un modulo (utilizzando espressioni booleane e controlli condizionali)
- *Strutturale:* descrive com il circuito interno di un modulo, suddividendolo in moduli più piccoli.

>[!warning] oss 
>Noi descriveremo i moduli in modo *comportamentale* 

---
## Sintassi Modulo

``` verilog
module name(input logic datatype variables...
						 ...
			output logic datatype variables...
						 ...
			);
	
	logic datatype variables ...;
	
	assign y = operazione;
	
endmodule
```

- `module` inizializza il modulo
- `name` è il nome che diamo al modulo
- dopo `input logic` scriviamo gli input
	- Data type 2 opzioni:
		1. Variabile booleana (default, non scrivere niente)
		2. Bus di bit (scrivere \[start:end] dove start ed end indicano la grandezza del bus )
	- gli input scritti sulla stessa "linea" sono dello stesso datatype
	- se abbiamo più input di tipo diverso scriverli su `input logic` diversi
- dopo `output logic` scriviamo gli output
	- Stessa cosa degli input
- `assign` è usato per assegnare a una variabile un valore o un risultato di un operazione

---
## Variabili logiche

Esistono 3 modi diversi per definire delle variabili:
- *Input Logic :* Variabili in ingresso (input del modulo)
- *Output Logic :* variabili in uscita (output del modulo)
- *Logic:* variabili interne

Esistono 2 tipi di variabili logiche:
- *Variabili booleane:* variabile che può assumere vero (1) o falso (0)
- *Bus:* più variabili booleane racchiuse in una sola variabile

**Come definire variabili:**
```verilog
logic a, b; // a e b sono variabilie booleane
logic [0:3] c, d; // c e d sono bus a 4 canali

```

>[!warning] oss
>Sostituendo `logic` con `logic input` o `logic output` si definiscono rispettivamente gli input e gli output logici

---
## Bus multipli
Un bus è una serie di variabili booleane contenuta in una sola variabile

**Definizione base:**
1. `[0:3] a` -> bus a 4 bit (dal meno significativo`a[0]`al più significativo`a[3]`)
2. `[4:1] a` -> bus a 4 bit  (dal più significativo`a[4]`al meno significativo`a[1]`)

*oss:* `[0:2] a` --> `a[0], a[1], a[2]`

**Bus concatenati**
```verilog
module esempio (logic input a, b,
                logic output [0:1] y);
      
      logic c;
      
      assign c = a & b;         
      assign y = {c, b}; // y[0] = c, y[1] = b

endmodule
```

1. `b = {a[0], a[1]}` -> bus a 2 bit (`b[0] = a[0]` e `b[1] = a[1]`)
2. `c = {3{a[0]}}` -> bus a 3 bit (copia di `a[0]`x 3 volte) 
3. `d = {3'b110}` -> bus a 3 bit (`d[0] = 1`, `d[1] = 1`, `d[2] = 0`)

*oss:* leggi [[#Numeri in verilog]] per capire meglio caso 4

**Notazione particolare (tipo slicing python):**
- È  possibile selezionare alcuni canali di un bus con questa sintassi

```verilog
module esempio(logic input [0:5] d           //bus 6bit dal meno al più significativo
			   logic output [0:2] x, y, x;). // bus 3 bit

assign x = d[0:2];   // x = {d[0], d[1], d[2]}
assign y = d[2:0];   // x = {d[2], d[1], d[0]}
assign z = d[1:3];   // x = {d[1], d[2], d[3]}

```

**Esempi generali bus:**

>[!warning] Esempio 1
>```verilog
> module and4_1(input logic [0:3] a, output logic y);
>
>    assign y = &a;
>    assign y = a[0] & a[1] & a[2] & a[3];
>    // fanno stessa cosa
>
>endmodule
>```
>

>[!warning] Esempio 2
>
>```verilog
>module and4_1(input logic a0, a1, a2, a3, output logic y);
>
>    assign y = a0 & a1 & a2 & a3;
>
>endmodule
>```

>[!warning] Oss:
>Esempio 1 ed Esempio 2 fanno stessa cosa

---
## Numeri in verilog

![[JPEG image-4096-8811-2D-0.jpeg|400]]

---
## Operatori
### Operatori  Logici
``` verilog
module all_logic(input logic a, b, 
			output logic NOT, AND, OR, XOR, NAND, NOR);

	assign NOT = ~a;         // NOT
	assign AND = a & b;      // AND
	assign OR = a | b;       // OR
	assign XOR = a ^ b;      // XOR
	assign NAND = ~(a & b);  // NAND
	assign NOR = ~(a | b);   // NOR
	
endmodule
```

**Operatori Bitwise:**
Questi sono operatori logici *Bitwise*, ovvero operatori che lavorano su singolo bit o su bus multipli

>[!warning] Esempi:
>*Esempio 1:*
>```verilog
>module not_bus(input logic [0:3] a, output logic [0:3] y);
> 
>    assign y = ~a;
 >    assign y = {~a[0], ~a[1], ~a[2], ~a[3]};
>    // fanno stessa cosa
>
>endmodule
>```
>
>*Esempio 2:*
>```verilog
>module and_bus(input logic [0:3] a, output logic y);
> 
>    assign y = &a;
>    assign y = a[0] & a[1] & a[2] & a[3];
>    // fanno stessa cosa
>
>endmodule
>```
>
>*Esempio 3:*
>```verilog
>module and4_1(input logic a0, a1, a2, a3, output logic y);
>
>    assign y = a0 & a1 & a2 & a3;
>
>endmodule
>```
>
>
>>[!danger] Oss:
>>Esempio 2 e 3 fanno la stessa cosa
>

---
### Operatori assegnazione continua
- *Assign* o operatore di assegnazione continua, assegna a una variabile un valore.
- Viene utilizzato per la realizzazioni di reti combinatorie

*Assegnare a una variabile true o false:*
- `assign y = 1'b1;` --> assegno a y un bit di binario di valore 1
- `assign y = 1'b0;` --> assegno a y un bit di binario di valore 0

*Assegnare a una variabile attraverso un operazione altre variabili:*
- `assign y = a | b;`

*Assegnazione tra bus:*
- `assign` `{x, y, z} = ~{a, b, c};` --> Significato: x = ~a,  y = ~b,  x = ~c

```verilog
assign {x, y, z} = ~{a, b, c};

assign x = ~a;
assign y = ~b;
assign z = ~c;

// fanno stessa cosa
```

>[!warning] Oss:
>Ogni volta che cambia a o b il valore di y viene ricalcolato 

---
#### Assign con ritardo

**Sintassi:**
```verilog
'timescale ritardo/precisione

module name(input ..., output ... );
	logic ... ;
	
    assign #1 ... ;
    assign #2 ... ;
	 ...
	assign #n ... ;

endmodule
```
- *Ritardo* indica l'unita di tempo del ritardi
	- esempio: 1ns (1 nano second), 10ms (10 millisecondi) ecc.
- *Precisione* indica il possibile errore
	- infatti per simulare circuiti reali serve prendere in considerazione anche possibili errori
- `assign #n` indica dopo quante unita di mistura eseguire l'assegnazione
	- esempio: `ritardo = 1ns` e allora `assign #1` verra effettuato dopo `1ns` e `assign #2` dopo `2ns`

**Esempio:**
```verilog
'timescale 1ns/1ps

module esempio(input a, b, c, output x, y);
	logic ab, ac, bc;
	
	assign #1 x = a | b | c;    //ritardo 1ns + 1ps
    assign #2 ab = a & b;       //ritardo 2ns + 1ps
    assign #2 ac = a & c;       //ritardo 2ns + 1ps
	assign #2 bc = b & c;       //ritardo 2ns + 1ps
	assign #4 y = ab | ac | bc; //ritardo 4ns + 1ps

endmodule
```

---
### Operatore condizionale
- Selezione in base a una condizione la prima o la seconda espressione

**Sintassi:**

```verilog
assign y = c? s1 : s2; // y = s1
// c = condizione
// s1 = espressione 1 
// s2 = espressione 2
```

$$
y = \begin{cases}
y=\text{s1} & \text{if }c=1 \\
y=\text{s2} & \text{if }c=0
\end{cases}
$$
**Esempio:**
```verilog
logic c;
assign c = a & b; //c = 1
assign y = c? s1 : s2; // y = s1

assign a = 1'b0; // a = 0
assign c = a & b; //c = 0
assign y = c? s1 : s2; // y = s2
```

---
### Operatore always
- Istruzione viene eseguita quando è rispettata una condizione
- Viene utilizzate 

**Sintassi:**
```verilog
always@(sensitivity list)
    istruzione
```
- *always@* va sostituito con:
	- `always_ff@`  (per [[Flip Flop]])
	- `always_latch@` (per [[Latch]])
	- `always_comb@`
	
- *sensitivity* va sostituita con:
	- `posedge` (sensibile al fronte di salita)
	- `negedge` (sensibile al fronte di discesa)
	
- *list* va sostituito con segale di ingresso, solitamente di usa:
	- `clk` (clock) 
	- `en` (enable) 

```verilog
always_ff@(sensitivity list)
always_latch@(sensitivity list)
always_comb@(sensitivity list)

always@(posedge clk) //sensibile al fornte di salita
```

**Bloccante e non bloccante:**
Esistono due tipi di always:
- *Non bloccante*  <=  (sequenziale, usato con always_ff e always_latch)
- *Bloccante*  =  (combinatoria, usato con always_comb) 

### Operatore case


---
## Modellazione Strutturale
- Utilizzo di uno p più moduli in un latro modulo

Dope aver definito un modulo con la sentassi
```verilog
module modulo1(input..., output ...);
	...
endmodule
```

È possibile riutilizzare il modulo in un altro modulo assegnatogli un nome univoco
```verilog
module modulo2 (input..., output ...);

	module modulo1( input_oputput ); 
	//in input_oputput iserire variabili che rispettino la definizione di modulo1 
	
endmodule
```

>[!example] Esempio: 
>`mux4:1` costruito utilizzando `mux2:1`
>1) Definire `mux2:1`
>2) Definire `mux4:1`
>
>```verilog
>module mux2_1(input logic d0, d1, s, 
>			output logic y);
>
>	assign y = s ? d1 : d0;
>	
>endmodule
>```
>
>
>```verilog
>module mux4_1(input logic d0, d1, d2, d3, s0, s1, // d bit dati, s bit selezione
>			output logic y);
>
>	logic basso, alto; //uscite dei mux (mux_alto, mux_basso)
>	mux2_1 muxalto(d0, d1, s0, basso);
>	mux2_1 muxbasso(d2, d3, s0, alto);
>	mux2_1 muxuscita(alto, basso, s1, y);
>
>endmodule
>```
> ![[Pasted image 20240130175305.png|400]]

>[!example] Esempio con bus: 
>`mux4:1` costruito utilizzando `mux2:1`
>
>```verilog
>module mux2(input logic [0:1] d,   // bus bit dati
>		    input logic s,         // bit selezione
>			output logic y);       // bit output
>
>	assign y = s ? d[1] : d[0];
>	
>endmodule
>```
>
>
>```verilog
>module mux4(input logic [0:3] d, 
> 			input logic [0:1] s,
>			output logic y);
>
>	logic basso, alto;
>	mux2 muxbalto(d[0:1], s[0], alto);
>	mux2 muxbasso(d[2:3], s[0], basso);
>	mux2 muxuscita({basso, alto}, s[1], y);
>
>endmodule
>```
> ![[Pasted image 20240130175415.png|400]]

---
**Esercizi:**
![[Pasted image 20240130175601.png|600]]

```verilog
module ffd(input logic D, clk, output logic Q, not_Q):
    
    always_ff@(posedge clk);
        begin
            Q <= D;
            not_Q <= ~D;
        end
endmodule
```

```verilog
module circuito(input logic A, clk, logic output [0:1] y);
    logic ponte;
    
    ffd ffd_sx(A, clk, y[0], ponte);
    ffd ffd_dx(ponte, clk, y[1]);

endmodule
```


**Shift register 8 bit con load e reset asincrono**

```Verilog
module mux2-1 (input logic x0, x1, s, output logic y);
     assign y = s ? x1 : x0
endmodule
```

```verilog
module ffd (logic input d, clk, reset, logic output y);

always@ff(posedege clk or posedge reset)
    
    if(reset) y <= 1b'0
    if else y <= d
	else q <= {y[6:0], si}
	
endmodule
```

```verilog
module registro (logic input [7:0] x, logic input load, reset, si,
				logic output  rso);

logic m7, m6, m5, m4, m3, m2, m1, m0; //output mux
logic o7, o6, o5, o4, o3, o2, o1, o0; //output fliplop

mux7(si,x[7],load, m7)
ff7(m7,clk, reset, o7)

mux6(o7,x[6],load, m6)
ff6(m7,clk, reset, o6)

mux5(o7,x[5],load, m5)
ff5(m7,clk, reset, o5)

mux4(rsi,x[4],load, m4)
ff4(m7,clk, reset, o4)

mux3(rsi,x[3],load, m3)
ff3(m3,clk, reset, o3)

mux2(rsi,x[2],load, m2)
ff2(m2,clk, reset, o2)

mux1(rsi,x[1],load, m1)
ff1(m1,clk, reset, o1)

mux0(rsi,x[0],load, m0)
ff0(m0,clk, reset, o0)


endmodule
```
