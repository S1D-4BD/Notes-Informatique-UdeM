```vhdl

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity fsm_moore is
    Port (
        clk : in  STD_LOGIC;  -- Clock
        reset: in  STD_LOGIC;  -- Reset
        m5: in  STD_LOGIC;  -- 5 cents (la switch completement a droite)
        m10: in  STD_LOGIC;  -- 10 cents
        m25: in  STD_LOGIC;  -- 25 cents (la switch completement a gauche)
        segment_somme: out STD_LOGIC_VECTOR(15 downto 0); -- 16 bits 
        segment_reste: out STD_LOGIC_VECTOR(15 downto 0); -- 16 
        distribuer: out STD_LOGIC -- led pr debug le cas sup. à 25
		  
    );
end fsm_moore;

architecture synth of fsm_moore is

    
    signal somme: STD_LOGIC_VECTOR(3 downto 0); -- 4 bits pour la somme (la plus groosse somme quon peut faire c'est 45)
    signal resteRemis: STD_LOGIC_VECTOR(2 downto 0); -- 3 bits pour la monnaie rendue (le plus de monnaie quon remet c'Est 20)

begin
    
    fsm_controller_inst : entity work.controller
        port map (
            clk => clk,
            reset => reset,
            in5 => m5,        			-- je mets 5 cents
            in10 => m10,       			-- je mets 10 cents
            in25 => m25,       			-- je mets 25 cents
            somme => somme,-- Bus somme  (va dans les 2 premiers afficheur)
            reste => resteRemis,
             -- Bus  DE monnaie a rendre (va ds les 2 derniers afficheurs)
            distribuer => distribuer 
            -- Signal pour moi (a chaque 25 et + ca va s'allumer)
        );

    afficheur_somme : entity work.segment_controller 
     --donc les switches vont dans le bus de somme monnaie 
        port map (                                             
           --(!!! la switch des 20 cents marche pas ca existe pas, 
            SW3 => somme(3), 											
-- mais on doit etre capable d'afficher 20 cents si jamais on fait 10 +10)
            SW2 => somme(2),
            SW1 => somme(1),
            SW0 => somme(0),
            segment => segment_somme   --  pour afficher la somme
        );

  
    afficheur_monnaie : entity work.segment_controller --la on va instancier mon segment controller 
        port map (
            SW3  => '0',                   	 -- Pas de pièce de 25 cents a remettre (on a anyways pas d'etat 50 cents on va jamais l'afficher)
            SW2  => resteRemis(2),        	-- pour afficher 20 cents
            SW1  => resteRemis(1),        	-- pour afficher 10 cens
            SW0  => resteRemis(0),        	-- pour 5 cents
            segment => segment_reste           -- pour afficher le reste
        );

end synth;

```

