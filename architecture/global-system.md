# 🏗️ Architecture Générale du Système Locker

## 🔎 Vue d'ensemble

Le système Locker repose sur une architecture modulaire, composée de plusieurs services interconnectés et de technologies modernes :

---

### 🧠 Backend — API centrale

- **Framework** : Spring Boot **3.3.x**
- **Langage** : Java **17+**
- **Sécurité** : Spring Security avec JWT
- **ORM** : Hibernate (JPA)
- **Doc API** : Swagger/OpenAPI via SpringDoc
- **Tests** : JUnit 5, Testcontainers
- Expose des endpoints REST pour :
  - Authentification & rôles
  - Utilisateurs, produits, casiers, armoires, machines
  - Notifications, températures, logs

---

### 🌐 Frontend — Service Web

- **Framework** : React **18.x**
- **Langage** : TypeScript
- **UI** : Tailwind CSS / ShadCN
- **State** : Zustand (ou Redux)
- **Routing** : React Router
- **Appels API** : Axios
- **Tests** : Vitest / React Testing Library
- Accès pour :
  - Utilisateurs finaux (consultation)
  - Administrateurs (gestion, supervision)

---

### 🖥️ Machine — Application embarquée

- **Support matériel** : Mini PC industriel (type Intel NUC ou équivalent)
- **OS embarqué** : Ubuntu **24.04 LTS**
- **Backend local** : Spring Boot **3.3.x** avec Thymeleaf
  - Utilisé pour servir à la fois la logique backend locale et l’interface utilisateur
  - Permet une interface légère et rapide, sans client JavaScript complexe
- **UI locale** : Thymeleaf + HTML/CSS responsive adaptée aux écrans tactiles
- **Périphériques gérés** :
  - Commande des **casiers motorisés**
  - Supervision du **groupe froid**
  - Paiement via **TPA (terminal CB/NFC)**
  - **Monnayeur** pour paiement en espèces
  - **Lecteur de badges RFID**
  - **Scannette** pour lecture de produits ou de codes

- **Communication** :
  - API REST sécurisée vers le backend central (`locker-api`)
  - Support **WebSocket** pour actions immédiates (ex. ouverture casier à distance)
  - Optionnel : **MQTT** pour capteurs ou messages légers (IoT)

---

### 🗄️ Base de données

- **SGBD** : **MariaDB 11.x** (ou MySQL 8.4+)
- **Interface d’administration** : **phpMyAdmin 5.x**
- Hébergement possible en Docker, serveur local ou cloud

---

## 🔗 Objectifs techniques

- 🔹 Séparation claire des responsabilités entre services
- 🔹 Architecture scalable : multi-machines, cloud-ready, microservices si besoin
- 🔹 Haute sécurité : JWT, rôles, logs, traçabilité
- 🔹 Facilité de maintenance : tests, doc, versioning
- 🔹 Extensibilité future vers des technologies embarquées plus avancées (IoT, edge computing)

