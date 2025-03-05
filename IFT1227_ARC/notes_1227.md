
---
# Introduction : Architecture des ordinateurs

- Langages haut niveau (Compilation) 
- Langage d'assemblage (Assembleur )
- Système d'exploitation (Appels système) 
- Jeu d'instructions propre à chaque machine Microprogrammes : micro-instructions binaires - Interprétation directe 
- Microarchitecture (UAL, UC, registres, ...) (Assemblage physique des portes logiques )
- Circuits logiques

**Couche logique combinatoire**: couche comportant uniquement des **gates** (AND OR NOT XOR NAND) conçus via des [transistors](note_transistors.pdf) et dont la sortie dépend de l'entrée uniquement

**Couche logique séquentielle** : couche comportant non seulement des **gates** mais des **verrous** et **bascules** afin de garder en **mémoire** des informations (états)

>==Note: on utilise les circuits séquentiel pour reconnaitre et détecter des **séquences** multi-digits dans des cas où on ne peux entrer qu'**un** seul bit à la fois==

Byte = 10101110, nibble = 1010, 1110
<div style="page-break-after: always;"></div>

---
#### Rappel des équations booléennes pour Y
SOP = $\sum (y=1, \forall abc...n)$
POS =$\prod (y=0) \rightarrow inverser, \forall abc...n$

| **Règle / Loi**          | **Expression**                                                |
| ------------------------ | ------------------------------------------------------------- |
| **Identité**             | A · 1 = A,  A + 0 = A                                         |
| **Domination**           | A · 0 = 0,  A + 1 = 1                                         |
| **Idempotence**          | A · A = A,  A + A = A                                         |
| **Complément**           | A · $\neg$ A = 0,  A + $\neg$ A = 1                           |
| **Commutativité**        | A · B = B · A,  A + B = B + A                                 |
| **Associativité**        | (A · B) · C = A · (B · C)                                     |
|                          | (A + B) + C = A + (B + C)                                     |
| **Distributivité**       | A · (B + C) = (A · B) + (A · C)                               |
|                          | A + (B · C) = (A + B) · (A + C)                               |
| **Loi d'absorption**     | A · (A + B) = A,  A + (A · B) = A                             |
| **Loi de De Morgan**     | $\neg$ (A · B) = $\neg$ A + $\neg$ B                          |
|                          | $\neg$ (A + B) = $\neg$ A · $\neg$ B                          |
| **Complémentarité**      | A + $\neg$ A = 1,  A · $\neg$ A = 0                           |
| **Loi de consensus**     | (A · B) + ($\neg$ A · C) + (B · C) = (A · B) + ($\neg$ A · C) |
| **Loi du zéro et du un** | A · 0 = 0,  A + 1 = 1                                         |
| **Loi de neutralité**    | A · 1 = A,  A + 0 = A                                         |
| **Loi de dominance**     | A · 0 = 0,  A + 1 = 1                                         |

---
### Niveaux de tension

*==Dans==* le cas ou le signal est entre 1 et 0, on peux **accepter/tolérer** des signaux dans certaines marges

>Note : ca 

**Marge de bruit (“Noise Margin”)**
Noise Margin High = VOH – VIH 
Noise Margin Low = VIL – VOL

---
# Machines de Moore et Mealy

### Latch vs Flip-flop

- **Latch** : La sortie **Q** suit l'entrée **D** tant que l'horloge est à '1'. Quand l'horloge passe à '0', **Q** reste figée.
- **Flip-Flop** : La sortie **Q** change **seulement** sur un front d'horloge (par exemple, le front montant). Entre deux fronts d'horloge, la sortie **Q** ne change pas, même si **D** change.
### VHDL

> [!NOTE]
> **Librairies** ==importe== les modules nécessaires (STD_LOGIC n'est **pas** natif)
> **L'entité** est la ==**chose**== qui possède des entrées/sorties
> **Architecture** est la ==définition== de que qui se passe entre les entrées et sorties de l'entité
#### exemple de STD_LOGIC simple
```vhdl
library IEEE; use IEEE.STD_LOGIC_1164.all;

entity gates is
-- on créé un bloc qui a en input 2 bus de 4 bits et en sorties 5 bus de 4 bits 
	Port (	a,b :in STD_LOGIC_VECTOR (3 downto 0);
			y1,y2,y3,y4,y5 : out STD_LOGIC_VECTOR (3 downto 0);
	);
end 
-- la on dit la logique qui se passe entre les inputs et outputs, donc la sortie 
-- y1 est le and bitwise entre les bus a et b
architecture synth of gates is
begin
	y1<= a and b;
	y2<= a xor b;
	y3<= a or b;
	y4<= a nand b;
	y5<= a nor b;
end;
```

---
### Exemple Mux

1) librairies :
```VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all;
```
2) entité avec ports in et out
```vhdl
entity mux is
Ports(
	d0:in STD_LOGIC;
	d1:in STD_LOGIC;
	d2:in STD_LOGIC;
	d3:in STD_LOGIC;
	d4:in STD_LOGIC;
	d5:in STD_LOGIC;
	d6:in STD_LOGIC;
	d7:in STD_LOGIC;
	S :in std_logic_vector(2 downto 0); -- 3 bits pour la sélection
	y:out STD_LOGIC;
)
```

3)Architecture, process 1 : quand je suis dans le cas X, y vaut quoi? 

```vhdl
architecture Behavioral of MUX_8to1 is 
	begin process(D0, D1, D2, D3, D4, D5, D6, D7, S);  
		case S is 
			when "000" => Y <= D0; -- Si S = 000, Y prend la valeur de D0 
			when "001" => Y <= D1; -- Si S = 001, Y prend la valeur de D1 
			when "010" => Y <= D2; -- Si S = 010, Y prend la valeur de D2 
			when "011" => Y <= D3; -- Si S = 011, Y prend la valeur de D3 
			when "100" => Y <= D4; -- Si S = 100, Y prend la valeur de D4 
			when "101" => Y <= D5; -- Si S = 101, Y prend la valeur de D5 
			when "110" => Y <= D6; -- Si S = 110, Y prend la valeur de D6
			when "111" => Y <= D7; -- Si S = 111, Y prend la valeur de D7 
			when others => Y <= '0'; -- Valeur par défaut si S est invalide 
		end case; 
	end process; 
end Behavioral;
```

---
### Mux 4:1

```vhdl
library IEEE; use IEEE.STD_LOGIC_1164.all;

entity mux4 is
	Ports(
	d0,d1,d2,d3:in STD_LOGIC;
	s:IN STD_LOGIC_vector(1 downto 0);
	Y:out STD_LOGIC
	);
end mux4

architecture synth of mux4 is
	process(d0,d1,d2,d3,s)
		case s is
			when "00" => y <= d0;
			when "01" => y <= d1;
			when "10" => y <= d2;
			when "11" => y <= d3;
			when others => y <= '0';
		end case; 
	end process; 
end synth;
```

---
### Exemple Decoder
Exo decodeur 2: 4

```vhdl

library IEEE; use IEEE.STD_LOGIC_1164.all;

entity dec2to4 is
Ports(
	d0,d1:in STD_LOGIC;
	y0,y1,y2,y3L out STD_LOGIC;
	); 
end dec2to4;

architecture synth of dec2to4 is
begin -- Initialisation des sorties 
y0 <= '0'; 
y1 <= '0'; 
y2 <= '0'; 
y3 <= '0';
	process(d0, d1)
	signal bus : d0&d1;
		case (bus) is
			when "00" => y0 <='1';
			when "01" => y1 <='1';
			when "10" => y2 <='1';
			when "11" => y3 <='1';
		end case
	end process
end synth
```