```vhdl

--controller

--Celina Sid Abdelkader, 2024-10-22
--IFT1227

--Machine a bonbons, fsm de Moore à 10 etats et affichage sur 4  7-segments (2 pour le reste, 2 pour la somme)


library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity controller is
	Port (
		clk : in  STD_LOGIC;   		-- Clock 
      reset : in  STD_LOGIC;   	-- Reset 
      in5  : in  STD_LOGIC;   	-- swt 5 cents
      in10 : in  STD_LOGIC;   -- swt 10 cents
      in25 : in  STD_LOGIC;   -- swt 25 cents (bit le plus significatif dans le input
      somme: out STD_LOGIC_VECTOR(3 downto 0); --le bus pour afficher le total (max 45c)
      reste: out STD_LOGIC_VECTOR(2 downto 0); -- bus pr afficher ce quil faut remettre (max20c)
      distribuer: out STD_LOGIC 						-- pour moi, debug à > 25
    );
end controller;

architecture synth of controller is

    -- les etats = toutes les sommes possibles
    type state_type is (etat0, etat5, etat10, etat15, etat20, etat25, etat30, etat35, etat40, etat45);
    signal state, next_state : state_type;

begin
    ---------------
    -- transition-- 
    process(clk, reset)
    begin
        if reset = '1' then
            state <= etat0; 
        elsif rising_edge(clk) then -- ma clock est une switch, qd la switch est a 1 le d-flip flop laissera passer l'input D du rising edge vers Q (next state)
            state <= next_state; 
        end if;
    end process;

    -----------------------------------------------------------------------------------------------------------------------
    -- Processus transition:  en fct des 3 pieces qu'on peut mettre et l'etat ou on est, on va ou et qu'est ce qu'on affiche
	 --des quon a distribué un bonbon, peu importe l'input qui suit on reset 
    process(state, in5, in10, in25)
    begin
        -- 
        somme <= "0000";  
        reste <= "000"; 
        distribuer <= '0'; 

        -----------------------------------
		  --case des etats + OUTPUT sur 7 seg
        case state is
            when etat0 => -- etat initial, 0 c lus
                if in5 = '1' then
                    next_state <= etat5;
						  
                elsif in10 = '1' then
                    next_state <= etat10;
						  
                elsif in25 = '1' then
                    next_state <= etat25;
						  
                else
                    next_state <= etat0;
                end if;
					 
                somme <= "0000"; -- affiche 00

            when etat5 => 
                if in5 = '1' then
                    next_state <= etat10;
						  
                elsif in10 = '1' then
                    next_state <= etat15;
						  
                elsif in25 = '1' then
                    next_state <= etat30;
                    
						  
                else
                    next_state <= etat5;
						  
                end if;
                somme <= "0001"; 

            when etat10 => 
                if in5 = '1' then
                    next_state <= etat15;
                elsif in10 = '1' then
                    next_state <= etat20;
                elsif in25 = '1' then
                    next_state <= etat35;
                    
                else
                    next_state <= etat10;
                end if;
                somme <= "0010"; 

            when etat15 =>
                if in5 = '1' then
                    next_state <= etat20;
						  
                elsif in10 = '1' then
                    next_state <= etat25;
						  
                elsif in25 = '1' then
                    next_state <= etat40;
                    
                else
                    next_state <= etat15;
						  
                end if;
                somme <= "0011";

            when etat20 => 
                if in5 = '1' then
                    next_state <= etat25;
                    
						  
                elsif in10 = '1' then
                    next_state <= etat30;
                  
						  
                elsif in25 = '1' then
                    next_state <= etat45;
               
						  
                else
                    next_state <= etat20;
                end if;
                somme <= "0100"; 
					 
					--A partir d ici, on retourne directement à l'état 0, peu importe l'input (d ailleur je traite pas ca j'y vais directement)

            when etat25 => 
                distribuer <= '1'; -- bonbon 
                next_state <= etat0;
					 
                somme <= "1000"; 
					 reste <= "000";
					  -- OUTPUT: 00 25

            when etat30 => 
                distribuer <= '1'; 
                reste <= "001"; 
                next_state <= etat0;
                somme <= "1001"; 
					 
					  -- OUTPUT: 05 30

            when etat35 => 
                distribuer <= '1'; 
                reste <= "010";
                next_state <= etat0;
                somme <= "1010"; 
					 
					  -- OUTPUT: 10 35

            when etat40 => 
                distribuer <= '1'; 
                reste <= "011"; 
                next_state <= etat0;
                somme <= "1011"; 
					 
					 -- OUTPUT: 15 40

            when etat45 => 
                distribuer <= '1'; 
                reste <= "100";
                next_state <= etat0;
                somme <= "1100"; 
					 
					 -- OUTPUT: 20 45

            when others =>
                next_state <= etat0;
                somme <= "0000"; 
					 reste <= "000"; 

        end case;
    end process;

end synth;
```


```vhdl

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity segment_controller is
    Port ( 
        SW3 : in STD_LOGIC;   
        SW2 : in STD_LOGIC;   
        SW1 : in STD_LOGIC;   
        SW0 : in STD_LOGIC;   
        segment : out STD_LOGIC_VECTOR(15 downto 0)
    );
end segment_controller;

architecture synth of segment_controller is
    signal monbus : STD_LOGIC_VECTOR(3 downto 0);  --bus parce que quartus accepte pas de concatener avec &
begin
    process(SW3, SW2, SW1, SW0)
    begin
        monbus <= SW3 & SW2 & SW1 & SW0;  
        segment <= "1100000011000000";  
		  

        case monbus is  
            when "0000" => segment <= "1100000011000000"; --00
            when "0001" => segment <= "1100000010010010"; --05
            when "0010" => segment <= "1111100111000000"; --10
            when "0011" => segment <= "1111100110010010"; --15
            when "0100" => segment <= "1010010011000000"; --20
            when "1000" => segment <= "1010010010010010"; --25
            when "1001" => segment <= "1011000011000000"; --30
            when "1010" => segment <= "1011000010010010"; --35
            when "1011" => segment <= "1001100111000000"; --40
            when "1100" => segment <= "1001100110010010"; --45
            when others => segment <= "1100000011000000"; --TT LE RESTE, 00
        end case;
    end process;
end synth;

```