# 🧠 Architecture de l’Application Machine – `locker-machine`

## 🎯 Objectif

L’application `locker-machine` gère l’interface physique entre l’utilisateur final et la machine connectée (casiers, groupe froid, paiement…). Elle fonctionne en local sur un mini PC installé dans chaque armoire/casier autonome.

---

## 💻 Environnement matériel

* **Mini PC industriel** :

  * OS : **Ubuntu 24.04 LTS**
  * CPU : ARM ou x86\_64 compatible
  * Stockage : SSD 64–128 Go
  * RAM : 4–8 Go
  * Connectique : USB, GPIO, Ethernet, Wi-Fi

* **Périphériques intégrés** :

  * 🧊 **Groupe froid** (surveillance/contrôle)
  * 🔐 **Contrôleurs de moteurs** pour les casiers
  * 🏷️ **Lecteur RFID/NFC** (identification badge)
  * 🧾 **Scannette code-barres** (produit ou ticket)
  * 💳 **TPA (terminal de paiement)** (Nexgo, Ingenico, etc.)
  * 🪙 **Monnayeur** (optionnel)

---

## 🖥️ Architecture logicielle

### 🧩 Stack technique

* **Frontend** : interface tactile en **React** ou HTML/JS/CSS embarqué (mode kiosk)
* **Backend** : **Spring Boot 3.x** léger (avec Thymeleaf si interface côté serveur)
* **Communication inter-composants** :

  * REST pour la communication avec `locker-api`
  * WebSocket (temps réel si nécessaire)
  * Port série / USB pour la lecture des périphériques

---

## 🔄 Fonctionnement général

```mermaid
flowchart TD
    Start[🔌 Allumage Machine]
    UI[🖥️ Interface Utilisateur]
    RFID[🏷️ Lecture badge]
    Auth[🔐 Authentification]
    Action[🎛️ Choix action (ouvrir casier, paiement, etc.)]
    Casier[📦 Contrôle casier]
    Temp[🌡️ Capteurs température]
    API[🌐 Appel API centrale]
    End[✅ Fin transaction]

    Start --> UI --> RFID --> Auth --> Action
    Action --> Casier --> API --> End
    Action --> Temp --> API
```