---
#### Exemple Moore FSM 

> [!NOTE]
> Très important; on a autant des **inputs** que des **states**, mais ils ne sont pas la même chose, le input est ce qui est **entré** par le user, le state est l'**étape ou on est rendu** (*chaque state à un comportement particuliers aux inputs*)

==EXO: un stylo à pression==

En inputs:
- l'action de cliquer "clic"
- l'horloge (clock)
- reset (pour démarrer la FSM)
En output:
- la possibilité d'écrire "write"

```VHDL FSM
library IEEE; use IEEE.STD_LOGIC_1164.all;

entity stylo is 
	Ports(
	clic : in STD_LOGIC;
	clock: in STD_LOGIC;
	reset: in STD_LOGIC;
	write: out STD_LOGIC;
end stylo;
	)
```

Architecture de la FSM:
 C'est une machine qui a 2 états:
	- on a un array d'états (pointe_in, pointe out) de type state_type
	- le signal nous permettra de nous déplacer dans l'array de state_type

```VHDL
architecture Structure of stylo is
	type state_type is (pointe_in, pointe_out);
	signal state, next_state: state_type;	
```


>Ici, on dit juste qu'on a les états et qu'on pourra changer d'état mais on ne dit pas ==**comment**==

**Premier** processus de changement d'état (avec clock et reset)
	- D'abord on reset la machine (démarrer en pointe_in ) si reset est "true"
	- sinon à chaque rising_edge de clock, on va changer d'état (en fonction du input, donc on peut "changer" vers le même état, bête mais bon).
	
```VHDL
process (clk,reset)
begin
if reset= '1' then
	state <=  pointe_in;
elsif rising_edge(clk) then
	state<= next_state;
end if
end process
```

Deuxième processus, logique des transitions
	la c'est le tableau de changement d'état, dépendamment de ou on est et quel est l'input, next_state deviens quoi?
	
```VHDL
process (state,clic)
begin
	case state is
		when 'pointe_in'
			if 'clic' = '1' then
			next_state <= pointe_out
			elsif 'clic' = '0' then
			next_state <= pointe_in
		when 'pointe_out'
		if 'clic' = '1' then
			next_state <= pointe_in
			elsif 'clic' = '0' then
			next_state <= pointe_out

if reset= '1' then
	state <=  pointe_in;
elsif rising_edge(clk) then
	state<= next_state;
end if
end process
```

Troisième processus, la sortie en fonction de l'état (parce que c'est Moore et on ==dépend uniquement du state==)

```VHDL
process(state)
begin
case state is
	when pointe_in => 
		write <= '0'
		
	when pointe_out => 
		write <= '1'
	end case;
end process;
end Structure;
```

---
#### Cas machine de Mealy pour le même stylo

donc step 1 : définir l'entité

```VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all;

entity stylo_mealy is
Ports(
	clk:in STD_LOGIC;
	reset:in STD_LOGIC;
	clic:in STD_LOGIC;
	write:out STD_LOGIC;
)
end stylo_mealy;
```

Architecture, on defini les états de la machine sans dire vraiment comment on va explicitement changer d'etat

```VHDL
architecture Structure of stylo is

	type type_state is (state,next_state);
	signal state, next_state: state_type;
```

Premier processus : le reset et le rising_edge:

``` VHDL
	process(clk, reset)
	begin
		if reset <= '1' then
			state <= pointe_in;
		elsif rising_edge(clk) then
			state <= next_state;
		end if
	end process
```

deuxième processus : de l'état présent, on va vers quel état dépendamment du clic?

```VHDL
process(state, clic)
begin
case state is
	when pointe_in
		if clic <= '1' then
		next_state <= pointe_out;
		if clic <= '0'then
		next_state <= pointe_in;
		
	when pointe_out
		if clic <= '1' then
		next_state <= pointe_in;
		if clic <= '0'then
		next_state <= pointe_out;
		end case;
end process;
```

troisième processus , en fonction de l'état et du clic, quel est le output?

```VHDL
process(state, clic)
begin

case state is
	when pointe_in
		if clic <= '1' then
		write <= '1';
		if clic <= '0' then
		write <= '0';
	when pointe_ou'
		if clic <= '1' then
		write <= '0';
		if clic <= '0' then
		write <= '1';
	end case;
	end process;
	end Structure;
```

> [!NOTE] Note
> La machine de Moore possède dans le troisième processus **seulement state** comme paramètre pour le output, il n'y a **pas de if clic** pour avoir le résultat. La machine de Mealy a non seulement state mais **clic aussi en paramètres** du process, et dans les case when on voit les **if clic**, donc le output dépend des deux

---

>Moore (seulement state en paramètres, write direct en fonction du state):
>process(state) 
>...
	when pointe_in => write <= '0' --une ligne, the when demande => 

>Mealy (state et clic en paramètes, write en fonction du state et du clic via un if-clic):
>process(state, clic) 
>...
	when pointe_in
		if clic <= '1' then		--le if demande un then
		write <= '0';

---
### FSM bizarre 2 input one-hot


> [!NOTE] Note
> À 2 inputs AB possible, la valeur de la flèche signifie la table de vérité de la ou les lettres qui figurent.  Si l'input est A, c'est les cas **1**0 et **1**1, not B c'est les cas 0**0** et 1**0**, AB c'est le cas 11 uniquement.

---
exo : Machine de Moore 2 inputs

![[fsm_weird.jpg]]

---
1) Table transitions en 

S0: = 001 en one-hot
Si input = A (10 ou 11) =>S1
Si input = not A (00 ou 01) =>S0

S1: = 010 en one-hot
Si input = B (01 ou 11) =>S2
Si input = not B (00 ou 10) =>S0

S2: ==OUT =1==, = 100 en one-hot
Si input = B (01 ou 11) =>S2
Si input = not B (00 ou 10) =>S0

<div style="page-break-after: always;"></div>


#### Encodage One-Hot
**B2B1B0 ---  AB --- B2'B1'B0' ---OUT**

001  00  001 0
001  01  001 0
001  10  010 0
001  11  010 0

010  00  001 0
010  01  100 0
010  10  001 0
010  11  100 0

100  00  001 1
100  01  100 1
100  10  001 1
100  11  100 1

**3) SOP pour B2' B1' B0' et OUT**

B2' = 01001 OR  01011 OR 10001 OR 10011
B1' = 00110 OR 00111
B0' = 00100 OR 00101 OR 01000 OR 01010 OR 10000 OR 10010

