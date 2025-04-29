
```library IEEE;
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


<div style="page-break-after: always;"></div>



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