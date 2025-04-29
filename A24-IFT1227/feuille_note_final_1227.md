## **Récursion MIPS**

$$
\begin{equation}
    Puissance(b,e) =
    \begin{cases*}
	    b*Puissance(b,e-1) & si e > 0  \\
	      1        & si e = 0 \\
    \end{cases*}
  \end{equation}
$$

```BASH
.data
.text

main : 
	li a0, b
	li a1, e

	jal puissance    #sauter dans le cas de base
#--------------------------------------------------------------	
	move result,a0 #on affiche le resultat quand on a fini
	li v0, 1
	move a0,result
	syscall
#--------------------------------------------------------------		
puissance: #fct recursive
	bne a1,zero,recursion #si pas = 0, on recurse
	li v0, 1              #sinon valeur = 1 cas de base
	jr ra                 #on remet ce result a l'étape 
	                      #qui aurait suivi si on avait un chiffre

recursion: #step recursif
	addi sp, sp -4   #laisser espace pour le retour
	sw ra, 0(sp)      #stocker le retour à l'appel antérieur
	addi a1,a1, -1    #modifier le paramètre concerné
	jal puissance    #next récursion
	
	mul v0, a0, v0  #le calcul quon fait après avoir atteint le cas de base
	lw ra, 0(sp)    #ce  quon aurait fait (frame précédent)
	addi sp, sp 4   #on vide le stack de cette instruction
	jr ra           #on va au call précédent
```

ex. 2

```
#----------------------
main:
    li $t0, n        
    li $t1, k         
    jal suite         # Appeler la fonction suite

    li $v0, 10        
    syscall
#----------------------

suite:
    # Base case : Si n == 0, retourner 1
    bne $t0, $0, recursion  
    li $v0, 1               # Base case : r = 1
    jr $ra                  # Retourner à l'appelant

recursion:
    
    addi $sp, $sp, -4       # Laisser de l'espace pour le retour
    sw $ra, 0($sp)          # Sauvegarder l'adresse de retour

    # Préparer les arguments pour l'appel récursif
    addi $t0, $t0, -1       # n - 1 (décrémenter $t0)
    addi $t1, $t1, 1        # k + l (incrémenter $t1)
    jal suite               # Appeler suite(n-1, k+l)

    #ce quon fait après base case atteint
						    # Calculer k % n
    div $t1, $t0            # Diviser k par n
    mfhi $s0                # mettre le reste dans $s0 (k % n)

							# Calculer r = r + k % n
    add $v0, $v0, $s0       # Ajouter (k % n) au résultat $v0

    # Restaurer le contexte avant de retourner
    lw $ra, 0($sp)          # Restaurer l'adresse de retour
    addi $sp, $sp, 4        # Libérer l'espace utilisé sur la pile
    jr $ra                  # Retourner à l'appelant

```

---
temps de carry dans ripple adder
$Cn = (P_{n-1}P_{n-2}...P_0C_0) + (P_{n-1}P_{n-2}...P_1G_0) + (P_{n-1}P_{n-2}...P_2G_1) + ... +(P{n-1}G_{n-2}+G_{n-1})$

---
## **VHDL stalling unit**

if ((rsE != 0) AND (rsE == WriteRegM) AND RegWriteM) 
	then ForwardAE = 10
else if ((rsE != 0) AND (rsE == WriteRegW) AND RegWriteW)
	then ForwardAE = 01 
else ForwardAE = 00 

Logique de “Stall”: 
lwstall = ((rsD == rtE) OR (rtD == rtE)) AND MemtoRegE StallF = StallD = FlushE = lwstall