>  Faire un décodeur qui prend en **entrée** les bits B2,B1,B0,A,B, (ex. 10011), faire les combinaisons **SOP de chaque bit futur** (donc regrouper les cas d'entrées des B2,B1,B0,A,B ) puis les lier à leur flip flop respectif (donc B2' est le OR de 4 combinaisons d'entrées du décodeur), le OUT est juste une logic gate

<div style="page-break-after: always;"></div>

---
### En version VHDL

``` VHDL
library IEEE; use IEEE.STD_LOGIC_1164.ALL;
entity fsm is
    port (
        clk, RESET, A,B :in std_logic;
        Q : out std_logic
    );
end fsm;

architecture Behavioral of fsm is
    type state_type is (state_001, state_010, state_100);
    signal state, next_state : state_type;

begin
    process (clk, reset)
    begin
        if reset = '1' then
            state <= state_001;
        elsif rising_edge(clk) then
            state <= next_state;
        end if;
    end process;
```

<div style="page-break-after: always;"></div>

Processus (transition d'états, logique output)

``` VHDL
    process (state, A, B)
    begin
        next_state <= state;
        case state is
            when state_001 =>
                if A = '1' then
                    next_state < = state_010;
                end if;
            when state_010 =>
                if B = '1' then
                    next_state < = state_100;
                end if;
            when state_100 =>
                next_state < = state_001;
            when others =>
                next_state < = state_001;
        end case;
    end process;
-- fin des transitions d etats
    process (state)
    begin
        case state is
            when state_100 =>
                Q < = '1';
            when others =>
                Q < = '0';
        end case;
    end process;
 -- fin des outputs
end Behavioral;

```

<div style="page-break-after: always;"></div>


### Components en VHDL (et port map)

<div style="page-break-after: always;"></div>

```VHDL
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity top_level is
    port (
        A, B, C : in std_logic;  -- Entrées A, B, C
        S1, S2 : in std_logic;   -- Bits de sélection S1 et S2
        Y : out std_logic        -- Sortie finale Y
    );
end top_level;

architecture Structural of top_level is
    -- Déclaration du multiplexeur 2:1
    component mux_2to1
        port (
            I0, I1 : in std_logic;
            S : in std_logic;
            Y : out std_logic
        );
    end component;

    -- Signal interne pour connecter les deux multiplexeurs
    signal inter_signal : std_logic;

begin
    mux1: mux_2to1 --premier mux
        port map(
            I0 => A,        -- Entrée I0 du premier MUX est A
            I1 => B,        -- Entrée I1 du premier MUX est B
            S => S1,        -- Bit de sélection du premier MUX est S1
            Y => inter_signal  -- La sortie du premier MUX va vers inter_signal
        );
        
    mux2: mux_2to1 -- deuxieme mux
        port map(
            I0 => inter_signal,  -- Entrée I0 du second MUX est la sortie du premier MUX
            I1 => C,             -- Entrée I1 du second MUX est C
            S => S2,             -- Bit de sélection du second MUX est S2
            Y => Y               -- La sortie finale Y
        );
end Structural;
```

---
# Langage assembleur data (MIPS - RISC)

32 registres dont:
types "v" = retour de sous-opérations
types "a" = arguments
types "t" = temporaires 
types "s" = sauvegardés

Doc de référence


![[MIPS_Green_Sheet.pdf]]



Notions de base:
1 byte = 8 bits
1 halfword = 2 bytes (16 bits)
1 word = 4 bytes (32 bits)

Adresses et pointeurs:

La mémoire est comme un gros array, et les éléments ont comme index l'adresse à laquelle ils sont stockés

>==Langage machine != langage assembleur==. Le langage machine serait 1009018700000342 et en assembleur ce serait **add, $ a0, $ t0, $ t1**


MIPS est un langage proche du matériel, la **complexité des opérations diminue** et le **nombre de lignes à coder augmente**

ex. "Prend une cuillère à soupe et mange ce plat" VS

"Prépare toi à tenir un objet : 
- L'objet est une cuillère  
Prend ta main droite: 
- "Tant que tu n'as pas touché la cuillère, avance" 
Si ta main touche, agrippe la cuillère:
- "tant que tu n'as pas touché le bol, avance" 
Si tu touches le bol avec la cuillère, plonge la cuillère: 
- "etc..."

---
#### Registres MIPS

**v0-v1** =  ==retournent== les valeurs des appels de fonctions ; si quelque chose est calculé, il est gardé dans v0 et v0+v1 si le résultat est sur 64 bits

**t0-t9** = registres qui ne sont ==pas sauvegardé==s et qui peuvent être réécris sans problème

**s0-s7** = registres dont la valeur est ==gardée== dans la pile (ne peuvent pas êtres directement changés)

**a0-a3** = registres servant d'arguments aux fonctions

---
# Fonctions et system calls

##### **Décortiquer le problème: Lire 2 input numériques, les additionner, imprimer la somme 
**

1) *Préparer* le système à lire un int ($v0 <-5)
2) Syscall (lecture)
3) Déplacer le contenu de retour dans un registre ($t0 <- $v0)
4) Préparer le système à lire un autre int ($v0 <-5)
5) Syscall (lecture)
6)  Déplacer le contenu de retour dans un registre ($t1 <- $v0)
7) Additionner les valeurs des 2 registres dans un troisième registre (add $t2, $t1, $t0)
8) Déplacer le contenu du troisième registre dans une case destinée à l'affichage ($a0 <- $t2)
9) Faire comprendre au système qu'on veux imprimer un int $v0 <-1)
10) Call

##### **et maintenant en code :**

```MIPS
.data
.text
main:
	li      $v0,5
	syscall
	move    $t0,$v0
	
	li      $v0,5
	syscall
	move    $t1,$v0
	
	add     $t2,$t1,$t0
	
	move    $a0,$t2
	li      $v0,1
	syscall

```

---
### Exemple `larger.asm` : lire 2 input numériques, afficher le plus grand

Décortiquer le problème:

1) Préparer le système à lire un int #1 ( $v0 <- 5 )
2) Syscall (lecture)
3) Save dans un registre ($t0 <- $v0)
4) Préparer le système à lire un int #2 ( $v0 <- 5 ) 
5) Syscall (lecture)
6) Save dans un registre ($t0 <- $v0)
7) Branch on Greater Or Equal vers *t0_bigger* si input#1 > input#2
8) *t0_bigger* : 
	1) affecte t0 dans le registre "larger" $t2
	2) Branch à "*fin*" 
	3) sinon…
9) Save t1 dans le registre "larger" $t2
10) *fin* :
	1) Préparer le système à afficher un int ($v0 <- 1)
	2) Mettre dans le registre pour afficher la valeur de t2 ($a0 <- $t2 )
	3) Syscall

en code : 

```MIPS
.data
.text
main: 
	li $v0,5
	syscall
	move $t0, $v0
	
	li $v0,5
	syscall
	move $t1, $v0
	
	bgt $t0,$t1, t0_big #si  t0 > t1 on va à t0_big
	move $t2,t1         #sinon on continue
	b endif             #on saute a la fin du programme
t0_big:
	move $t2,t0
	# pas besoin de branch, on y va direct
endif:
	move $a0, $t2
	li $v0,1
	syscall
```

 >[!TRICKS]
 >.byte 0 : + 0 byte.
 >.ascii "\n"      # C **newline**. 
 >.asciiz            # \n en fin de ligne
 >.byte 0xA      # hex ASCII **newline**
 >.byte 0x0       # hex ASCII **NULL**
 
 ---
 Algorithme de multiplication **séquentielle**:

Une multiplication est une addition **successive**. On va ajoute un int B à un int A, et lorsqu'on  cette somme atteint le nombre 

