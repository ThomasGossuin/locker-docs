# 🌐 Structure du Service Web – `locker-front`

## 🎯 Objectif

Le service `locker-front` fournit une interface React centralisée permettant aux administrateurs, techniciens et utilisateurs finaux d'interagir avec le système Locker : gestion des casiers, produits, machines, utilisateurs et opérations en temps réel.

---

## ⚙️ Stack technique

* **React** (v18+)
* **TypeScript**
* **Vite** (ou Create React App, selon préférences)
* **React Router** pour la navigation
* **Axios** pour les appels API
* **TailwindCSS** pour le style
* **Zustand** ou **Redux Toolkit** pour la gestion d'état globale
* **AuthContext / JWT** pour l'authentification

---

## 🧭 Structure des pages

```
/src
 ┣ /components       → composants réutilisables (Button, Modal, Loader...)
 ┣ /pages            → pages principales (Dashboard, Users, Products...)
 ┣ /layouts          → Layouts (AdminLayout, PublicLayout)
 ┣ /services         → appels API via Axios
 ┣ /hooks            → hooks personnalisés (useAuth, useLocker...)
 ┣ /store            → état global (Zustand/Redux)
 ┣ /types            → interfaces TypeScript partagées
 ┣ /utils            → fonctions utilitaires (formattage, validation...)
 ┣ /assets           → images, icônes, logos
 ┗ /App.tsx          → définition des routes et contexte
```

---

## 🧑‍💻 Pages principales

* **/login** → Connexion utilisateur
* **/dashboard** → Vue d'ensemble (statistiques, alertes, activité récente)
* **/users** → Gestion des utilisateurs
* **/products** → Catalogue des produits
* **/lockers** → Liste des casiers + actions
* **/cabinets** → Organisation physique
* **/machines** → État réseau des machines
* **/temperatures** → Historique + alertes
* **/transactions** → Liste des ventes

---

## 🔐 Authentification

* JWT stocké en localStorage (ou cookie sécurisé en option)
* Middleware React Router pour bloquer les routes protégées
* Gestion des rôles : ADMIN, TECHNICIEN, USER

---

## 📡 Communication avec l'API

* Via `AxiosInstance` configuré avec token
* Gestion centralisée des erreurs (401, 500...)
* Loader global / feedback utilisateur

---

## 🧪 Tests (optionnel)

* Jest + React Testing Library
* Cypress pour les tests end-to-end

---

## 📦 Déploiement

* Build statique via `vite build` ou `npm run build`
* Servi via Nginx, Netlify, ou Docker
* Intégration dans l’environnement global locker via sous-domaine ou iframe machine tactile

---