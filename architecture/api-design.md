# 📡 Spécification de l’API REST – `locker-api`

## 🔐 Authentification

**Endpoints**

* `POST /auth/login` → Authentifie un utilisateur, retourne un JWT
* `GET /auth/me` → Infos utilisateur connecté
* `POST /auth/refresh` → Rafraîchit le token *(optionnel)*

```json
{
  "email": "admin@locker.local",
  "password": "password123"
}
```

---

## 👤 Utilisateurs

**Endpoints**

* `GET /users` *(ADMIN)* : Liste utilisateurs
* `GET /users/{id}` : Détail
* `POST /users` *(ADMIN)* : Création
* `PUT /users/{id}` : Édition
* `DELETE /users/{id}` : Suppression

```json
{
  "id": 1,
  "email": "admin@locker.local",
  "fullName": "Admin Système",
  "role": "ADMIN",
  "badgeId": "RFID123456"
}
```

---

## 📦 Produits

**Endpoints**

* `GET /products`
* `GET /products/{id}`
* `POST /products` *(ADMIN)*
* `PUT /products/{id}` *(ADMIN)*
* `DELETE /products/{id}` *(ADMIN)*

```json
{
  "id": 101,
  "name": "Yaourt Fraise",
  "requiresCold": true,
  "minTemp": 0,
  "maxTemp": 4,
  "expiryDate": "2025-06-30"
}
```

---

## 📈 Armoires

**Endpoints**

* `GET /cabinets`
* `GET /cabinets/{id}`
* `POST /cabinets` *(ADMIN)*
* `PUT /cabinets/{id}` *(ADMIN)*
* `DELETE /cabinets/{id}` *(ADMIN)*

---

## 🔐 Casiers

**Endpoints**

* `GET /lockers`
* `GET /lockers/{id}`
* `POST /lockers` *(ADMIN)*
* `PUT /lockers/{id}` *(ADMIN)*
* `DELETE /lockers/{id}` *(ADMIN)*
* `POST /lockers/{id}/open`

```json
{
  "id": 23,
  "status": "OCCUPIED",
  "currentTemp": 3.2,
  "productId": 101,
  "cabinetId": 5
}
```

---

## 🧊 Températures

**Endpoints**

* `GET /temperatures` *(ADMIN/TECHNICIEN)*
* `GET /temperatures/latest`
* `POST /temperatures` *(MACHINE)*

```json
{
  "lockerId": 23,
  "timestamp": "2025-06-02T14:45:00Z",
  "value": 3.5
}
```

---

## 💰 Transactions

**Endpoints**

* `GET /transactions` *(ADMIN)*
* `GET /transactions/{id}`
* `POST /transactions`

---

## 🔧 Machines

**Endpoints**

* `GET /machines`
* `GET /machines/{id}`
* `POST /machines/checkin`

```json
{
  "machineId": "MCH-01",
  "ip": "192.168.1.45",
  "status": "OK",
  "softwareVersion": "1.0.2"
}
```

---

## ⛔ Règles métier

* ❄️ Produit froid → casier entre 0–4°C
* 🮺 1 produit par casier
* 🛡️ Ouverture journalisée
* ❌ Vente refusée si :

  * Paiement KO
  * Température non conforme
  * Casiers en erreur

---