Donc: pour 3* 4
1) Obtenir A de user (3)
2) Obtenir B de user (4, valeur)
3) Déclarer C (itérateur) C = A à init
4) Déclarer R (résultat) R = 0
5) si C >= 0 on branch à *multiplication*
6) *multiplication* : 
	2) ajoute B à R
	3) retire 1 de C
7) Si C=0, branch à *fin*
8) Sinon branch à *multiplication* (loop)
9) *fin*:
	1) Préparer la systeme à print R

Ici, A et B ne doivent **pas** changer, mais R et C doivent changer, ça veux dire que les registres utilisés pour A et B ne peuvent pas être de même type

A et B doivent êtres sauvegardés, tandis que C et R doivent êtres temporaires

```MIPS
.data
.text
main: 

#s0 = A (3)
#s1 = B (4)
#t0 = resultat
#t1 = compteur

li $v0,5     #lire A
syscall
move $s0,$v0 #save A

li $v0,5     #lire B
syscall
move $s1,$v0 #save B

li $t0,0     #initialise le résultat = 0
move $t1,$s0 #initialise le compteur = A


multiplication: 
	add $t0,$t0,$s1  #j'ajoute B au result
	addi $t1,$t1, -1 #j'enlève 1 à compteur (1 step faite)

beq $t1,$zero, fin   #si on a fini on saute à fin

b multiplication # sinon bah pas fini, on multiplie

fin:
	li $v0,1  #preparer a output un int
	move $a0,t0 #met le resultat dans boite à print
	syscall
	li $v0,10
	syscall

```

---
#### Jump and Link, Return Adresse (instruction suivante)

**Exemple mathématique:**

On souhaite afficher à la fois la somme et la différence entre deux nombre, a et b avec les fonctions
$$
\begin{align*}
somme(a,b) = a+b \\
difference(a,b) = a-b \\
\end{align*}
$$

et exécuter l'affichage de somme(a,b) , affichage de somme(a,b) dans cet ordre

Soit a = 10, et b = 4

Nous savons que pour afficher les réponses correctes on doit calculer d'abord le retour des fonctions $somme(a,b)$ et $difference(a,b)$, garder en mémoire ces résultats sous $R1$ et $R2$, et ensuite afficher ces derniers. 

##### Étape 1) Arguments
On charge a et b comme arguments de fonctions (registres $ax$)
	a0 <- 10
	a1 <- 4
##### Étape 2) Somme(a,b)
on Jump And Link vers la fonction *somme*. Le jump implique qu'on mette dans $ra$ **l'instruction qu'on ferait si je savais ce que valais somme(10,6)**. Comme je ne le sais pas, je garde dans ra l'instruction "*sauvegarder le retour dans une variable temporaire*"

##### Étape 2.1) somme: 
dans *somme* j'additionne les contenu de a et b dans un registre de retour de valeur de type $vx$ et je **Jump Register à l'endroit où j'aurais continué l'exécution de la fonction englobante si j'avais les valeurs**. Cet endroit est l'adresse pointée par $ra$.   
	add v0, a, b   :   v0 <- 14
	jr $ra
Comme ra contenait l'instruction de *sauvegarder le retour dans une variable temporaire*, on le fait 

etc.

Traduction en Mips

```
.data
a: .word 10   # Premier nombre (a = 10)
b: .word 5    # Deuxième nombre (b = 5)
R1: .word 0   # Espace pour le résultat de la somme
R2: .word 0   # Espace pour le résultat de la différence

.text
main:
    
    lw $a0, a            #  a = 10 dans $a0
    lw $a1, b            #  b = 5 dans $a1

    jal sum  
    move $t0, $v0   

    jal difference  
    move $t1, $v0 

    li $v0, 10           
    syscall

sum:
    add $v0, $a0, $a1    # $v0 = $a0 + $a1
    jr $ra               # Retourner à l'appelant

difference:
    sub $v0, $a0, $a1    # $v0 = $a0 - $a1
    jr $ra               # Retourner à l'appelant
```

---

# Récursion simple en MIPS

La fonction récursive de puissance est une fonction de 2 cas ; le cas récursif (elle s'appelle elle-même) et le cas de base (une valeur connue)

En général, on a 5 étapes pour un code impliquant de la récursion (excluant la fin)

1) Entrer dans la fonction (exécution du main)
2) Vérification du Cas de base
3) Jump récursif
4) Retourner à l'appelant
5) Cas de base

$$
\begin{equation}
    Puissance(b,e) =
    \begin{cases*}
	    b*Puissance(b,e-1) & si e > 0  \\
	      1        & si e = 0 \\
    \end{cases*}
  \end{equation}
$$
On récupère d'abord les paramètres de la fonction, donc b (base) et e (exposant)
Dans le main, **dès qu'on aura obtenu une valeur** on sauvegarde le résultat et on l'affiche (cette partie est après les étapes récursives)

```
.data
.text
main : 
	li a0, b
	li a1, e

	jal puissance

	move result ,a0
	li v0, 1
	move a0,result
	syscall
```

Le cas de base est une adresse particulière qui **retourne une valeur au dernier appel** si elle est vérifiée, et qui saute vers la récursion si elle n'est pas vérifiée

```
puissance:
	bne a1,zero,recursion #si pas = 0, on recurse
	li v0,1               #sinon valeur = 1
	jr ra                 # on remet ce result a l'étape 
	                      # qui aurait suivi si on avait un chiffre
```

Les étapes pré récursives consistent à allouer de l'espace pour le retour, les paramètres utiles et les modifier 

```
recursion:
	addi sp, sp -4   #laisser espace pour le retour
	sw ra,0(sp)      #stocker retour à la place réservé
	addi a1,a1,-1    #modifier le paramètre concerné
```

Le saut récursif consiste à jump à nouveau à l'étape de vérification du cas de base juste après les étapes pré récursives et garder à ra ce qu'on aurait fait si on avait déjà atteint le cas de base (qui est le calcul en lui même)

```
recursion:
	addi sp, sp -4   #
	sw ra,0(sp)      #
	addi a1,a1,-1    #
	jal cas_base     # on refait; pour next récursion
```

Dès qu'on aura atteint un premier retour de valeur (le jr suivant cas de base) on devra effectuer un calcul, qui est placé juste après le jal, puisque le ra note l'instruction qui aurait été faite si on avait une valeur pour calculer au lieu de sauter en récursion. Ca sera fait jusqu'à ce qu'on aura atteint le ra qui a stocké comme prochaine instruction "*terminer le programme*"

```
recursion:
	addi sp, sp -4  #
	sw ra,0(sp)     #
	addi a1,a1,-1   #
	jal cas_base    # on refait; pour next récursion
	
	mul v0, a0, v0  # le calcul lui meme
	lw ra, 0(sp)    # ce  quon aurait fait (frame précédent)
	addi sp, sp 4   # on vide le stack de cette instruction
	jr ra           # on y va
```

trick, avant le jal et après bah c'est la même chose, juste à l'inverse

```

.data
.text

main : 
	li a0, b
	li a1, e

	jal puissance    #sauter dans le cas de base
	move result ,a0
	li v0, 1
	move a0,result
	syscall
	
puissance:
	bne a1,zero,recursion #si pas = 0, on recurse
	li v0,1               #sinon valeur = 1
	jr ra                 # on remet ce result a l'étape 
	                      # qui aurait suivi si on avait un chiffre

recursion:
	addi sp, sp -4   #laisser espace pour le retour
	sw ra,0(sp)      #stocker le retour à l'appel antérieur
	addi a1,a1,-1    #modifier le paramètre concerné
	jal puissance    # next récursion
	
	mul v0, a0, v0  # le calcul lui meme
	lw ra, 0(sp)    # ce  quon aurait fait (frame précédent)
	addi sp, sp 4   # on vide le stack de cette instruction
	jr ra           # on va au call précédent
```