```
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Forwarding_Unit is
    port (
        rsE : in STD_LOGIC_VECTOR(4 downto 0);    -- Registre source de l'ALU (EX)
        WriteRegM : in STD_LOGIC_VECTOR(4 downto 0); -- Registre écrit en MEM
        RegWriteM : in STD_LOGIC;        -- Indique si MEM écrit dans un registre
        WriteRegW : in STD_LOGIC_VECTOR(4 downto 0); -- Registre écrit en WB
        RegWriteW : in STD_LOGIC;           -- Indique si WB écrit dans un registre
        ForwardAE : out STD_LOGIC_VECTOR(1 downto 0) -- Signal de forward de l'ALU
    );
end Forwarding_Unit;
---------------------------------------------------------------------------------
architecture Behavioral of Forwarding_Unit is
begin
    process(rsE, WriteRegM, RegWriteM, WriteRegW, RegWriteW)
    begin
        if (rsE /= "00000" and rsE = WriteRegM and RegWriteM = '1') then
            ForwardAE <= "10";  -- Forward depuis MEM
        elsif (rsE /= "00000" and rsE = WriteRegW and RegWriteW = '1') then
            ForwardAE <= "01";  -- Forward depuis WB
        else
            ForwardAE <= "00";  -- Pas de forwarding
        end if;
    end process;
end Behavioral;

---------------------------------------------------------------------------------

entity Stalling_Unit is
    port (
        rsD : in STD_LOGIC_VECTOR(4 downto 0);   -- Registre source en Decode (ID)
        rtD : in STD_LOGIC_VECTOR(4 downto 0); -- Deuxième regsource en Decode (ID)
        rtE : in STD_LOGIC_VECTOR(4 downto 0);-- Reg destination en Execute (EX)
        MemtoRegE : in STD_LOGIC;    -- Indique si l'instruction en EX est un `lw`
        StallF : out STD_LOGIC;                     -- Bloque l'étape Fetch
        StallD : out STD_LOGIC;                     -- Bloque l'étape Decode
        FlushE : out STD_LOGIC                      -- Vide l'étape Execute
    );
end Stalling_Unit;
----------------------------------------------------------------------------------

architecture Behavioral of Stalling_Unit is
begin
    process(rsD, rtD, rtE, MemtoRegE)
    begin
        if ((rsD = rtE or rtD = rtE) and MemtoRegE = '1') then
            StallF <= '1'; -- Bloque le Fetch
            StallD <= '1'; -- Bloque le Decode
            FlushE <= '1'; -- Vide l'étape Execute
        else
            StallF <= '0';
            StallD <= '0';
            FlushE <= '0';
        end if;
    end process;
end Behavioral;


```

---
## **PIPELINE**

phases  de pipeline :
- coloré à gauche = écriture
- coloré à droite = lecture
- coloré au complet = occupé tout le cycle
### **Cycles requis pour chaque instru**

| **Type d'instruction**     | **Description**        | **Étapes prises**        | **Nbr cycles** |
| -------------------------- | ---------------------- | ------------------------ | -------------- |
| **R-Type (arithmétique)**  | `add`, `sub`, `and`... | IF → ID → ALU → WB       | **4 cycles**   |
| **I-Type (accès mémoire)** | `lw`, `sw`             | IF → ID → ALU → MEM → WB | **5 cycles**   |
| **I-Type (arithmétique)**  | `addi`, `andi`         | IF → ID → ALU → WB       | **4 cycles**   |
| **Branch**                 | `beq`, `bne`           | IF → ID → ALU            | **3 cycles**   |
| **Jump**                   | `j`, `jal`             | IF → ID → ALU            | **3 cycles**   |
## **Les trucs sont prêts quand**

| **Instru**                | **EX (ALU)**             | **MEM**                  | **WB**                 | **data prete à ?**                |
| ------------------------- | ------------------------ | ------------------------ | ---------------------- | --------------------------------- |
| **R (`add`, `sub`)**      | Résultat calculé         | -                        | Écrit dans le registre | **fin de ALU**                    |
| **Load (`lw`)**           | Adresse mémoire calculée | Valeur chargée           | Écrit dans le registre | **fin de MEM**                    |
| **Store (`sw`)**          | Adresse mémoire calculée | Valeur écrite en mémoire | -                      | **avant MEM**                     |
| **Branch (`beq`, `bne`)** | Comp. calculé            | -                        | -                      | **fin de ALU***                   |
| **Jump (`j`)**            | -                        | -                        | -                      | **Pendant ID**                    |
| **Jump Register (`jr`)**  | -                        | -                        | -                      | **Pendant ID (si prêt)** ou stall |

### **Quand je stall

Si **Instruction 1** produit une donnée dans une étape **PLUS TARD** à celle où **Instruction 2** en a besoin

## **Qand je forward**

Si **Instruction 1** produit une donnée dans une étape (ALU ou MEM) **avant que l'étape où Instruction 2 en a besoin ne commence**, je **forward

## **Résumé des Cas**



---
## **RAM, ROM**

| **Type de mémoire** | Description                                                                                                                  | **l'utilité**                                                   | **Sur la carte physique**    |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- | ---------------------------- |
| **DRAM**            | - Ne conserve pas son contenu qd on l'éteint<br>- Par cher  <br>- Utilise des condensateurs, faut un rechargement périodique | Mémoire centrale                                                | Condensateurs et transistors |
| **SRAM**            | - Ne conserve pas son contenu qd on l'éteint<br>- Très rapide <br>- Plus chère que la DRAM                                   | Cache mémoire (L1, L2, L3)                                      | Latches ou Flip-flops        |
| **ROM**             | - Conserve son contenu  (non volatile)  <br>- Souvent réinscriptible (EEPROM, clée USB)                                      | Stockage permanent (Firmware) donc cartes mère, BIOS et tout ça | Transistors                  |

