# **Brigitte Friang, DGSE & ESIEE**

**Contributeurs: [N'Famoussa Kounon NANAMOU](https://www.linkedin.com/in/nanamou/) & [Mehdi SADIR](https://www.linkedin.com/in/sadirmehdi/)**   


![Google logo](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/challenge_home.PNG "google logo")


### Description de la compétition
Du samedi 24 octobre au mercredi 11 novembre 2020, la **DGSE** et l'**ESIEE Paris** organisaient le challenge de cybersécurité intitulée **Brigitte Friang** qui consistait à incarner l’**agent 42** afin de déjouer une attaque menaçant les ressortissants et les intérêts français suite à une révolte dans un pays fictif.  

Ce CTF était composé en trois phases. Une première phase de **pré-CTF** qui consistait à trouver les challenges de la compétition ( :stuck_out_tongue_closed_eyes: ). Après avoir perdu bon nombre des participants à cette phase, venait ensuite la deuxième phase qui était le vrai **CTF**. Enfin, les mieux classés sont attendus pour une remise de prix lors de l'European Cyberweek à Rennes (https://www.european-cyber-week.eu/).  

En ce qui me concerne, par faute de temps, je n'ai pu accorder que 3h ( :mask:) à la compétition durant lesquelles j'ai réalisé tous les défis de la phase de **pré-CTF** que je me propose de traiter dans les lignes qui suivent.  

Lien du challenge: www.challengecybersec.fr

[DGSE](https://www.defense.gouv.fr/dgse): Direction Générale de la Sécurité Extérieure  
[ESIEE](https://www.esiee.fr/): École Supérieure d'Ingénieurs en Électrotechnique et Électronique


---  
---
# I. Défis du pré-pré-CTF: débuts des hostilités (jolie tautologie !)
**Objectif**: retrouver les défis de la compétitions  
En me rendant sur le lien du challenge (www.challengecybersec.fr), recupéré sur le site de la DGSE, je suis tombé sur la jolie page web suivante.   

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture1.PNG " ")                        

                              
Etant donné que c'est un CTF-like, il faut être attentif aux moindres détails. C'est d'ailleurs ce qu'on nous rappelle en cette phrase   
> **Ouvrez bien les yeux, vous avez jusqu'au 11/11/2020 23:59:59**.  

## I.1. Analyse/Inspection de code source  
Je ne sais pas pour vous, mais face à une page web, je suis toujours tenté d'aller voir, toute de suite, le code source de la page web avec CTRL+U.  

![capture2](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture2.png " ")  

Dans ce code source, une chose m'a sauté aux yeux. Il s'agit du commentaire à la ligne 10 qui indique une nouvelle page web `/static/message-secret.html`.

**Note 1**: Pour une question d'organisation et de bonnes pratiques, je regarde toujours le code source des pages et je n'hésite pas à suivre les liens que j'y trouve. Il serait quand même dommage de perdre beaucoup de temps ou même de baisser les bras parce qu'on a laissé de côté un détail pertinent qui sert pour la suite. En le faisant, j'ai téléchargé les deux images présentes sur la page courante pour les analyser plus tard.

__Lien dans le code source__
+ /static/bootstrap/css/bootstrap.min.css
+ /static/css/style.css
+ /static/js/particles.min.js
+ /static/js/app.js  
+ /static/img/dgse.png
+ /static/img/esiee.png

Les deux derniers correspondent aux images disponibles ici:  
+ https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/dgse.png
+ https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/esiee.png

:information_source: : La seule chose utile dans le code source était bien le commentaire que j'ai suivi en complétant mon URL (encadré rouge). Je suis alors tombé sur un long texte incompréhensible. En sélectionnant tout le texte (CTRL+A), on découvre:   


![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture3.png " ")  

**Remarque 1**: Ce message a l'air de commuiquer une information secrète (tout comme son chemin d'ailleurs!: **/static/message-secret.html**).   
**Remarque 2**: Dans le corner gauche (encadré jaune), on aperçoit le titre de la page **Cesar** ; il s'agit donc d'un **chiffrement par décalage**.    
**Remarque 3**: Certains caractères sont en gras et, délimités par des barres verticales `|` si sélectionnés (encadrés noires): `/`, `j`, `o`, `h` et `a`.  
Comme toujours, j'ai *checké* le code source de la page avant de continuer. Rien d'intéressant ne s'y trouvait.  



## I.2. Déchiffrement du code de Cesar  
**Etape 1: trouver le décalage (la clef de déchiffrement)**    
***Méthode 1***: analyse à la mano    
Les lettres du texte sont typiquement celles utilisées en français et en anglais. De plus, on remarque un mot formé d'une seule lettre (encadré vert): la langue utilisée est probablement du français où: h --(correspondance)--> a. **La clef de déchiffrement est donc 7**.

***Méthode 2***: analyse automatisée (brute force)  
L'autre méthode consiste à copier un court passage (une phrase, par exemple) et le dechiffrer avec un outil en ligne comme https://www.dcode.fr/caesar-cipher ou https://cryptii.com/pipes/caesar-cipher?fbclid=IwAR0ca6cVpcx1ZdJJEKY0NpY7Ey0m_g5YnVLftwaE90ZH_fCPHy8_8-kK7Us.   


![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture4.png "outil en ligne https://www.dcode.fr/caesar-cipher")   

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture5.png "outil en ligne https://cryptii.com/pipes/caesar-cipher?fbclid=IwAR0ca6cVpcx1ZdJJEKY0NpY7Ey0m_g5YnVLftwaE90ZH_fCPHy8_8-kK7Us")   