Évolution du code

| Instru                          | ra                         | a   | b   | v0 (resultat) |
| ------------------------------- | -------------------------- | --- | --- | ------------- |
| a0 = 5                          | -                          | 5   | -   | -             |
| a1 = 3                          | -                          | 5   | 3   | -             |
| jal puissance                   | -                          | 5   | 3   | -             |
| addi sp, sp -4                  | **imprimer**               | 5   | 3   | -             |
| ==sw ra,0(sp)==                 | imprimer                   | 5   | 3   | -             |
| addi a1,a1,-1                   | imprimer                   | 5   | 3   | -             |
| jal puissance                   | imprimer                   | 5   | 2   | -             |
| ~~bne a1,zero,recursion~~       | **mul v0, a0, v0**         | 5   | 2   | -             |
| addi sp, sp -4                  | mul v0, a0, v0             | 5   | 2   | -             |
| ==sw ra,0(sp)==                 | mul v0, a0, v0             | 5   | 2   | -             |
| addi a1,a1,-1                   | mul v0, a0, v0             | 5   | 2   | -             |
| jal puissance                   | mul v0, a0, v0             | 5   | 1   | -             |
| ~~bne a1,zero,recursion~~       | **mul v0, a0, v0**         | 5   | 1   | -             |
| addi sp, sp -4                  | mul v0, a0, v0             | 5   | 1   | -             |
| ==sw ra,0(sp)==                 | mul v0, a0, v0             | 5   | 1   | -             |
| addi a1,a1,-1                   | mul v0, a0, v0             | 5   | 1   | -             |
| jal puissance                   | mul v0, a0, v0             | 5   | 0   | -             |
| ==***bne a1,zero,recursion***== | **mul v0, a0, v0**         | 5   | 0   | -             |
| jr ra                           | mul v0, a0, v0             | 5   | 0   | 1             |
| mul v0, a0, v0                  | mul v0, a0, v0             | 5   | 0   | **5**         |
| lw ra, 0(sp)                    | mul v0, a0, v0             | 5   | 0   | **5**         |
| addi sp, sp 4                   | ==mul v0, a0, v0 # 3==     | 5   | 0   | **5**         |
| jr ra                           | ==mul v0, a0, v0 # 3==     | 5   | 0   | **5**         |
| ==mul v0, a0, v0 # 3==          | ==mul v0, a0, v0 # 3==     | 5   | 0   | **5**         |
| lw ra, 0(sp)                    | ==mul v0, a0, v0 # 3==     | 5   | 0   | **25**        |
| addi sp, sp 4                   | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | **25**        |
| jr ra                           | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | **25**        |
| ==mul v0, a0, v0 # 2==          | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | **25**        |
| lw ra, 0(sp)                    | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | 125           |
| addi sp, sp 4                   | ==imprimer # 1==           | 5   | 0   | 125           |
| jr ra                           | ==imprimer # 1==           | 5   | 0   | 125           |
| ==imprimer # 1==                | FIN                        |     |     |               |

| STACK                  |
| ---------------------- |
| ==imprimer # 1==       |
| ==mul v0, a0, v0 # 2== |
| ==mul v0, a0, v0 # 3== |

---
Exemple somme des chiffres

$$
\begin{equation}
    sommeChiffres(n) =
    \begin{cases*}
	    (n mod 10)+sommeChiffres(n // 10) & si n > 0  \\
	      0        & si n = 0 \\
    \end{cases*}
  \end{equation}
$$

```
.data
number: .word 123  #nombre de 4byte
result: .word 0   #la variable de résultat

.text
.globl main

main:
    lw $a0, number  #load param de fonction a0 (123)
    jal base        #vérif du cas de base
    sw $v0, result  #si on a atteint la fin des retours, on remplit le result
    move $a0, $v0
    li $v0, 1
    syscall
    li $v0, 10
    syscall

base:
    beq $a0, $zero, base_case #si est le cas de base, branch
    li $t0, 10                #sinon load 10 (le diviseur)
    div $a0, $t0              #diviser par 10
    mfhi $v1                  #recup l'entier
    mflo $t2                  #recup le modulo
    addi $sp, $sp, -8         #laisser de l espace pour 2 infos:
    sw $ra, 0($sp)            #stocker le retour
    sw $v1, 4($sp)            #stocker le modulo
    move $a0, $t2             #mettre l'entier comme nouveau param
    jal base                  #recurison: verif cas de base encore
    lw $v1, 4($sp)            #post-base: load le modulo
    lw $ra, 0($sp)            #post-base: load le précédent retour
    addi $sp, $sp, 8          # ... : vider le stack
    add $v0, $v0, $v1         # ... : add le modulo à result 
    jr $ra                    # add le prochain modulo au result en jump

base_case:
    li $v0, 0                #premiere valeur concrète
    jr $ra

```



Instruction R TYPE:

OP RS RT RD SHAMT FUNCT
6    5   5   5    5           6

==Exo : traduire add $t0, $s4, $s5 en langage machine==

OP RS    RT    RD   SHAMT FUNCT
0    $s4  $s5   $T0  0           32 


op et funct => 0, 32 car c'est **add** en **R type**
s4 = 20 ième registre
s5 = 21 ième registre
t0 = 8 ième registre
 
0000:00,10:100,1:0101,:0100:0,000:0010:0000 =  (0x 02954020)
J TYPE = JUMP
I TYPE = IMMEDIATE

---

# Microarchitecture

#### Half adder

| A   | B   | Sum | Carry | A+B = (C:S)   |
| --- | --- | --- | ----- | ------------- |
| 0   | 0   | 0   | 0     | 0+0 = 0:0     |
| 0   | 1   | 1   | 0     | 0+1 = 0:1     |
| 1   | 0   | 1   | 0     | 1+0 = 0:1     |
| 1   | 1   | 0   | **1** | 1+1 = **1**:0 |

S = A xor B
C = A and B

#### Full adder : prend un carry précédent

| A   | B   | Carry IN | Sum | Carry OUT | A+B +Cin = (A+B) + C = (COUT:S) |
| --- | --- | -------- | --- | --------- | ------------------------------- |
| 0   | 0   | 0        | 0   | 0         | (0+0) 0:0 +0 = 0:0              |
| 0   | 0   | 1        | 1   | 0         | (0+0) 0:0 +1 = 0:1              |
| 0   | 1   | 0        | 1   | 0         | (0+1) 0:1 +0 = 0:1              |
| 0   | 1   | 1        | 0   | 1         | (0+1) 0:1 +1 = 1:0              |
| 1   | 0   | 0        | 1   | 0         | (1+0) 0:1 +0 = 0:1              |
| 1   | 0   | 1        | 0   | 1         | (1+0) 0:1 +1 = 1:0              |
| 1   | 1   | 0        | 0   | 1         | (1+1) 1:0 +0 = 0:1              |
| 1   | 1   | 1        | 1   | 1         | (1+1) 1:0 +1 = 1:1              |

S = A xor B xor C
C = AB or  and B

![[half-fullAdder 1.jpg]]

---
#### Ripple Adder (carry par cascade)

Un adder constitué de **half-adders** en série dont le carry est **propagé** tout le long du calcul

 >[!NOTE]
 >Attention le temps d'obtention de la réponse dépendra du délai causé par la propagation du carry

==Attention: le temps de propagation est ==


S = A xor B xor Cin
C = AB or C(A xor B)

![[rippleAdder.jpg]]

---
#### Look Ahead Adder (carry séquentiel)

Le but est de **ne pas propager un carry**, mais de le calculer séquentiellement **sans attendre un carry précédent**

- Au niveau du AB, le signal est $G_0$
- Au niveau du A xor B, le signal est $P_0$
- Au niveau du Ci(A xor B) le signal est $P_0C_0$

Donc le carry out qui sortira sera calculé comme étant $C_1$ = $P_0C_0$+$G_0$ et au niveau de la somme, le signal est $P_0$ xor $C_0$

C'est le cas de base pour le carry, 
	$C_1$ = $P_0C_0$+$G_0$,

donc pour $C_2$ on peut assumer que c'est 
	$C_2$ = $P_1C_1$+$G_1$

Or on sait déjà c'est quoi $C_1$ et c'est ** $P_0C_0$+$G_0$ **
- donc $C_2$ = $P_1$($P_0C_0$+$G_0$)+$G_1$
- donc $C_3$ = $P_2$($P_1$($P_0C_0$+$G_0$)+$G_1$)+$G_2$

Autrement on pourrait dire que
 - $C_2$ = $P_1$$P_0C_0$+$P_1$$G_0$+$G_1$
- $C_3$ = $P_2P_1P_0C_0+P_2P_1G_0+P_2G_1 + G_2$

On va avoir une forme du style (récursive) $$C_n = P_{n-1}(P_{n-2}...(P_0C_0+G_0)+G_1)+G_n$$
Ou autrement (séquentielle)
$$Cn = (P_{n-1}P_{n-2}...P_0C_0) + (P_{n-1}P_{n-2}...P_1G_0) + (P_{n-1}P_{n-2}...P_2G_1) + ... +(P{n-1}G_{n-2}+G_{n-1})$$

*ex* $C_4$ :
$$C4 = P_3P_2P_1P_0C_0 +  P_3P_2P_1G_0 + P_3P_2G1 + P_3G_2 +G_3$$

Ca va contenir log2N étages 
Flemme de faire le circuit, mais c'est ca le look-ahead

---
#### Full substractor

bah c'est un full adder avec le B en not

### ALU
---
Arithmetic Logic Unit, c'est le composant qui contient tout les types d'opérations qu'on peut faire, c'est un multiplexeur avancé d'opérations dont l'aiguillage est contrôlé par le opcode

| F2:0 | FONCTION |
| ---- | -------- |
| 000  | A and B  |
| 001  | A or B   |
| 010  | A + B    |
| 011  | -        |
| 100  | A and NB |
| 101  | A or NB  |
| 110  | A - B    |
| 111  | SLT      |

![[alucase000.jpg]]

1) Comme $F_2$ = 0, on sélectionne B
2) Les opérations *disponibles* sont $A \wedge B, A \vee B, A+B$
3) Comme $F_{1:0}$ = 00, l'opération sélectionnée est $A \wedge B$


