# **Brigitte Friang, DGSE & ESIEE**

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
### Débuts des hostilités 
**Objectif**: retrouver les défis de la compétitions  
En me rendant sur le lien du challenge (www.challengecybersec.fr), recupéré sur le site de la DGSE, je suis tombé sur la jolie page web suivante.   

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture1.PNG " ")                        

                              
Etant donné que c'est un CTF-like, il faut être attentif aux moindres détails. C'est d'ailleurs ce qu'on nous rappelle en cette phrase   
> **Ouvrez bien les yeux, vous avez jusqu'au 11/11/2020 23:59:59**.  

## 1. Analyse/Inspection de code source  
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



## 2. Déchiffrement du code de Cesar  
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



**Conclusion 1**: A mon avis, le cheminement (**Web** --> **Stéganographie** --> **Cryptographie**) présenté jusqu'ici était celui espéré par les organisateurs/créateurs des défis si non, ils se seraient pas donnés la peine de chiffré le texte laissé en code de Cesar! Ils n'ont peut-être pas vérifié l'existence du repertoire `/chat` dans des dictionnaires couramment utilisés en CTF. Nous utilisons la technique d'énumération web **fuzzing directory** à l'aide de l'outil **gobuster** sur un des dictionnaires nativement integrés à kali Linux **/usr/share/wordlists/dirb/small.txt** comme suit.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture8.png "capture8.png")  


En accédant à `/chat`, nous nous retrouvons face à une application sécrète de communication comme le montre le titre de la page **S3curConv** (encadré jaune).   


![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture9.png "capture9.png")  


**Remarque 4**: Armand Richelieu de la direction nous dit dans son premier message que nous repartons en mission. Ce qui veut dire, qu'on est pas encore au bout des surprises!  
**Remarque 5**: Le nom des services semblent faire référence aux catégories des défis à relever.    
- Service Crypto;  
- Service Web;  
- Service Algo;  
- Service Forensic;  

Nous passons alors aux communications suivantes.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture10.png "capture10.png") 
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture11.png "capture11.png") 
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture12.png "capture12.png") 


Antoine Rossignol


Jérémy Nitel


Blaise Pascal


Alphonse Bertillon
Service Forensic


echange.txt  
archive_chiffree 
layout.pdf 
compte_rendu_eve.pdf