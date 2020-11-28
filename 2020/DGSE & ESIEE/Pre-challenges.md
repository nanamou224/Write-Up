# **Brigitte Friang by DGSE & ESIEE**

![Google logo](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/challenge_home.PNG "google logo")


### Description de la compétition
Du samedi 24 octobre au mercredi 11 novembre 2020, la **DGSE** et l'**ESIEE Paris** organisaient le challenge de cybersécurité intitulée **Brigitte Friang** qui consistait à incarner l’**agent 42** afin de déjouer une attaque menaçant les ressortissants et les intérêts français suite à une révolte dans un pays fictif.  

Ce CTF était composé en trois phases. Une première phase de **pré-challenge** qui consistait à trouver les challenges de la compétition ( :stuck_out_tongue_closed_eyes: ). Après avoir perdu bon nombre des participants à cette phase, venait ensuite la deuxième phase qui était le vrai **challenge**. Enfin, les mieux classés sont attendus pour une dernière phase **post-challenge** à la DGSE.  

En ce qui me concerne, par faute de temps, je n'ai pu accorder que 3h ( :mask:) à la compétition durant lesquelles j'ai réalisé tous les challenges de la phase de **pré-challenge** que je me propose de traiter dans les lignes qui suivent.  

Lien du challenge: www.challengecybersec.fr

[DGSE](https://www.defense.gouv.fr/dgse): Direction Générale de la Sécurité Extérieure  
[ESIEE](https://www.esiee.fr/): École Supérieure d'Ingénieurs en Électrotechnique et Électronique

---
### Débuts des hostilités 
En me rendant sur le lien du challenge (www.challengecybersec.fr), recupéré sur le site de la DGSE, je suis tombé sur la jolie page web suivante.   

![capture1](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture1.PNG " ")                        

                              
Etant donné que c'est un CTF-like, il faut être attentif aux moindres détails. C'est d'ailleurs ce qu'on nous rappelle en cette phrase   
> **Ouvrez bien les yeux, vous avez jusqu'au 11/11/2020 23:59:59**.  

Je ne sais pas pour vous, mais face à une page web, je suis toujours tenté d'aller voir, toute de suite, le code source de la page web avec CTRL+U.
![capture2](https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/capture2.PNG " ")  

Dans ce code source, une chose m'a sauté aux yeux. Il s'agit du commentaire à la ligne 10 qui indique une nouvelle page web `/static/message-secret.html` que j'ai suivi en complétant mon URL comme ceci `https://challengecybersec.fr/static/message-secret.html`.  

**NB**: A noter que j'ai également suivi tous les liens dans le code source pour m'assurer ne pas passer à côté d'autres indices! En le faisant, j'ai téléchargé les deux images présentes sur la page courante pour les analysées plus tard.

__Lien dans le code source__
+ /static/bootstrap/css/bootstrap.min.css
+ /static/css/style.css
+ /static/img/dgse.png
+ /static/img/esiee.png
+ /static/js/particles.min.js
+ /static/js/app.js  

__Images téléchargées__
+ https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/dgse.png
+ https://github.com/nanamou224/Write-Up/blob/main/2020/DGSE%20%26%20ESIEE/Ressources/esiee.png