**Etape 2: déchiffrer le code**  
Maintenant que nous connaissons la clef de déchiffrement, il suffit de réutiliser l'une des méthodes précédentes sur le texte en entier pour avoir le message en clair. Comme je suis gentil :blush:, je vous donne une autre méthode en ligne de commande (utile en offline).  

Texte déchiffré en entier:
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture6.png "capture6.png")   

En concordance avec mes remarques **Remarque {1,2,2}**, j'ai copié-collé les mots dans cet ordre en mettant les lettres concernées entre `[` et `]`.   
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture7.png "capture7.png")     

Après rassemblessement des pièces du puzzle, j'ai donc obtenu le repertoire caché `/chat`.  



**Conclusion 1**: A mon avis, le cheminement (**Web** --> **Stéganographie** --> **Cryptographie**) présenté jusqu'ici était celui espéré par les organisateurs/créateurs des défis si non, ils se seraient pas donnés la peine de chiffré le texte laissé en code de Cesar! Ils n'ont peut-être pas vérifié l'existence du repertoire `/chat` dans des dictionnaires couramment utilisés en CTF. Nous utilisons la technique d'énumération web **fuzzing directory** à l'aide de l'outil **gobuster** sur un des dictionnaires nativement integrés à kali Linux **/usr/share/wordlists/dirb/small.txt** comme suit. Je vous réserve une troisième méthode dans la **Conclusion 2**

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture8.png "capture8.png")  

---  
---  

# II. Défis du pré-CTF
En accédant à `/chat`, nous nous retrouvons face à une application sécrète de communication comme le montre le titre de la page **S3curConv** (encadré jaune).   


![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture9.png "capture9.png")  


**Remarque 4**: Armand Richelieu de la direction nous dit dans son premier message que nous repartons en mission. Ce qui veut dire, qu'on est pas encore au bout de nos surprises!  
**Remarque 5**: Le nom des services semblent faire référence aux catégories des défis à relever.    
- Service Crypto;  
- Service Web;  
- Service Algo;  
- Service Forensic;  

Nous passons alors aux communications suivantes.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture11.png "capture11.png")  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture12.png "capture12.png")  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture13.png "capture13.png")  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture14.png "capture14.png")  


**Remarque 6**: D'après les échanges avec Antoine Rossignol, Jérémy Nitel, Blaise Pascal et Blaise Pascal, nous pouvons confirmer la remarque **Remarque 5** et que pour valider chaque défis, il suffit de laisser le bon message à la bonne personne du service choisi.  

**Note 2**: Encore un autre élément, non espéré par les constructeurs des challenges. Un joueur plus malin pouvait aller plus vite en utilisant la technique de reconnaissance **Google dorking** (l'opérateur Google `site:` permet de trouver tous les contenus liés à un sujet sur le site précisé) afin de retrouver directement le lien des défis:  

+ https://www.challengecybersec.fr/35e334a1ef338faf064da9eb5f861d3c/
+ https://www.challengecybersec.fr/4e9033c6eacf38dc2a5df7a14526bec1/
+ https://gitlab-rive2.challengecybersec.fr/
+ https://www.challengecybersec.fr/chat/public/uploads/original.txt
+ https://www.challengecybersec.fr/chat/public/uploads/compte_rendu_eve.pdf
+ https://www.challengecybersec.fr/9bcb53d26eab7e9e08cc9ffae4396b48
+ https://challengecybersec.fr/1410e53b7550c466c76fc7268a8160ae
+ https://challengecybersec.fr/1410e53b7550c466c76fc7268a8160ae/5f3949527e73ad93b73b070bb12cde1292bbcde5
+ https://gitlab-rive2.challengecybersec.fr/users/sign_in
+ https://challengecybersec.fr/d3d2bf6b74ec26fdb57f76171c36c8fa/VX_elliptique.pdf
+ https://ctf.challengecybersec.fr/7a144cdc500b28e80cf760d60aca2ed3/lock.php  

Ce dernier lien est celui recherché depuis le début. Il donne accès aux challenges du vrai **CTF**. 

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture15.png "capture15.png")  


  

