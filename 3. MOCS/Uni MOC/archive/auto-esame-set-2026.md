---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-10-01T13:45
updated: 2026-10-01T18:17
---
 

>[!note]- $\{ a^{n}b^{m}c^{k} : n,m,k \geq 0\text{ e }n-m+k \equiv 0(\text{mod} 3)\}$
>
>Stabilire se il linguaggio $L$ è regolare.
>
>![[Pasted image 20261001142029.png|400]]
>
>[Codice dell'autome](https://automatarium.tdib.xyz#/share/raw/H4sIAAAAAAAAA1XTv2_TQBQHcDsJ+QFt+QuQOjCSyhUlbdWpQnQFUUBiQs_nc3rI9oW7C8QSE2oFYqoYQEzkEjuFhgHR_4CuiUBsDAxsrEysvGtMa1uyZH9svXtf3_PLcUfwh5SoO3GHDre2N4cPmPfjsuOtLHt4NN3Vlt9ccRynue7TtSa4fqt1bX117aoDI6lAUfl2V_d6Op68HjDPOmByi0UQHCNOjnU8tS8h2__5C_LUvm98A72U98l3HV9ELOdrTO0FLP0cuVKscYScIleLfEXH314g14pFnuj4D2q98HJpXscWauNUx0pAJJliPJLvdhNf8NAaKF42yRJBwevPsIxYM7nyaCNWTKg8VhDrJlQeS4hVEymPVcQG4rk8mtVtk_IENZytVDIhC2qqmjj1glazrhozdc_aMqnOF7Sc9XWhoLUswtxMyUzrWbvzBW1kH2Yh0_eEhyGNlNz_IFl4m8puoPZTHBoln40ki9oB7acuKLLzZgAwBAAN_SG4JMWTkI8IrmuuzA2LcGcg2DZTZyUhVbCXRBDST5tdxUNY9GiwKLA0H3v4xnXsQFHvq2XZ_b93f88dGrzhsVP7+erXwWMqJG52urzkLDlHcFJHgWDd8F7+yYjwyGftvURlP8n4ZPRvCeqznn50yMXNDhWguNBPPwMhtKMgItgCriYYJC5XOynhARcjjhPWpv8AXm59p3YDAAA=)

>[!note]- $\{ a^{n}b^{m} : n,m \geq 0\text{ e }n\geq100 \text{ allora } n=m\}$
>
>Stabilire se il linguaggio $L$ è regolare.
>
>Proviamo attraverso il pumping lemma:
>
>**Pumping lemma** Se $L$ è regolare allora esiste $p>0$ tale che, per ogni $w \in L$ con $|w| \geq p$ esiste una suddivisione $w := xyz$ tale che:
>- $|xy|\leq p$
>- $|y|>0$
>- $\forall i \in \mathbb{N}\ \ xy^{i}z \in L$ 
>  
>**Procediamo per Assurdo.** Sia per assurdo $L \in REG$, allora per il pumping lemma esiste una lunghezza di pumping $p > 0$.
>
>Consideriamo la stringa $w = a^{p}b^{p}$ abbiamo che:
>- $|w| = 2p \geq p$
>- $w \in L$, perché contiene $p$ `a` e $p$ `b`;
>
>Per il pumping lemma esiste quindi una suddivisione $w = xyz$ con $|xy| \leq p$ e $|y| > 0$.
>
>Quindi dato che $|xy| \leq p$ siamo sicuri che la sotto stringa $y$ sia composta da solo `a`.
>
>Ora prendiamo la stringa $xy^{i}z$ con $i=2$ questa non appartiene a $L$ in quanto ha un numero di `a` maggiore al numero di `b` dato che abbiamo fatto $i^{2}$ quindi il numero di `a` è $p + |y|$ (con $|y|>0$) invece il numero di `b` è p

>[!note]- $\{ w \in \{ a,b \}^{*} : \#_{ab}(w) = \#_{ba}(w) \}$
>
>Stabilire se il linguaggio $L$ è regolare.
>
>![[Pasted image 20261001164344.png|350]]
>
>[Codice Automa](https://automatarium.tdib.xyz#/share/raw/H4sIAAAAAAAAA2XSP08bMRgG8Lvc8e9DdENiCgoJIWSsEKyggljRe7YTXN3Zqf0GiMSECEMnGFgYEEcuCZBOlE8Aa6POHbp3q5hY8RFDe2L9+dHzvrL9ddBQ8jMjuNFqsM7K+sfOFqe_pgulxUqlWKjkabkI+fnFYjUfzFcW8tUyoSWyQKEcQE8jINOnh_He0D2KW0P3wyWnTp_rFS4gfHjxv3Hrx51h9x0P3V3juYznbm3ce+X7Vx7F_TcfoAKhOXIp9NlhUlMyci5RuukKiWJAY_inuXSDkQYjdY166fyMerbByzS4Vv2MerZhLNOQs9PG36lvdCLT4NvsZCbr2+yUzV4RGUVMoD6+1jz6xHQzxOOuuXjUBz3NRT1kMXQDQLJ9cvGNC3MlEK6nT+MkEUNoJwIi1glnYEANLplWZPSn47gXT7_PqzcpLlP+Zn8ed_o7TGlzsd252cJs4Ts0UUaAoHgz2vz_pEekqPF6O0H7eQYvX2JNsRrfi7_cSLXaYApQqnj_FghhDQRBzApmmuKQBBK3u0SGUvWkec06ewZWtM61jgIAAA==)

>[!note]- $\{ w\#t\#w^{R} : w,t \in \{ a,b \}^{*} \text{ e } |w|\leq 5\}$
>
>Stabilire se il linguaggio $L$ è regolare.

>[!note] Dimostrare che un linguaggio è acontestuale se e solo se esiste un PDA che lo riconosce.
>
>**Dimostrazione:**  ${\cal L}(PDA) \subseteq {\cal L}(CFG)$
>
>Sia $L$ il linguaggio contestuale riconosciuto dalla CFG $G = (S, V,\Sigma, R)$, ovvero $L(G) = L$, dove G è in Forma Normale di Chomsky.
>
>Costruiamo il PDA $P = (Q,\Sigma,\Gamma,\delta,q_{start},q_{accept})$  dove:
>- $Q = \{ q_{start},q_{loop},q_{accept} \}$
>- $\Gamma = V \cup \Sigma$
>
>**Dimostrazione:**  ${\cal L}(CFG) \subseteq {\cal L}(PDA)$