gros résumé des mémoires

- **Pour coder une RAM**, on programme **ligne par ligne** (via wordlines et bitlines).
- **Pour coder une ROM**, on programme **colonne par colonne** (logique combinatoire par colo.)
- **Pour accéder à la RAM ou à la ROM**, l’accès se fait **par adresse** qui active une ligne spécifique avec un **DECODEUR POUR LES 2**

==exo lecture de RAM==

| Adresse $(2^n)$ | **Wordline** | **Contenu (m = 4 bitlines)** |
| --------------- | ------------ | ---------------------------- |
| 00              | 0            | `1010`                       |
| 01              | 1            | `1100`                       |
| 10              | 2            | `1111`                       |
| 11              | 3            | `0001`                       |
```vhdl
Si signal = 10 -> wordline = 2 -> donc on obtien 1111
```


Logique des ROMS

Soit
$X = AB$
$Y = A+B$, 
$Z = A\overline B$

On créer la mémoire associée pour $2^2$ x 3 bits

| A,B $(2^n)$ | **Bitline2 x** | **Bitline1 y ** | **Bitline0 z** |
| ----------- | -------------- | --------------- | -------------- |
| 00          | \|             | \|              | \|             |
| 01          | \|             | .               | \|             |
| 10          | \|             | .               | .              |
| 11          | .              | .               | \|             |


---
Traduire du code mips en binaire +hexadécimal

-Identifier type R, I , J

Complément à deux
- La valeur est `-5`. En complément à deux sur 16 bits :
    1. binaire de `5` : `0000 0000 0000 0101`.
    2. INVERSION   : `1111 1111 1111 1010`.
    3. Add `1`          : `1111 1111 1111 1011`.

Immediate offset =  `1111 1111 1111 1011`.


![[jumppseudodirect.jpg]]

![[beq 1.jpg]]

![[mips cycle 1.jpg]]
![[datapathmulticycle.jpg]]

---

# CACHE

### Taux de succès et d’échec**

- **Total d’instructions** = 2,000 (lecture/écriture)
- **Succès (Hit)** = 1,250
- **Échec (Miss)** = 750

1. **Taux de succès (TS)** :
    $SUCCES/TOTAL = 1250/2000 = 0.625$
2. **Taux d’échec (TE)** :
    $ECHEC/TOTAL = 750/2000 = 0.375$

 Temps moyen d’accès à la mémoire (TMAM)
 - **Temps d’accès au cache**  = 1 cycle 
 - **Temps d’accès à la mémoire principale** = 100 cycles
 - **Taux d’échec** = 0.375

 **Formule pour TMAM :**
	 $t_{cache}​+TE⋅t_{MP}​$ 
	 1+ 0.375(100) =38,7 CYCLE

| **Concept**                   | **Explication**                                        | **Valeur**      |
| ----------------------------- | ------------------------------------------------------ | --------------- |
| **Capacité (C)**              | Nombre ***total*** d’aliments qu'on stocke (en octets) | C=64            |
| **Taille d’un bloc (b)**      | Taille d'un transfert (panier)                         | b=4             |
| **Nombre de blocs (B)**       | Nombre total de paniers dans le cache.                 | B=C/b : 64/4=16 |
| **Degré d’associativité (N)** | Nbr d'étagères                                         | N=2             |
| **Nombre d’ensembles (S)**    | Nombre de rayons par étagères                          | S=B/N: 16/2=8   |
###
 
# mémoire virtuelle

| **Unité** | **Exposant** | **Conversion    |
| --------- | ------------ | --------------- |
| **KB**    | $2^{10}$     | 1KB=1024 octets |
| **MB**    | $2^{20}$     | 1MB=1024 KB     |
| **GB**    | $2^{30}$     | 1GB=1024 MB     |

---

si  mémoire virtuelle= 2^{31}
que la ram =  $2^{27}$
et page = $2^{12}$

donc
- l'adresse virtuelle s'écrit sur 31 bits
- l'adresse physique s'écrit sur 27 bits
- on regarde les 12 bits les + faibles pr avoir l off set (3 hex)
nbr Pages virtuelles = $\dfrac{2^{31}}{2^{12}} = 2^{19}$

| page virtuelle | offset |
| -------------- | ------ |
| 0x00002        | 47c    |
- on regarde où la page virtuelle hit = 1
- on prend la page physique et on concatène le offset
- ex.  0x00002 hit = 0x7fff
**donc page physique = 0x7fff:47c**