**Conclusion 2**: Il n'yavait pas de fichier `/robots.txt` ni `/sitemap.xml` sur l'application web ! Un habitué averti pouvait bien pensé dès cet instant à faire du **dorking**!  
Faisant suite à la conclusion **Conclusion 1**, nous pouvons supposer que les constructeurs des challenges ont une fois de plus "oublié" que les robots de Google indexent toutes les pages des sites web sur Internet à moins qu'on n'interdise explicitement cela dans un fichier `/robots.txt`.



## II.1. Service Crypto  
Dans cette catérogrie, Antoine Rossignol nous donne 4 fichiers qui pourront nous être utiles.  
+ [echange.txt ](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/echange.txt)  
+ [archive_chiffree](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/archive_chiffree)    
+ [layout.pdf ](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/layout.pdf)   
+ [compte_rendu_eve.pdf ](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/compte_rendu_eve.pdf)    


J'ai alors décidé d'analyser fichier par fichier.   
[**archive_chiffree**]  
**Remarque 6**: Nous y reviendrons!  


[**layout.pdf**]  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture19.png "capture19.png")   

**Remarque 7**: Aucun mot de passe évident n'a pu ouvrir la sésame.  

[**Fichier echange.txt**]  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture18.png "capture18.png")   

**Remarque 8**: On doit se réferer au compte-rendu d'Eve Descartes.  


[**compte_rendu_eve.pdf**]  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture16.png "capture16.png")   

**Remarque 9**: Il s'agit d'un standard connu à 256 micro-fusibles programmables typpe eFuse dont l'ordre des bits est sûrement interverti ainsi que la position du MSB.  
**Remarque 10**: On peut la contacter par téléphone ou par mail pour tout renseignement complémentaire.

:information_source: Après plusieurs analyses sur ces fichiers sans succès, soyons fous et contactons Eves Descartes au regard de ma remarque **Remarque 10**


**Etape 1** : Joindre Ève Descartes par son adresse mail `eve.descartes@esiee.fr`  
J'ai envoyé un mail à son adresse mail et j'ai obtenu cette réponse 2 minutes plus tard.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture17.png "capture17.png")  
 
 
 Au regard de sa réponse (encadré en evrt), elle préfère être joint par téléphone, pauvre Eve Descartes!
 
 
**Etape 2** : Joindre Ève Descartes par téléphone  `+33 (0)1 45 92 60 96`
C'est alors que j'ai pris mon téléphone pour la joindre. Le répondeur me donne des bips bips bips (classiques pour ceux qui voient ce que je veux dire :p). Il s'agit du [code morse](https://www.youtube.com/watch?v=QNNwv7si4qU) que j'ai décodé avec cet outil en ligne: https://morsecode.world/international/decoder/audio-decoder-adaptive.html  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture20.png "capture20.png")  

**Remarque 11**: Bingo! On vient d'obtenir quelque chose mais un peu bruité. En effet, entre l'enregistrement du vocal et le décodage sur le site, le premier caractère a été alteré mais ce n'est pas du tout gênant car on peut clairement deviner que le mot `resistance` est le mot de passe recherché. En le saisissant dans le champ du fichier `layout.pdf`, nous y entrons et voyons ceci.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture21.png "capture21.png") 

**Remarque 12**: Cela ressemble à des fusibles programmables type eFuse au nombre de **256 = 16 ligne x 16 colonnes**, comme nous l'avait dit Eve Descartes dans son `compte_rendu_eve.pdf`. J'ai alors imaginé que chaque ""fusible"" correspondait à un bit de la clef. 

**Etape 3** : déchiffrer le fichier `archive_chiffree`
Deux façons de coder s'offrent à moi.  
+ Code 1: codé par 0 les fusibles mordus en leur milieu et par 1 ceux intacts  
+ Code 2: codé par 1 les fusibles mordus en leur milieu et par 0 ceux intacts   

