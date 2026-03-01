





<p align="center">

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" width="50" height="50" alt="Docker"/>
&nbsp;&nbsp;&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-plain-wordmark.svg" width="70" height="50" alt="Docker Compose"/>
&nbsp;&nbsp;&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg" width="50" height="50" alt="MongoDB"/>
&nbsp;&nbsp;&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg" width="50" height="50" alt="WSL2/Linux"/>
&nbsp;&nbsp;&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg" width="50" height="50" alt="mongosh"/>

</p>







🗄️ MongoDB Replica Set with Docker
===================================

📌 Description
--------------

Ce projet met en place une **simulation d’un Replica Set MongoDB** en utilisant **Docker Compose**.  
Il permet de comprendre et tester :

*   🔁 La réplication des données
    
*   ⚡ L’élection automatique du PRIMARY
    
*   🛡️ La tolérance aux pannes (failover)
    
*   📦 Une architecture distribuée locale
    

* * *

🏗️ Architecture
----------------

Le cluster contient :

*   1 PRIMARY
    
*   2 SECONDARY
    
*   1 réseau Docker dédié
    
*   3 volumes persistants
    

              ┌─────────────┐
              │   PRIMARY   │
              │   mongo1    │
              └──────┬──────┘
                     │
         ┌───────────┼───────────┐
         │                       │
    ┌─────────────┐        ┌─────────────┐
    │ SECONDARY   │        │ SECONDARY   │
    │  mongo2     │        │  mongo3     │
    └─────────────┘        └─────────────┘
    

* * *

🛠️ Technologies utilisées
--------------------------




| Technologie | Icône | Rôle |
|-------------|--------|------|
| Docker | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" width="40"/> | Conteneurisation des services MongoDB |
| Docker Compose | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" width="40"/> | Orchestration multi-conteneurs |
| MongoDB 7 | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg" width="40"/> | Base de données NoSQL distribuée |
| mongosh | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bash/bash-original.svg" width="40"/> | Shell d’administration MongoDB |
| WSL2 | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg" width="40"/> | Backend de virtualisation sous Windows |


* * *

🚀 Installation et démarrage
----------------------------

### 1️⃣ Cloner le projet

    git clone https://github.com/ton-username/mongodb-replica-set-docker.git
    cd mongodb-replica-set-docker
    

### 2️⃣ Lancer les conteneurs

    docker compose up -d
    

### 3️⃣ Initialiser le Replica Set

    docker exec -it mongo1 mongosh
    

Puis :

    rs.initiate({
      _id: "rs0",
      members: [
        { _id: 0, host: "mongo1:27017" },
        { _id: 1, host: "mongo2:27017" },
        { _id: 2, host: "mongo3:27017" }
      ]
    })
    

* * *

🔎 Vérification
---------------

    rs.status()
    

Vous devriez voir :

*   1 PRIMARY
    
*   2 SECONDARY
    

* * *

🔌 Connection String
--------------------

Depuis votre machine :

    mongodb://localhost:27017,localhost:27018,localhost:27019/?replicaSet=rs0
    

* * *

🧪 Test du failover
-------------------

1.  Identifier le PRIMARY :
    

    rs.isMaster()
    

2.  Stopper le conteneur PRIMARY :
    

    docker stop mongo1
    

3.  Vérifier l’élection automatique :
    

    rs.status()
    

* * *

🧹 Nettoyage
------------

    docker compose down
    docker system prune -f
    

* * *

🎯 Objectifs pédagogiques
-------------------------

Ce projet permet de comprendre :

*   Les bases des bases de données distribuées
    
*   La haute disponibilité
    
*   L’architecture Replica Set MongoDB
    
*   L’intégration avec Docker
    

* * *

📜 Licence
----------

Projet open-source à des fins éducatives.

