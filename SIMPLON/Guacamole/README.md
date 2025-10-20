# 🏰 Mise en place d'un bastion 🏰 

<details>
<summary><h2> :large_blue_circle: Etude comparative des solutions de Bastion<h2></summary>  

### :arrow_forward: Définition  
>Un Bastion est un serveur spécialement sécurisé entre un réseau interne et un réseau non sécurisé comme internet.  
>Il permet de protéger les comptes à privilèges en particulier, en contrôlant et surveillant les accès dans un environnement sécurisé.

---

### :arrow_forward: Comparaison de différentes solutions de Bastions

J'ai retenu 3 solutions 
* Guacamole
* Teleport
* Azure Bastion

|Nom du serveur|Guacamole|Teleport|Azure Bastion|
|---|---|---|---|
|Protocole pris en charge|SSH, RDP, HTTPS...|SSH, RDP, HTTPS...|SSH et RDP seulement|
|Gratuité|:white_check_mark:|:white_check_mark:|:x:|
|Type de gestion|On premise|On premise|SaaS|
|Maintenance|Nous-même|Nous-même|Microsoft|


Après analyse de ces 3 solutions, j'élimine rapidement Azure Bastion qui est une solution payante. Et je choisis d'installer Guacamole, qui est gratuit, et considéré comme assez simple d'installation pour des accès en RDP et SSH.  
J'opte pour une solution simple et efficace !  

Guacamole sera donc le point d'accès unique pour accéder aux autres serveurs.
Il convient d'installer Guacamole dans une DMZ si l'on souhaite s'y connecter depuis l'extérieur (internet) pour se connecter sur les serveurs internes aux réseau privé.  
</details>

---

<details>
<summary><h2> :large_blue_circle:  Déploiement d'un bastion<h2></summary>  


### :arrow_forward: Connexion par interface Web  

**On se connecte à l'interface depuis une machine cliente sur le réseau à l'adresse du serveur Guacamamole comme montré ci dessous.**  

<img width="1208" height="623" alt="Capture d'écran 2025-10-16 175520" src="https://github.com/user-attachments/assets/fe05e5ca-d97d-447e-be54-123e548a5a3b" />

---

### :arrow_forward: Je rentre ensuite mes identifiants  

> 💡 Note: J'ai supprimé le compte Admin standard et récréé un nouveau avec un nouveau mot de passe  

<img width="290" height="320" alt="image" src="https://github.com/user-attachments/assets/16cf923e-bc82-4ee0-ae4c-160a09fbba50" />  

---

### :arrow_forward: Création de groupes  

**`Paramètres > Connexions > Nouveau groupe`**  
Puis Nommer le groupe  
> 💡 Note:  
> *ROOT* est à la racine de l'arborescence.  
> *Organizationel* contient les groupes qui gèrent les connexions.  
<img width="1207" height="457" alt="Capture d'écran 2025-10-16 182124" src="https://github.com/user-attachments/assets/273e8c10-ab54-4269-a6b9-bb9c02dc3b1e" />  

---

<details>
<summary><h3>  :arrow_forward: Ajouter connexion SSH<h3></summary>  

> ⚙️ **`Paramètres > Connexions > Nouvelle connexion`**  

<img width="1209" height="368" alt="Capture d'écran 2025-10-16 181718" src="https://github.com/user-attachments/assets/bb86a619-0f42-4910-8ac2-01abf36a0d40" />  

---

> ⚙️ **`Bien renseigner le paramètre SSH`**  

<img width="316" height="154" alt="image" src="https://github.com/user-attachments/assets/6bae02f7-0f2e-4d80-bc13-51a75dcc0c44" />  

---

> ⚙️ **`Renseigner l'IP de la machine cible, le port (ici port 22 par défaut), puis l'identifiant et le mot de passe du compte de la machine distante`**  

<img width="481" height="330" alt="Capture d'écran 2025-10-17 144755" src="https://github.com/user-attachments/assets/5875b34f-76d0-4401-a773-f6406110101b" />  