![[alucase101.jpg]]

1) Comme $F_2$ = 1, on sélectionne $\overline B$
2) Les opérations *disponibles* sont $A \wedge \overline B, A \vee  \overline B, A+ \overline B$ 
3) Comme $F_{1:0}$ = 01, l'opération sélectionnée est $A \vee \overline B$

---
# CPU Single Cycle

Soit la convention que A -> RD = Adresse -> ReadData et WD = WriteData

La première étape est de créer les state éléments soit 
- **control unit:**
	- ==Décodeur==, il décode le opcode, chaque bit sert à expliquer ce a quoi consiste l'instruction (ex. jump ou non? écriture mémoire ou non?) en signaux de de control des MUX, activant un signal pour chaque bit à 1
- **program counter**
	- lit ==l'adresse== (32 b) de la prochaine instruction et la sort sur 32b vers le A du instruction memory
- **instruction memory**
	- ayant obtenu l'adresse du *program counter* sur 32b dans A, il lit et envoie le ==contenu de cette adresse sur 32b vers les registres utilisées du **register file**== (l'instruction elle-même)
- **register file**
	- l'instruction lue du instruction memory contient les adresses des **registres** utilisés sur 5 bits (de 1 à 3 registres utilisés pour une instruction). 5 bits donne un max de 32 registres.
	- On peux avoir jusqu'à 2 adresses de registres opérants (A1, A2) et 1 adresse de registre d'écriture (A3). 
	- A1 à en sortie le contenu du registre opérant 1 sur 32b  (RD1), A2 à en sortie le contenu du registre opérant 2 sur 32b (RD2)
	- En écriture on 1 port d'écriture sur 32b (WD3), 1 adresse destination sur 5 bits pour écrire (A3) et un *enable* (WE3). **Si le signal enable = 1, on écrit le contenu de la donnée WD sur A3 (RegWrite)**
- **data memory**
	- Si le signal WE est à 1, on écrit la data contenue à WD sur 32b vers l'adresse (en général dans la mémoire) A sur 32b (**MemWrite**), sinon La mémoire **lit** la donnée située à l’adresse A et l’envoie sur la sortie **RD** (**MemRead**)

#### OPCODE MAP

Alors on va first vérifier si c'est du type R (REG) ou non, car sinon on focus sur **funct**, ensuite on va grouper par trio les bits pour former l'opération. C'est un énorme **décodeur** de signaux

|     | 000  | 001   | 010  | 011  | 100  | 101 | 110  | 111  |
| --- | ---- | ----- | ---- | ---- | ---- | --- | ---- | ---- |
| 000 | REG  |       | j    | jal  | beq  | bne | blez | bgtz |
| 001 | addi | aadiu | slti | slti | andi | ori | xori |      |
| 010 |      |       |      |      |      |     |      |      |
| 011 | llo  | lhi   | trap |      |      |     |      |      |
| 100 | lb   | lh    |      | lw   | lbu  | lhu |      |      |
| 101 | sb   | sh    |      | sw   |      |     |      |      |
| 110 |      |       |      |      |      |     |      |      |
| 111 |      |       |      |      |      |     |      |      |

CAS REG : FUNCT

|     | 000  | 001   | 010  | 011  | 100  | 101 | 110  | 111  |
| --- | ---- | ----- | ---- | ---- | ---- | --- | ---- | ---- |
| 000 | sll  |       | srl  | sra  | sllv |     | srlv | srav |
| 001 | jr   | jalr  |      |      |      |     |      |      |
| 010 | mfhi | mthi  | mflo | mtlo |      |     |      |      |
| 011 | mult | multu | div  | divu |      |     |      |      |
| 100 | add  | addu  | sub  | subu | and  | or  | xor  | nor  |
| 101 |      |       | slt  | sltu |      |     |      |      |
| 110 |      |       |      |      |      |     |      |      |
| 111 |      |       |      |      |      |     |      |      |

La map de funct est simplement le décodeur du control de l'ALU

![[baseDatapath 1.jpg]]

---
#### Signaux de base (Control Unit)

