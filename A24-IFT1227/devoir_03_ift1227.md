
---
```VHDL

#Ce programme lit un texte utilisateur, segmente le texte en mots, 
#trie ces mots, et les affiche formatés ligne par ligne avec un maximum de 4 mots par ligne.
#Il gère également la validation des caractères et la détection des erreurs, 
#comme les dépassements de taille de tampon.

#Devoir fait par :

#Celina Sid Abdelkader	(20279666)
#Ayman Kaissi		    (20253368)
#Farah Romdhane		    (20288662)
#26 Novembre 2024
.data
# Tampon pour le texte
texte: .space 300      #300 octets pour le texte qu'on va
           
tabMots: .space 1200   #1200 octets pour le tableau de mots         [a,c,b,d,...... 1200 caractere  ]

# Message de prompt)
msg: .asciiz "Entrez un texte :"

msgInvalidInput: .asciiz "\nErreur: Tampon plein \n"

result_msg: .asciiz "Nombre de caractere est :  "
msgRetour:	.asciiz "\nVoici le tableau des mots avant tri:\n"

msgTrie:    .asciiz "\nTableau des mots apres tri :\n"



	
# Segment contenant le code
.text

 main: 
 
   # afficher msg 
   li $v0 , 4 
   la $a0 ,msg 
   syscall 
   
   jal saisir 
   jal compter 
   
      # On va verif le resultat
   bgez $v0, afficher_resultat    # si $v0 >= 0, afficher nbr char + espace
   beq $v0, -1 , afficher_erreur
   
  afficher_resultat:
      li $v0, 4
      la $a0, result_msg
      syscall
   
      addi $t1,$t1,-1
      add $a0, $t1 ,$zero # load le rsultat dans $a0
      li $v0, 1           # Syscall pour afficher un int
      syscall
              #retour pour commencer sur une nouvelle lign
      addi    $a0, $0, 10     # ASCII de '\n'
      li      $v0, 11
      syscall
      
      ###li $v0, 4
      la $a0, msgRetour    # imprime tableau de mot non-trier 
      li $v0, 4
      syscall
     
       jal decMots           #decoupe le buffer texte
     
    	move	$a0, $v0
    	move	$a1, $v1
    	move	$s6, $v0
    	move	$s7, $v1
    	
    	la $a0 , tabMots
    	move $a1 , $v1
    
    	jal afficher	#affiche le buffer 
    	li $v0, 4 
    	la $a0 , msgTrie
    	syscall 
    	jal trier 
    	la $a0, tabMots 
    	move $a1, $v1 
    	jal afficher
    	j exit 
      
  afficher_erreur:
      li $v0, 4
      la $a0, msgInvalidInput
      syscall

  exit:
      li $v0, 10
      syscall

#############################################################################
###### ROUTINE SAISIR : PERMET DE GARDER DANS TEXT UNE ENTREE UTILISATEUR ###
#############################################################################

saisir:                     
    li $v0, 8  # perparer systeme a lire 
    la $a0, texte  # Load l Adresse du texte
    li $a1, 300 # a1 = limite en taille
    syscall
    jr $ra   # Retour

compter:    # Routine extra pour compter les char (ou retour -1 si overflow)
    la $t0, texte        
    li $t1, 0               
    li $t2, 300            

count_loop:
    lb $t3, 0($t0)  # Load un octet du buffer
    beqz $t3, done    # si t3 == null arret
    addi $t1, $t1, 1   # sinon -> t1 +=1 
    addi $t0, $t0, 1   # traiter prochain octet
    blt $t1, 299 , count_loop # condition doverflow
    

overflow:

    li $v0, -1              # Retour -1
    jr $ra                  

done:
    move $v0, $t1 # garder dans v0 le compte
    jr $ra        # Retour routine
  
#################################################################
###### ROUTINE ISAPLHA : VERIFIE SI LE CHAR EST ALPHABETIQUE ####
#################################################################  
isalpha: 

    blt $a0, 0x41, not_valid # CAS < 'A'
    bgt $a0, 0x7A, not_valid # CAS > 'z'
    blt $a0, 0x5B, isvalid # ENTRE 'A' et 'Z' -> confimre majuscule
    bge $a0, 0x61, isvalid # ENTRE 'a' et 'z' -> confirme minuscule

   not_valid: 
            li $v0, 0  # pas valide
            jr $ra

   isvalid: 
           li $v0, 1 # Valide
           jr $ra
  
#################################################################
###### ROUTINE DECOTS : DECOUPE LE STRING EN MOTS VALIDES #######
#################################################################
decMots:
	##INIT##
    # a0 = addr buffer (texte), $a1 = taille texte (number of characters)
    # sortie: v0 va contenir l addresse de tabMot (array des debuts de mots)
    #        v1 contient la taille de tabMot (nbr de mots trouves dans texte)
    la    $s0, texte # pointeur de texte -> s0
    lbu   $t1, ($s0) # Load  premier char du tampon dans t1
    addi  $t2, $0, 0 # compteur de taille text
    addi  $t3, $0, 0 #  0
    addi  $t4, $0, 1 #  1
    addi  $s5, $0, 0 # compteur pour iterations 
    add   $s6, $0, $a1 # on va garder la taille du texte dans s6
    add   $s7, $0, $ra # on garde le nouveau retour d adresse
    la    $s2, tabMots # pointeur de tabMots -> s2
    addi  $s3, $0, 0 # apres la fin du traitement on add (\0)
    addi  $s4, $0, 0 # tabmot = taille 0 initialement
    
    j     processTextLoop  # Jump au traitement

processTextLoop:
    slt   $t9, $s6, $s5   # condition :on a atteint la fin du buffer?
    beq   $t9, 1, decMotsDone # CAS VRAI : fin de la loop
    addi  $a0, $t1, 0  # SINON, on va traiter le char dans isalpha
    jal   isalpha      # jump dans islapha
    addi  $s5, $s5, 1  # on incremente le compteur de loop
    beq   $v0, 1, saveWordAddress    # CAS ASCII VRAI: on le garde
    addi  $s0, $s0, 1  # sinon on va juste traiter le prochain char
    lbu   $t1, ($s0) 
    j     processTextLoop       # refaire la loop tant quon atteint pas la fin

saveWordAddress:
    sw    $s0, 0($s2) # garder addresse courante dans tabMot
    addi  $s2, $s2, 4  # traiter l index suivant dans tabMot
    addi  $s4, $s4, 1  # on incremente la taille de tabMot
    j     skipWord # on va trouver un prochain char non valide

skipWord:
    addi  $s0, $s0, 1 # on va se deplacer au prochain char dans le buffer
    lbu   $t1, ($s0) # on load ce char
    addi  $a0, $t1, 0 # on le passe en argument a isalpha
    jal   isalpha # jump
    addi  $s5, $s5, 1 # on incremente de 1 la loop 
    beq   $v0, 0, markEndOfWord # SI == 0 -> FIN DE MOT
    j     skipWord              # SINON cherche un mot non valide

markEndOfWord:
    sb    $s3, 0($s0) # on remplace le char courant par /0
    addi  $s0, $s0, 1 # on passe au prochain char
    lbu   $t1, ($s0) # load le prochain char
    j     processTextLoop # retour au traitement

decMotsDone:
    # sortie
    la    $v0, tabMots # v0 = pointeur de tabMot
    addi  $v1, $s4, -1 # v1 = taille de tabMot (nbr mots trouves)
    move $v1 ,$s4
    add   $ra, $0, $s7   # remet l'Adresse de retour au main
    jr    $ra            # on retourne

afficher:
    # init:
    #   a0 - pointeur de tabMot
    #   a1 - nbr de mots
    #
    # sortie:
    #   on va imprimer chaque mot de tabMot au I/O, 4 mots par ligne
    #   on va donc ajouter un retour "/n " apres quon ai atteint 4 mots (limite)
    #

    move    $s1, $a0  # on va copier adresse de tabMots dans  s1
    move    $t1, $a1  # on copie la taille de tabMot  dans t1
    addi    $t2, $0, 0 # compteur pour la loop = 0
    addi    $t3, $0, 0 # notre flag pour controler l'Affichage
    addi    $t4, $0, 0 # compteur pr le nbr de mots par ligne
    slt     $t3, $t2, $t1 # COMPARAISON: t2 (index) < t1 (nbr de mots)
    beq     $t3, $0, done # sil n y a plus de mots a imprimer -> fin
    j       loop1       # sinon on fait la loop

loop1:
    lw      $t9, 0($s1)# on va load laddresse du mot present dans t9
    j       decWord # on saut a decWord pour l imprimer

back:
    addi    $t4, $t4, 1 # increment de 1 le comtpeur de mots par ligne
    addi    $t2, $t2, 1 # incremente de 1 le compteur de loop pour traiter le prochain mot
    addi    $s1, $s1, 4 # on se deplace au prochain mot

    slti    $t5, $t4, 4    # VERIF: on a moins de 4 mots imprimes sur cette ligne?#
    bne     $t5, $0, checkLoop # CAS OUI: on n imprime pas le retour de ligne

    # CAS NON: on prnint une nouvelle ligne
    addi    $a0, $0, 10 # on prepare ('\n') dans a0.
    li      $v0, 11 # on print le retour
    syscall                 
    addi    $t4, $0, 0  # on remet a 0 le comtpeur de mots par ligne

checkLoop:
    slt     $t3, $t2, $t1 # t2 < t1
    beq     $t3, $0, done2  # si aucun mot restants ->fin
    j       loop1  # sinon on cotninue

decWord:
    add     $t7, $t9, $0  # on garde le pointeur t9 dans t7
    lbu     $t8, 0($t7) # on load le prochain char du mot dans t8
    beq     $t8, '\0', return #SI char  == null -> fin de mot
    addi    $t9, $t9, 1  # sinon on passe au prochain char du meme mot

    add     $a0, $0, $t8 # on met le char a imprimer dans a0
    li      $v0, 11         
    syscall                
    j       decWord # ON CONTINUE D IMPRIMER TANT QUON A DES MOTS

return:
    addi    $a0, $0, 32 # on load un espace (' ') dans a0 pour l imprimer
    li      $v0, 11         
    syscall                
    j       back  # on retourne a la routine pour continuer le prnit

done2:
    # il se pourrait quon ai eu a imprimer moins de 4 mots dans la derniere ligne; on ajotue un retour pour une bonne structure
    beq     $t4, $0, exit  # sil n y en a pas -> fin
    addi    $a0, $0, 10  # imprimer le retour de ligne pour le restant des mots
    li      $v0, 11 
    syscall                 
    jr      $ra # retour 
    
#################################################################
###### ROUTINE TRIER : TRIE LES MOTS DANS LE TABLEAU INDEX ######
#################################################################

trier: #c est du bubblesort ici
	move $s0, $ra #/!\ ATTENTION : On garde dans s0 le ra du MAIN , sinon on ferai une loop infini
	
	la $t0, tabMots # premier pointeur: adresse du tableau index
	li $t3, 1     # nbr mots avant de compter = 1  
	###### li $t3, 0     # nbr mots avant de compter = 0   <=== ### doit etre 1 pour aller jusqu'a la fin du tableau 

compterMots:	# comme le texte peut avoir une longueur variable de mots et je ne sais pas 
		# il y en aura combiens APRES le retrait des chars non valides, on va compter la longueur du tableaux des index
				
	lw $t2, 0($t0) # deuxieme pointeur : l'adresse d'un elem directement pointee par le pointeur de index 
	beqz $t2, compterMotsFin # Si adresse pointee = 0 ->FIN ,ON A LE NBR DE MOTS A TRIER
	addi $t3, $t3, 1 # si pas vide ajouter 1 au nbr de mots
	addi $t0, $t0, 4 # decaler de 4 octetes
	j compterMots 	 # et recommencer pour faire le prochain décompte ( au prochain mot)

compterMotsFin:
       ## beq $t3 ,1, fin
	la $t0, tabMots # ON A LE NBR DE MOTS ICI: on remet $t0 comme pointeur d'index (on commence le tri)
	mul $t3, $t3, 4 # on va compter combien de "max" on va trouver (le nbr de tours) maintenant quon connait il y a combien de mots
	add $t1, $t0, $t3 # troisieme pointeur: la fin du tableau est l'adresse de debut + ( nbr de mots * 4 octets)
			  # t1 servira de stop pour eviter de retrier des elemnts deja tries
			  # et arreter le tri a la fin

# COMMENCE LE TRI (donc le bubblesort)

forAdresses:
	beq $t0, $t1, fin # Si t0 = t1 alors on a déja trié le premier mot puisque t1 pointe au dernier mot non trie a partir de t0 tries en remontant vers t0, on a fini
	
	subi $t1, $t1, 4# sinon, on monte t1 pour marquer l'adresse pointee precedemment par t1 comme etant "triee" (on n y retourne pas)
	la $t0, tabMots   # on recompare le premier element en repointant t0 au debut du tableau  des index
	addi $t2, $t0, 4# t2 pointe le deuxieme mot

forChar: #pour iterer les char des mots selectionnees precedemment

	lw $a0, 0($t0)  # pointeur a0: adresse du char du premier mot
	lw $a1, 0($t2)  # pointeur a1: adresse du char du deuxieme mot
	jal strcmp  # on satu a strcmp pour comparer les lettres (et trier apres)
	bltz $v0, pasEchanger # si retour = -1 on les laisse si == 1 alors on echange

	lw $t6, 0($t0)# on load les valeurs contenues dans les adresses de index pour echanger la bonne adresse 
	lw $t7, 0($t2)#dans le cas ou on a du changer de char dans le meme mot, il faut tout de meme garder le bon debut de mot
	sw $t7, 0($t0) 
	sw $t6, 0($t2)
pasEchanger:
	addi $t0, $t0, 4 # ON NE FAIT QU'AVANCER ET TRAITER NEXT ADRESSE
	addi $t2, $t2, 4 
	blt $t2, $t1, forChar #condition de fin de boucle (on a traité tout les mots pour la n ieme iteration)

	j forAdresses     #on arrive ici car t0 = t1 (comparer premier avec lui meme = arreter tri en bubblesort)    

fin:
	move $ra, $s0 
	jr $ra

#############################################
#### ROUTINE STRCMP : COMPARE DEUX CHARS ####
#############################################
strcmp:

    ##partier ajouter pour le cas d'un seul caractere OU pas de caractere (car $a1 pointe vers une invalide address dans la memoire##
                ##(0x00000000) QUAND ELLE ESSAYE DE ACCESS L'ADRESS DU 2 EME MOTS##
                
    beqz $a0, invalidPointer    # Si a0 est null, debug erreur ( en cas ou 0 caractere est valid Ou pas de caractere entree )
    beqz $a1, invalidPointer    # si a1 est null, debug erreur ( si un des caractere valid est entree expml: 1234 5678 9000 5555a)
    
    
    lb $t3, 0($a0) #on load le char a l'adresse  directement pointee par a0 ( premier mot)
    lb $t4, 0($a1) #on load le char a l'adresse pointee par a1 ( 2ieme mot)

comparaisonChar:
    beq $t3, $t4, prochainChar # CAS PAREIL : on diot verifier les prochains char
    bgt $t4, $t3, deuxiemePlusGrand # CAS PAS ECHANGER
    bgt $t3, $t4, premierPlusGrand  # CAS ECHANGER

prochainChar:
    beqz $t3, PremierPlusCourt   # CAS premier mot inclu dans deuxieme
    beqz $t4, DeuxiemePlusCourt  # CAS deuxieme mot inclu dans premier
    addi $a0, $a0, 1            # sinon traiter les prochains char ...
    addi $a1, $a1, 1       
    lb $t3, 0($a0)           
    lb $t4, 0($a1)           
    j comparaisonChar# refaire
    
    #NOTE !!! C'est un peu inutile de faire un cas "v0 = 0" pour les mots identiques, on croisera dans 
    # prochain char le "beqz premier plus court" on mettra le premier en "premier" mais comme ce sont les memes mots 
    # ca change vraiment rien au resultat... 
    # avec le cas 0 on aurait besoin d'une instruction au label "motsIdentique" pour quoi a la fin? pour faire "bez $v0, pasEchanger"....

PremierPlusCourt:
    li $v0, -1 # 1 ier mot plus court (PAS ECHANGER)
    jr $ra

DeuxiemePlusCourt:
    li $v0, 1 # 2ieme mot plus court ECHANGER
    jr $ra

premierPlusGrand:
    li $v0, 1 #Pas besoin d'echanger car dans le bon ordre
    jr $ra

deuxiemePlusGrand:
    li $v0, -1 #A ECHANGER car PAS BON ORDRE
    jr $ra
    
invalidPointer:
    li $v0, -99               # Error: POINTEUR INVALIDE 
    jr $ra                       # Retour

