---
type: Programming Note
programming language:
related:
completed: false
created: 2025-12-12T15:27
updated: 2026-04-29T22:51
---
## Apps

`brew install --cask bitwarden ente-auth zen discord obsidian onlyoffice pika raycast karabiner-elements`

`brew install --cask github visual-studio-code ghostty`

>[!note] Notes
>- [Install Battery-Toolkit (aldente alternative)](https://github.com/mhaeuser/Battery-Toolkit)
>- Discord Themes: [Vencord Installer](https://vencord.dev/download/) - [Theme](https://github.com/catppuccin/discord?tab=readme-ov-file)
>- Remember to add [NextDNS](https://nextdns.io/)

## Programming Languages

```
brew install node golang rust
```

## Terminal

`brew install stow fish starship zoxide atuin eza bat gitui bob container`

>[!note] Configs
>
>1. clone https://github.com/rimaout/.dotfiles
>2. use `stow` for linking the configs 

>[!note] Notes
>- *Install Cascadia Cove Font:* `brew install --cask font-caskaydia-cove-nerd-font`
>- *add bob path to fish:* `fish_add_path ~/.local/share/bob/nvim-bin`

On mac os when you open a new terminal window a message like this is printed: `Last login: Sat Jan 31 13:51:18 on ttys004`, to disable this just do `touch ~/.hushlogin`.

## Cluster Sapienza

Install open vpn connect to access Sapienza network: `brew install openvpn-connect`
...

Use `ssh surname_studentId@192.168.0.102` to connect, but this will ask for you user password.

I like to create a ssh key for the login, so I don't have to type the password each time:
1. create the ssh key: `ssh-keygen -t ed25519 -f ~/.ssh/sapienza_cluster`
2. save the public key to the server: `ssh-copy-id -i ~/.ssh/sapienza_cluster.pub surname_studentId@192.168.0.102`
3. I like also to add ...

Here is the consolidated guide, rewritten to be clear, copy-pasteable, and easy for other students to follow.

I have organized it logically: **Connection** $\to$ **Security (No Password)** $\to$ **Convenience (Short Alias)**.

---

# Sapienza Cluster Access Guide

### 1. Prerequisites (VPN)

You must be connected to the Sapienza network to access the cluster.

- **Install OpenVPN Connect:**
    
    Bash
    
    ```
    brew install openvpn-connect
    ```
    
- _Make sure your VPN is active before proceeding._
    

---

### 2. Create an SSH Key

_Why? So you don't have to type your password every time you log in._

Run the following command to generate a specific key for this cluster (using the modern `ed25519` algorithm):

Bash

```
ssh-keygen -t ed25519 -f ~/.ssh/sapienza_cluster
```

_(Press Enter to accept defaults. You can leave the passphrase empty if you want fully automatic login)._

Next, copy this key to the server. Replace `surname_studentId` with your actual username:

Bash

```
ssh-copy-id -i ~/.ssh/sapienza_cluster.pub surname_studentId@192.168.0.102
```

_(You will be asked to enter your cluster password one last time)._

---

### 3. Create an SSH Short Alias

_Why? So you can type `ssh sapienza` instead of the long command._

1. Open your SSH config file:
    
    Bash
    
    ```
    nano ~/.ssh/config
    ```
    
2. Paste the following block into the file. **Make sure to replace `surname_studentId` with your specific username:**
    
    Plaintext
    
    ```
    Host sapienza
        HostName 192.168.0.102
        User surname_studentId
        IdentityFile ~/.ssh/sapienza_cluster
    ```
    
3. Save and exit (`Ctrl + O`, `Enter`, `Ctrl + X`).
    

---

### 4. How to Connect

Now that everything is set up, you can simply run:

Bash

```
ssh sapienza
```

---


## Domanda 1

Matteo, 22 anni, Studente Universitario (informatica)

## Domanda 2

Per la produttività utilizzo principalmente un app sola Task (da telefono) che serve per scrivere le cose da fare o le idee che mi vengono. Poi anche il calendario ma lo uso solo per segnare gli impegni.

## Domanda 3

Si le uso ancora, un app che ho smesso di usare è tomato clock (un app che ti fare seguire la tecnica del pomodoro, vedi: https://en.wikipedia.org/wiki/Pomodoro_Technique ) ho smesso perché quando trovo il focus mi sebra stupido perderlo facendo una pausa.

## Domanda 4

Non ho dei momenti specifici in cui le uso, quando mi servono (ad esempio mi viene idea o scopro una cosa da fare) uso le app sopra citate.

Non pianifico le mie daily activities, uso l'app task per segnare le cose da fare (solitamente senza scadenza), poi uso il calendario per segnarmi le cose che hanno una scadenza precisa.

## Domanda 5

Dell'app task mi piace molto la possibilità di poter specificare le sotto attività in mdi un task, ad esempio il task preparare esame analisi può essere composto da più sotto task come fare esercizio x, studiare pagina y, are domanda al prof ecc.

Quello che non mi piace è che è difficile integrarla con il calendario, e che non è possibile integrarla con le note audio.

Molto spesso uso le note audio per salvarmi le idee che mi vengono / cose da fare mentre cammino o non mi va di scrivere. sarebbe bello se ci fosse un modo di convertire le mie note audio in task dell'app.

## Domanda 6

La feature che è diventato un abit che mi fa spesso usare l'app delle task è le notifiche basate sulla priorità.

Infatti quando crei un task ti viene chisto di inserire una priorità (da 1 a 5) e in base a quanto è alta ti vengono mandate delle notifiche più o meno ricorrenti, per ricordarti del task. Questo è utile per tutte quelle cose che non hanno una scadenza precisa ma che allo stesso momento sono importati da fare.

## Domanda 7

Solitamente all'università o dei momenti dedicati al solo studio senza distrazioni. Però non uso app particolari, disabilito le notifiche dal telefono e lo metto il più lontano possibile.

## Domanda 8

Si voglio e cerco attivamente di limitare il mio screen time, specialmente quello involontario (ovvero quando prendi il telefono e neanche sai perché).

## Domanda 9

Si credo che il tempo  sia una fonte di distrazione, però sono anche un caso un pò particolare, infatti:
- non ho social sul telefono (no instagram, no spotify, no youtube)
- per evitare di perdere tempo online ho un browser che dimentica tutto quando lo chiudi, quindi ogni volta andare su un sito (esempio vinted, youtube, instagram ...) bisogna loggare di nuovo.
- non ho giochi

Quindi penso che il telefono sia una fonte di distrazione, ma per come lo ho impostato io non c'è molto su cui distrarsi ahhah

Oramai non mi capita quasi mai di scrollare a caso sul telefono, ho dei momenti in cui voglio distarmi, in quel caso mi capita di andare su internet e leggere siti e blog che mi interessano, ma data la difficoltà nell accedere è una azione volontaria.

Sono sicuro che un delay nell aprire un applicazione sia un buon modo per ridurre la facilità di accesso alle distrazioni, però forse per certe app servono contro misure più difficili (tipo rompicapo o richieste di scrivere qualcosa).

## Domanda 10 

No non ho usato app per bloccare altre app, per il time management uso le statistiche del telefono però solo per vedere quali app uso di più.

Penso che bloccare determinate app in base al task che si sta svolgendo possa essere una feature molto utile, però bisogna far attenzione a non renderla troppo complicata. Magari può essere integrata con il calendario per gli venti ricorrenti. Tipo se sto in palestra soltanto l'app per la palestra e i messaggi sono utilizzabili.

## Domanda 11

Penso che tutte e due siano buone e utili idee, non debbano essere mutualmente esclusive.

## Domande 12

Quando stavo cercando di ridurre il tempo speso al telefono usavo molto spesso le statistiche del telefono. Mi avrebbe fatto molto comodo ricevere consigli su come ridurre il tempo, magari ricevendo consigli specifici per le varie app.