>[!NOTE]
>==RegDst==, un signal pour **choisir** dans un MUX si le paramètre 2 de l'instruction
> - est à lire ou
> - est à écrire

>[!NOTE]
>==ALUSrc==, un signal pour **choisir** dans un MUX connectant l'immediate offset et le Read Data pour avoir comme param # 2 dans l'ALU
>- le contenu du registre # 2
>- l'immediate offset 
>

>[!NOTE]
>==ALUop==, un signal donnant le calcul à effectuer dans l'ALU qui *==override funct==* dans les commandes de type I et J
>

>[!NOTE]
>==MemRead==, un signal permettant de **lire le contenu du résultat** calculé par l'ALU (le résultat est une adresse)

>[!NOTE]
>==MemWrite==, un signal permettant d'écrire en **mémoire** le contenu du **paramètre 2** (pas une adresse) **dans une adresse calculée par l'ALU**
>

>[!NOTE]
>==RegWrite==, un signal permettant d'écrire dans un **registre** le contenu du **WRITEDATA** dans le paramètre **REGWRITE** 

>[!NOTE]
 ==PCsrc==, un signal provenant du **OR logique entre le flag zéro de l'ALU et du signal Branch** du Control Unit servant à choisir dans un MUX entre 2 adder pour que 
>- Le nouveau PC soit celui seulement incrémenté de 4 (adder simple) OU
>- Le nouveau PC soit celui additionné du immédiat multiplié par 4 ( adder simple + left shift : 2) 

---
#### Cycle d'instruction de type R

==l'instruction de type R ==
`add $s4, $t1, $t2 ` donne 

| opcode (R) | rs    | rt    | rd    | shamt | funct  |
| ---------- | ----- | ----- | ----- | ----- | ------ |
| 000000     | 01001 | 01010 | 10100 | 00000 | 100000 |

Donc dans instruction memory on a en sortie l'instruction "00000001001010101010000000100000". 

D'après le opcode l'instruction ==**n'est pas liée à la mémoire (b 31)**==, c'est une ==particularité des instructions de type R== car on n'aura besoin d'**aucun** **signal de contrôle pour la mémoire, seulement les registres** 

Le signal **RegDst** est à 0, donc on est dans une instruction utilisant 3 paramètres, les 2 premiers lu et le dernier à écrire. *Si **RegDst** était à 1, alors on parle d'un ==premier paramètre lu et du deuxième paramètre **écrit** ==*

Après le opcode et en fonction des signaux:
- les premiers bits (25:21) 01001 vont dans READREG1
- les 5 suivants (20:16) 01010 vont dans READREG2
- les 5 après (15:11) 10100 vont dans WRITEREG

On lit le contenu des registres, on obtient 5 de t1 et 6 de t2 et *rien* de s4

On a pas besoin de shift quoi que ce soit (shamt = 0), alors on entre dans l'ALU l'instruction "add" via **funct**. Funct sert de signal "ALUop" lorsque le signal est pas utilisé par l'instruction (type R)
Dans l'ALU, on additionne le contenu de t1 et t2, soit 5 et 6, et on **envoi la réponse 11 dans Write Data**
Comme le signal ==**RegWrite** est à 1==, le contenu de WRITEDATA est écrit dans **WRITEREG**, qui est le registre s4, qui contiendra 11

![[addDatapath_2.jpg]]

---
#### Cycle d'instruction de type I : Load Word

l'instruction de type I (immédiate) de 
`lw t0, -4(sp)` se lit :

| opcode (I) | rs    | rt    | address             |
| ---------- | ----- | ----- | ------------------- |
| 100011     | 11101 | 01000 | 1111 1111 1111 1100 |

Donc dans instruction memory on a en sortie RD l'instruction "10001111101010001111111111111100". 

Pour ce genre d'instruction on **additionne** au  READDATA1 le **==offset==** contenu dans le paramètre **address**, on accède le contenu via la mémoire et on write ce contenu dans le registre target du WRITEREG

D'après le opcode l'instruction implique la **mémoire**

Après le op code:
- les 5 premiers bits (25:21) vont dans A1
- les 5 suivants (20:16) vont dans A2

Le chemin des 16 restants sont gérés par un MUX au niveau de l'ALU et **le signal de contrôle ALUsrc**; dans le cas "0" du signal (R type) l'ALU choisirai comme entrée # 2 le READDATA2, mais dans le cas "1", l'ALU prendrait les 16 bits des instructions immédiates (passant par un extenseur de signe pour remplir les bits jusqu'à 32 bits)

L'ALU additionne l'offset avec le contenu du premier paramètre (RD1). On obtiens l'adresse, et comme le signal MemRead est actif, cette adresse se retrouve dans **Read Data**.

Le résultat de l'ALU, qui est une **adresse** et non une valeur, implique qu'on mette une valeur contenue à l'adresse calculée puis l'écrire dans le registre cible en paramètre.


![[lwdatapath.jpg]]

>==Attention: t0 est aussi dans A2, mais n'est pas utilisé pour fournir le data du paramètre 2 de l'ALU==

---
#### Cycle d'instruction de type I : Store word

l'instruction de type I (immédiate) de sw t0, 2(sp) se lit :

| opcode (I) | rs    | rt    | address             |
| ---------- | ----- | ----- | ------------------- |
| 101011     | 11101 | 01000 | 0000 0000 0000 0010 |

Donc dans instruction memory on a en sortie RD l'instruction machine "10101111101010000000000000000010".

D'après le opcode l'instruction implique la **mémoire**

Après le op code:
- les 5 premiers bits (25:21) vont dans A1
- les 5 suivants (20:16) vont dans A2

Le chemin des 16 restants sont gérés par  **le signal de contrôle ALUsrc**; l'ALU prend dans une des entrées **les 16 bits des instructions immédiates** (passant par un extenseur de signe pour remplir les bits jusqu'à 32 bits).

Le **RD1 contient l'adresse pointée par s0**, 269500992, et le **RD2 contient la char à stocker**, "A". Nous mettons un **bus de 32b direct entre RD2 et WD** puisque c'est cette data qu'on souhaite écrire dans le paramètre adresse A du *Memory Unit* dans le cas ou le signal MemWrite est actif

L'ALU additionne l'offset avec le contenu du premier paramètre (RD1). On obtiens l'adresse où stocker "A", et comme le signal **MemWrite est actif**, le contenu de WD est écrit à cette nouvelle adresse. 

>Il n'y a plus rien à faire après, les signaux ==MemToReg et RegWrite sont dont care==


![[swdatapath_2 1.jpg]]

---
#### Cycle d'instruction de type I : branchement

Soit le code MIPS suivant :

```
	beq $at, $0, Label 
	add $v1, $v0, $0         #start
	add $v1, $v1, $v1        #+4         
	j Somewhere              #+8
Label:  add $v1, $v0, $v0    #+12
```

l'instruction Branch, de format I contient le offset entre l'adresse de l'instruction **suivant le Branch (PC+4)** et l'adresse de l'instruction du label 

>Même si on "*recule*" dans le Branch, on part du PC+4

| opcode (R) | rs    | rt    | address             |
| ---------- | ----- | ----- | ------------------- |
| 000100     | 00001 | 00000 | 0000 0000 0000 0011 |
donc le offset est de **3**, car pour aller de `add $v1, $v0, $0` jusqu'à `L:  add $v1, $v0, $v0` il y a 3 "ligne/adresses". 