---

> ⚙️ **`Sur le menu d'acceuil on peut visualiser les dernières connexions ainsi que les connexions possibles en bas à gauche, il suffit de cliquer`**  

<img width="1206" height="481" alt="image" src="https://github.com/user-attachments/assets/6dfd6355-2c80-40dd-a17d-18e03c4c12f7" />   

---

> ⚙️ **`Connexion sur la machine distante, on voit bien le nom de compte et l'adresse IP de la machine`**  

<img width="1198" height="679" alt="Capture d'écran 2025-10-17 151122" src="https://github.com/user-attachments/assets/abff8edb-4bad-43ac-ae4c-bd41be5c16b3" />  
</details>

---

<details>
<summary><h3>  :arrow_forward: Ajouter connexion RDP<h3></summary>  
  
> ⚙️ **`Paramètres > Connexions > Nouvelle connexion`**  

<img width="1209" height="368" alt="Capture d'écran 2025-10-16 181718" src="https://github.com/user-attachments/assets/bb86a619-0f42-4910-8ac2-01abf36a0d40" />  

---

> ⚙️ **`Renseigner le nom de la nouvelle connexion, le groupe, le protocole.`**

<img width="293" height="145" alt="Capture d'écran 2025-10-20 080719" src="https://github.com/user-attachments/assets/6d0154b2-cf45-43f1-9859-1afb2b3cc26d" />  

---

> ⚙️ **`Dans Réseau, renseigner DNS ou IP de la cible. Le port si ce n'est pas le port par défaut.`**  

<img width="488" height="200" alt="Capture d'écran 2025-10-20 080724" src="https://github.com/user-attachments/assets/27fcf43e-97c7-473a-845a-88b03669a67c" />  

---

> ⚙️ **`Compte avec lequel s'authentifier sur le serveur distant, le nom de domaine`**

<img width="727" height="266" alt="Capture d'écran 2025-10-20 080731" src="https://github.com/user-attachments/assets/9b1a7708-62cc-421f-807e-71c812da5fb3" />  

---

> ⚙️ **`D'autres paramètres peuvent être ajoutés, comme ignorer certificats si on se connecte par adresse IP. Le fuseau horaire, clavier, beaucoup d'options de conforts sont paramétrables dans ce menu... 
>Puis, enregistrer`**    


### :arrow_forward: Côté client  

> ⚙️ **`On autorise la connexion RDP, on autorise un utilisateur`**  

<img width="957" height="652" alt="image" src="https://github.com/user-attachments/assets/0a0e0761-7622-4738-9e80-05552b68d31f" />  

---

> ⚙️ **`On vérifie que le port 3389 est en écoute depuis toutes les machines`**

<img width="888" height="388" alt="image" src="https://github.com/user-attachments/assets/c830d2a7-6e66-4442-a54d-a15e3f465f2b" />  

---

### :arrow_forward: Problème rentcontré côté serveur  

> ⚙️ **`Ce problème est lié au compte utilisateur "daemon" utilisé par défaut pour exécuter le service "guacd". Vous pouvez le vérifier avec cette commande : sudo ps aux | grep -v grep| grep guacd`**  

<img width="1093" height="435" alt="image" src="https://github.com/user-attachments/assets/5988b207-d2f2-45dd-a45e-4a38361e566b" />  

---

> ⚙️ **`Voici les commandes à exécuter, on voit par la suite que tout est fonctionnel`**  

<img width="1083" height="526" alt="image" src="https://github.com/user-attachments/assets/968eaf4a-0cfb-41dd-aa8d-c279136ac144" />

---

### :arrow_forward: Connexion RDP  

> ⚙️ **`Lorsque l'on clique sur notre serveur on est connecté en RDP dessus`**   


<img width="563" height="578" alt="Capture d'écran 2025-10-20 075123" src="https://github.com/user-attachments/assets/e3d3e21f-20f7-4b80-9e33-77ff591be612" />







</details>
</details>

---

# 🥑 😸 🥑
