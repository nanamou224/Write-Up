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
+ echange.txt  
+ archive_chiffree  
+ layout.pdf  
+ compte_rendu_eve.pdf  


**Remarque 7**: Dans son dernier message, il nous fait comprendre que l'objectif est de lire le contenu du fichier `archive_chiffree`.   
**Remarque 8**:
**Remarque 9**:

**Etape 1** : Joindre Ève Descartes par son adresse mail `eve.descartes@esiee.fr`  
J'ai envoyé un mail à son adresse mail et j'ai obtenu cette réponse 2 minutes plus tard.  

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Service Crypto/capture17.png "capture17.png") 

**Etape 2** : Joindre Ève Descartes par téléphone  `+33 (0)1 45 92 60 96`
Le répondeur est un tout petit peu bizarre. J'ai alors enregistré le son émis.
![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/Service\ Crypto/audio1.mp3 "audio1.mp3") 



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
A compléter ...  


![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture40.png "capture40.png") 

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture41.png "capture41.png") 
