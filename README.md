# 🏢 GIE Backend

> Système de gestion intégré pour les achats et les contacts - Backend RESTful API

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Maven](https://img.shields.io/badge/Maven-3.x-blue.svg)](https://maven.apache.org/)
[![Hibernate](https://img.shields.io/badge/Hibernate-6.4.3-green.svg)](https://hibernate.org/)
[![Spark Java](https://img.shields.io/badge/Spark%20Java-2.5-red.svg)](https://sparkjava.com/)

---

## 📋 Table des matières

- [À propos](#-à-propos)
- [Fonctionnalités](#-fonctionnalités)
- [Technologies utilisées](#-technologies-utilisées)
- [Prérequis](#-prérequis)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Démarrage](#-démarrage)
- [Structure du projet](#-structure-du-projet)
- [API Endpoints](#-api-endpoints)
- [Base de données](#-base-de-données)

---

## 🎯 À propos

**GIE Backend** est une application backend robuste développée en Java qui fournit une API RESTful pour gérer :

- 📦 **Gestion des achats** : Produits, catégories, détails d'achat et statuts
- 👥 **Gestion des contacts** : CRM pour particuliers et entreprises
- 📧 **Envoi d'emails** : Service d'envoi de mails intégré
- 🏠 **Gestion des adresses** : Système d'adressage complet

Ce projet fait partie d'un écosystème GIE avec un frontend JavaFX séparé.

---

## ✨ Fonctionnalités

### Module Achats

- ✅ Gestion complète des produits avec catégories
- ✅ Création et suivi des achats
- ✅ Détails d'achat avec réductions
- ✅ Gestion des statuts d'achat
- ✅ Persistance automatique via Hibernate

### Module CRM

- ✅ Gestion des contacts (Particuliers & Entreprises)
- ✅ Système d'adresses complet
- ✅ Recherche par email, nom, téléphone
- ✅ Envoi d'emails automatisé
- ✅ Base de données relationnelle optimisée

---

## 🛠 Technologies utilisées

| Technologie      | Version   | Description                   |
| ---------------- | --------- | ----------------------------- |
| **Java**         | 21        | Langage de programmation      |
| **Maven**        | 3.x       | Gestion des dépendances       |
| **Spark Java**   | 2.5       | Framework web micro-services  |
| **Hibernate**    | 6.4.3     | ORM pour la persistance       |
| **MySQL**        | 5.x / 8.x | Base de données relationnelle |
| **Gson**         | 2.9.0     | Sérialisation JSON            |
| **Jakarta Mail** | 2.0.1     | Envoi d'emails                |

---

## 📦 Prérequis

Avant de commencer, assurez-vous d'avoir installé :

- ☕ **JDK 21** - [Télécharger ici](https://www.oracle.com/java/technologies/downloads/#java21)
- 🗄️ **MySQL Server** (5.x ou 8.x)
- 📦 **Maven** (3.6+)
- 🔧 **Git** (optionnel)

> ⚠️ **Important** : Ce projet nécessite **JDK 21**. Si vous rencontrez des problèmes, vérifiez votre version Java avec `java -version`.

---

## 🚀 Installation

### 1. Cloner le projet

```bash
git clone https://github.com/k2b2gie/gie-backend.git
cd gie-backend
```

### 2. Installer les dépendances

```bash
mvn clean install
```

### 3. Compiler le projet

```bash
mvn package
```

Le fichier JAR sera généré dans le dossier `target/` :

- `gie-backend-1.0-SNAPSHOT.jar`

---

## ⚙️ Configuration

### Configuration de la base de données

Éditez le fichier `src/main/resources/hibernate.cfg.xml` :

```xml
<property name="hibernate.connection.url">
    jdbc:mysql://localhost:3306/gie?createDatabaseIfNotExist=true
</property>
<property name="hibernate.connection.username">root</property>
<property name="hibernate.connection.password">root</property>
```

> 💡 **Note** : Le schéma de base de données `gie` sera créé automatiquement au premier lancement.

> ⚠️ **Attention** : Si un schéma `gie` existe déjà, veuillez le supprimer pour éviter les conflits :
>
> ```sql
> DROP DATABASE IF EXISTS gie;
> ```

### Configuration du serveur

Le serveur démarre par défaut sur :

- **URL** : `http://localhost:4567`
- **Port** : `4567`

---

## 🎬 Démarrage

### Méthode 1 : Exécuter le JAR

```bash
java -jar target/gie-backend-1.0-SNAPSHOT.jar
```

### Méthode 2 : Via Maven

```bash
mvn exec:java
```

### Vérification

Si le serveur démarre correctement, vous devriez voir :

```
Serveur démarré sur l'adresse http://localhost:4567
```

---

## 📁 Structure du projet

```
gie-backend/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── org/uiass/eia/
│   │   │       ├── achat/              # Module gestion des achats
│   │   │       │   ├── Achat.java
│   │   │       │   ├── AchatDao.java
│   │   │       │   ├── Produit.java
│   │   │       │   ├── ProduitDao.java
│   │   │       │   ├── DetailAchat.java
│   │   │       │   ├── CategorieProduit.java
│   │   │       │   └── StatutAchat.java
│   │   │       ├── controller/         # Contrôleurs REST
│   │   │       │   ├── AchatController.java
│   │   │       │   ├── ContactController.java
│   │   │       │   └── TestController.java
│   │   │       ├── crm/                # Module CRM
│   │   │       │   ├── Contact.java
│   │   │       │   ├── ContactDao.java
│   │   │       │   ├── Particulier.java
│   │   │       │   ├── Entreprise.java
│   │   │       │   ├── Adresse.java
│   │   │       │   ├── AdresseDao.java
│   │   │       │   ├── MailSender.java
│   │   │       │   └── GetSessionFactory.java
│   │   │       └── helper/             # Utilitaires
│   │   │           └── HibernateUtility.java
│   │   └── resources/
│   │       ├── hibernate.cfg.xml       # Configuration Hibernate
│   │       └── META-INF/
│   │           └── persistence.xml     # Configuration JPA
│   └── test/
│       └── java/
├── pom.xml                              # Configuration Maven
├── dependency-reduced-pom.xml          # POM optimisé (généré)
└── README.md                            # Documentation du projet
```

---

## 🔌 API Endpoints

### 📦 Achats

#### Produits

| Méthode  | Endpoint                   | Description                 |
| -------- | -------------------------- | --------------------------- |
| `GET`    | `/api/produits/all`        | Récupérer tous les produits |
| `GET`    | `/api/produits/get/:id`    | Récupérer un produit par ID |
| `POST`   | `/api/produits/add`        | Ajouter un nouveau produit  |
| `PUT`    | `/api/produits/update`     | Mettre à jour un produit    |
| `DELETE` | `/api/produits/delete/:id` | Supprimer un produit        |

#### Achats

| Méthode  | Endpoint                 | Description               |
| -------- | ------------------------ | ------------------------- |
| `GET`    | `/api/achats/all`        | Récupérer tous les achats |
| `GET`    | `/api/achats/get/:id`    | Récupérer un achat par ID |
| `POST`   | `/api/achats/add`        | Créer un nouvel achat     |
| `PUT`    | `/api/achats/update`     | Mettre à jour un achat    |
| `DELETE` | `/api/achats/delete/:id` | Supprimer un achat        |

### 👥 Contacts

| Méthode  | Endpoint                         | Description                 |
| -------- | -------------------------------- | --------------------------- |
| `GET`    | `/api/contacts/all`              | Récupérer tous les contacts |
| `GET`    | `/api/contacts/get/email/:email` | Rechercher par email        |
| `GET`    | `/api/contacts/get/:id`          | Récupérer un contact par ID |
| `POST`   | `/api/contacts/add`              | Ajouter un nouveau contact  |
| `PUT`    | `/api/contacts/update`           | Mettre à jour un contact    |
| `DELETE` | `/api/contacts/delete/:id`       | Supprimer un contact        |

### 📍 Adresses

| Méthode  | Endpoint                   | Description                   |
| -------- | -------------------------- | ----------------------------- |
| `GET`    | `/api/adresses/all`        | Récupérer toutes les adresses |
| `POST`   | `/api/adresses/add`        | Ajouter une nouvelle adresse  |
| `PUT`    | `/api/adresses/update`     | Mettre à jour une adresse     |
| `DELETE` | `/api/adresses/delete/:id` | Supprimer une adresse         |

---

## 🗄️ Base de données

### Schéma

Le backend utilise MySQL avec création automatique des tables via Hibernate (`hibernate.hbm2ddl.auto=update`).

#### Tables principales :

- **`contact`** - Informations des contacts (avec héritage pour Particulier/Entreprise)
- **`adresse`** - Adresses des contacts
- **`produit`** - Catalogue des produits
- **`achat`** - En-têtes des achats
- **`detail_achat`** - Détails ligne par ligne des achats
- **`categorie_produit`** - Catégories de produits
- **`statut_achat`** - États des achats

### Connexion

```properties
URL      : jdbc:mysql://localhost:3306/gie
Username : root
Password : root
```

---

## 🔗 Projet Frontend

Ce backend fonctionne avec une application JavaFX frontend.

### Prérequis Frontend

- 📦 **JavaFX SDK** - [Télécharger la dernière version](https://gluonhq.com/products/javafx/)
  - Compatible avec toutes les versions récentes (22+)
  - Téléchargez la version correspondant à votre OS (Windows, Mac, Linux)

### Lancement du frontend

Remplacez `<CHEMIN_JAVAFX>` par le chemin de votre JavaFX SDK :

```bash
java --module-path "<CHEMIN_JAVAFX>\lib" --add-modules javafx.controls,javafx.fxml -jar .\GieFrontend1-1.0-SNAPSHOT.jar
```

**Exemple Windows :**

```bash
java --module-path "C:\javafx-sdk-23\lib" --add-modules javafx.controls,javafx.fxml -jar .\GieFrontend1-1.0-SNAPSHOT.jar
```

---

## 📝 Licence

Ce projet est développé dans le cadre académique pour l'UIASS - EIA.

---

## 👥 Contributeurs

Développé avec ❤️ par l'équipe GIE

---

## 📞 Support

Pour toute question ou problème :

- 📧 Créer une issue sur GitHub
- 💬 Contacter l'équipe de développement

---

<div align="center">

**[⬆ Retour en haut](#-gie-backend)**

Made with ☕ and Java

</div>