Le premier code me donne le code ci-dessous:   
1011111010111010  
1010110011011111  
1100110111001010  
1100100111011111  
1011101010111100  
1011110111011111  
1101111111011111  
1101111111011111   
1101111111011111   
1101111111011111   
1101111111011111  
1101111111011111  
1101111111011111   
1101111111011111   
1101111111011111   
1101111111011111  

Le seond code me donne le code ci-dessous: 
0100000101000101   
0101001100100000   
0011001000110101   
0011011000100000   
0100010101000011   
0100001000100000   
0010000000100000   
0010000000100000   
0010000000100000   
0010000000100000   
0010000000100000   
0010000000100000   
0010000000100000   
0010000000100000   
0010000000100000   
0010000000100000    

:information_source: Attention à la copie, deux espaces sont ajoutés à la fin de chaque ligne afin de pouvoir formater car j'utilise le langage markdown pour écrire ce write-up!  

**Coucou cyberchef**  
On décode le premier code avec cyberchef et on obtient ce truc insensé `¾º¬ßÍÊÉßº¼½ßßßßßßßßßßßßßßßßßßßßß`. Ce n'est clairement pas ce qu'on recherche
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture22.png "capture22.png") 


On décode le deuxième code avec cyberchef et on obtient `AES 256 ECB                     `. Woyé, ça sent la fête!!!  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture23.png "capture23.png")  

**Remarque 13**: Il faut bien noter les espaces après **AES 256 ECB**. Il m'a bien fait transpirer :rage: et je suis sorti prendre un café après :sweat_smile:  
**Remarque 14**: J'avais aussi remarqué que les coupures en plein milieu sont toutes alignées. Cela n'a pa servi!  
**Remarque 15**: Ce résultat donné par cyberchef nous indique que l’algorithme de chiffrement utilisé est **AES 256 en mode ECB**.  
Nous allons donc réutiliser notre outil cyberchef avec les bons paramètres.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture24.png "capture24.png")  

Pour les habitués, le magic number indique qu'il s'agit d'un fichier **zip**. J'enregistre donc l'output avec cette extension et le dézippe juste après.    
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture25.png "capture25.png")  

En fouillant un peu à l'intérieur du fichier extrait, on obtient d'autres fichiers PDF.  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture26.png "capture26.png")  

**Etape 4** : déchiffrer le fichier `code_acces.pdf`
Après avoir tapé à la porte de tout un chacun des fichiers PDF, il en ressort que `code_acces.pdf` est protégé par un mot de passe, probablement la solution au système de congruences contenu dans `message.pdf`???  

Après résolution de ce système par un outil en ligne dont je ne me souviens plus ( disappointed_relieved: ), on trouve:   
+ x=5622 pour l'équation **x^3≡573[8387]**  
+ x=5622 ou x=7640 ou x=5964 pour l'équation **x^3≡98[9613]**  
+ x=5622 ou x=2589 ou x=7643 pour l'équation **x^3≡2726[7927]**  

Il s'agit d'un système d'équation, donc la solutioon commune à chacune des équations de congruence est celle du système **x=5622**  
J'ai utilisé cette valeur pour accéder au contenu du fichier `code_acces.pdf` et.... je suis tombé à nouveau sur une autre équation (please give me that flag :sob: :sob: :sob: )  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture27.png "capture27.png")  

Un copier-coller de l'équation sur google m'indique que le code utilisé est **corps de Galois (ou GF(256))** que je décode avec cet [outil en ligne](shorturl.at/xABW5)  

**Flag**: `b a:e z`


Antoine Rossignol était content de ma démarche et m'a filé donc le lien du vrai CTF ( :triumph: ): `/7a144cdc500b28e80cf760d60aca2ed3`  
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Crypto/capture28.png "capture28.png")  

**Fin du défis "Service Crypto"**



## II.2. Service Web  
A compléter ...  



## II.3. Service Algo  
A compléter ...  

## II.4. Service Forensic  
**II.4.1 Défis 1: Analyse de log Nginx**  
Alphonse Bertillon du Service Forensic nous demande de retrouver l'adresse IP suspecte dans le fichier de log `access.log` et la lui envoyer.      
A compléter ... 


---  
---  

# III. Défis du CTF (COROS CTF)
Et voici ou nous nous sommes limités par manque de temps. Nous espérons pouvoir participer à la prochaine édition :heart_eyes:. Merci à la DGSE et à l'ESIEE pour ces beaux challenges.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture40.png "capture40.png") 

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture41.png "capture41.png")  