En passant par le left shift, on aura multiplié par 4 le nombre d'adresses a sauter

On aura comme registres at et zéro pour la condition, comme on vérifie l'**égalité** on vérifiera cette condition si leur **soustraction donne 0**.

Au niveau de l'ALU, le signal ALUOP est celui du SUB, si c'est un 0 le flag 0 enverra un "1", qui rejoindra le signal Branch pour former le signal PCsrc


![[beq.jpg]]

---
### Cycle d'instruction de type j : jump

| opcode (J) | address (26)                     |
| ---------- | -------------------------------- |
| 000100     | 00 0000 0000 0000 1100 0000 0100 |

Les jumps sont assez direct, il n'y a pas de condition pour jump; **pas besoin de l'ALU pour le jump classique**, seul le signal *Jump* est utilisé

Comme le jump doit être une une adresse, ==il faut qu'elle soit sur 32 bits, mais elle n'a que **26** bits.==

#### Datapath J

>[!NOTE]
>Pour avoir le bon format on doit
>
>1) Left shift de 2 pour avoir un offset d'adresse sur 28 bits (27:0)
>2) Calculer PC+4
>3) **Concaténer** les bits (31:28) du PC+4 pour avoir une instruction complète sur 32 bits

**Étape 1 **
- PC ($0x00100008_{hex}$) passe par adder de 4 pour obtenir PC+4 ($0x0010000C_{hex}$) ET 
- Offset de 26 bits **entre dans le SHIFTLEFT**; *C'est sûr que le register unit se remplira des paramètres de base, mais il n'y a aucun signal qui permet de travailler avec, donc on n'en fera rien*
**Étape 2**
- les 4 premiers bits de PC+4 ($0000$) rejoignent les 28 bits du offset étendu $0x0100008_{hex}$ , on a là une instruction sur 32 bits (rajoute un 0 devant en hexadécimal).
- Donc on aura $0x00100008_{hex}$ comme adresse de jump
**Étape 3**
- un MUX permet un choix entre: 
	- le jump adresse qu'on vient de créer via concaténation OU 
	- le résultat du MUX utilisé pour choisir entre PC+4 (adresse suivante normale) ou une adresse calculée (branchement)

![[datapathJump.jpg]]

---
# CPU Multi Cycle

Le problème du cycle singulier est qu'il faut que toute l'opération se fasse sur **1 seul cycle**, a chaque fois qu'on add une opération il faudra ==allonger== le cycle pour qu'il soit de la ==**longueur de l'opération la plus longue**==.

Le multicycle implique qu'on découpe l'instruction en plusieurs étapes, des cycles très courts

Un cycle de CPU consiste en maximum 5 étapes

| Étape         | C'que ca fait                                                           |
| ------------- | ----------------------------------------------------------------------- |
| Fetch         | Lire PC depuis la mémoire d'instruction et add 4 (préparer PC+4)        |
| Decode        | Lire les registres utilisés dans l'instruction, étendre le offset si là |
| Execution     | Calculer                                                                |
| Memory access | Lire ou écrire la mémoire                                               |
| Write Back    | Écrire le résultat dans le registre cible (si)                          |

exemples :

| Instruction               | Étapes                                         | Nbr      |
| ------------------------- | ---------------------------------------------- | -------- |
| **`add $t0, $t1, $t2`**   | IF → ID → EX → WB                              | 4 cycles |
| **`lw $t0, 4($t1)`**      | IF → ID → EX → MEM → WB                        | 5 cycles |
| **`beq $t0, $t1, Label`** | IF → ID → EX → Branch Decision (PC Update)<br> | 4 cycles |
| **`j Label`**             | IF → Jump Decision                             | 2 cycles |

#### Cycle 1 : Fetch

L'instruction est récupéré de PC, le signal IorD est à "0", donc on prend une instruction.
Cette instruction va dans le MAR (Memory Adresse Register) et on récupère l'instruction sur 32 bits
Cette instruction va dans le Instruction Register, avec les bits 
- 31:26 -> OP
- 25:21 -> Field 1
- 20:16 -> Field 2
- 15:0   -> (plus tard...)

>**Ces données vont nul part au cycle 1, on les garde dans le IR**

En même temps le PC est envoyé dans un mux ayant le signal ALUsrcA à 0 (ce n'est pas A qu'on prend) et donc le PC se retrouve automatiquement dans l'ALU comme paramètre 1. Le paramètre 2 est la constante 4 obtenue par le multiplexeur de la source B dont le signal est mit à "01".
L'ALUOP au cycle 1 est toujours à ADD, on additionne alors le PC (param 1) et la constante 4 (param 2). Le résultat est envoyé dans le MUX géré par PCsrc. Ce signal choisi d'envoyer un PC' provenant 
- soit de l'addition PC+4
- soit d'un résultat de ALUOUT
- soit de l'offset d'un jump (26 bits - significatifs) étendu (32 bits)

Ici PCsrc est à "00", donc notre prochaines instruction est bien PC+4

#### Cycle 2 : Instruction Decode

Les données figurant dans les bus de paramètres RS et RT contenues dans le instruction register sont **sauvegardées** dans le register unit pour les utiliser plus tard dans le cycle 3, donc

- 31:26 -> OPCODE
- 25:21 -> Field 1 (rs) -> Read Reg 1 -> A
- 20:16 -> Field 2 (rt) -> Read Reg 2 -> B

>**Peu importe ce qu'est l'opcode, on va calculer une adresse de branchement**, ca veux dire qu'on *aura en signal ALUsrcA "00" (on prend pas le contenu du registre rs) et en ALUsrcB "11" (on prend une adresse immédiate)*

- PC ->*==ALUsrcA = 0==*  -> ***ALU***
- 15:0 -> sign extend (32bits) -> shift 2 ( x4 oct) -> *==ALUsrcB* = "11"== -> ***ALU***

L'ALUOP est donc **add** puisqu'on prépare un **potentiel** branchement, on les add et on les stock dans ALUOUT.

Le signal *ALUout* est à 0, on envoie l'adresse de branchement "**optimistie**" directement dans le MUX des PCsrc (option "00")
#### Cycle 3 : Execute

Là qu'on a décodé l'opcode et on sait qu'on peut faire des opérations de 
- type R
- Type I
- Type J

##### a) Si on doit faire une op de type R  
1) On va pop A et B comme paramètres de l'alu, L'ALUop est mit par exemple à **add** et on calcule
2) Le signal ALUout est à "1"; on sauvegarde dans le registre temporaire ALUout par la réponse calculée
3) Le contenu est directement envoyé dans le MUX géré par MemToReg, le signal MemToReg est à 1, donc c'est le contenu de l'ALUout qui est passé comme data à écrire

##### a) Si on doit faire une op de type I
1) On va pop A dans comme paramètre # 1 dans l'ALU
2) CAS LW/SW:  On met comme paramètre # 2 dans l'ALU le offset immédiat  étendu sur 32 bits
#### Cycle 4 : Memory
##### a) Si on doit faire une op de type I

Le contenu de l'ALUout est envoyé au mux géré par IorD et comme ce contenu provient de ALUout, le signal est donc mit à 1, il part dans Memory Unit
#### Cycle 5 : Write Back


---
### JAL Multicycle

