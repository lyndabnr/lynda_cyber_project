# Veille Technologique & Préparation au TOEIC 🤖💼

[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TOEIC Morning](https://github.com/lyndabnr/veille_et_toeic/actions/workflows/toeic_morning.yml/badge.svg)](https://github.com/lyndabnr/veille_et_toeic/actions/workflows/toeic_morning.yml)
[![TOEIC Evening](https://github.com/lyndabnr/veille_et_toeic/actions/workflows/toeic_evening.yml/badge.svg)](https://github.com/lyndabnr/veille_et_toeic/actions/workflows/toeic_evening.yml)
[![Cybersecurity News Watch](https://github.com/lyndabnr/veille_et_toeic/actions/workflows/cyber_watch.yml/badge.svg)](https://github.com/lyndabnr/veille_et_toeic/actions/workflows/cyber_watch.yml)

Une suite d'outils automatisés conçus pour la veille technologique (Informatique, IA, Cybersécurité et Réglementation) et l'entraînement quotidien au test d'anglais TOEIC. Le tout est orchestré par GitHub Actions et délivré directement sur vos canaux Telegram sous forme de digests et de questions enrichies.

---

## 🌟 Fonctionnalités Principales

### 1. 🎓 Préparation Quotidienne au TOEIC (`english_toeic_bot.py`)
Ce bot envoie des exercices de préparation au TOEIC en deux sessions quotidiennes :
* ☀️ **Session du Matin (Part 5 - Incomplete Sentences) :** Questions à choix multiples portant sur la grammaire et le vocabulaire.
* 🌙 **Session du Soir (Part 7 - Reading Comprehension) :** Textes courts de compréhension écrite accompagnés de questions.
* 💡 **Correction masquée :** Les réponses et explications détaillées sont envoyées sous forme de **spoiler Telegram** (`<tg-spoiler>`) pour encourager la réflexion avant de révéler la solution.

### 2. 📰 Veille Technologique Complète (`security_audit.py`)
Un agrégateur et traducteur automatique de flux d'actualités structuré en **6 catégories professionnelles** :
* 🔒 **Cybersécurité :** CERT-FR (Avis/Alertes), The Hacker News, BleepingComputer, Krebs on Security, Dark Reading.
* 🤖 **Intelligence Artificielle :** OpenAI News, TechCrunch AI, Actu IA, Hugging Face, Google Research.
* 💻 **Actualités IT & Tech :** Le Monde Informatique, ZDNet Actualités, Wired, Ars Technica.
* 📜 **Conformité & Réglementation :** ANSSI Actualités, LINC CNIL (RGPD), Global Security Mag (GRC).
* 🎯 **Sécurité Offensive & Pentest :** Hack The Box Blog, PortSwigger Web Security.
* 🛡️ **Threat Intel & SOC :** CERT-FR Menaces (CTI), SANS Internet Storm Center, ESET WeLiveSecurity, Microsoft Security.

> [!TIP]
> **Traduction & Dédoublonnage :** Les actualités issues de sources anglophones sont automatiquement traduites en français à la volée. Les doublons sont exclus et les actualités promotionnelles sont filtrées à l'aide d'une liste de mots-clés.

### 3. 🚨 Audit de Sécurité des Logs (`security_audit.py`)
Analyse des fichiers de journaux d'authentification (ex: `mock_auth.log`) pour détecter les attaques par force brute (adresses IP dépassant un seuil de tentatives de connexions échouées) et envoie des rapports d'alertes par e-mail ou Telegram.

---

## 📂 Structure du Projet

```text
├── .github/workflows/
│   ├── cyber_watch.yml      # Workflow de la veille (Matin 09:00 / Soir 23:05)
│   ├── toeic_morning.yml    # Workflow TOEIC Matin (08:00)
│   └── toeic_evening.yml    # Workflow TOEIC Soir (20:00)
├── english_toeic_bot.py      # Script du bot TOEIC (exercices et corrections)
├── security_audit.py        # Script de veille d'actualités et d'audit de logs
├── mock_auth.log            # Fichier de log de démonstration pour l'audit
├── .env.example             # Modèle de variables d'environnement locales
└── README.md                # Présentation du dépôt
```

---

## 🛠️ Configuration & Variables de Sécurité

Les scripts utilisent uniquement la bibliothèque standard de Python (aucune dépendance externe requise) pour garantir une exécution rapide et sans maintenance.

### 1. Configuration Locale (Sécurisée)

Pour exécuter les scripts sur votre propre machine sans risquer de divulguer vos jetons Telegram sur GitHub :

1. Créez un fichier nommé `secrets_config.py` à la racine du projet (ce fichier est déjà présent dans `.gitignore` et ne sera jamais commité).
2. Ajoutez-y vos jetons de la manière suivante :
   ```python
   # Configuration Telegram Confidentielle
   TELEGRAM_BOT_TOKEN_TOEIC = "votre_token_bot_toeic"
   TELEGRAM_CHAT_ID_TOEIC = "votre_id_canal_toeic"

   TELEGRAM_BOT_TOKEN_WATCH = "votre_token_bot_veille"
   TELEGRAM_CHAT_ID_WATCH = "votre_id_canal_veille"
   ```

> [!IMPORTANT]
> Pour configurer d'autres options comme les alertes SMTP, vous pouvez copier le fichier `.env.example` en un fichier `.env` local. Le fichier `.env` est également ignoré par Git.

### 2. Configuration sur GitHub (GitHub Actions)

Pour automatiser les envois via GitHub Actions, configurez les secrets dans votre dépôt GitHub :
1. Allez dans **Settings** > **Secrets and variables** > **Actions** > **New repository secret**.
2. Créez les secrets suivants :
   * `TELEGRAM_BOT_TOKEN_TOEIC` : Le jeton API du bot Telegram TOEIC.
   * `TELEGRAM_BOT_TOKEN_WATCH` : Le jeton API du bot Telegram de Veille.
   * `TELEGRAM_CHAT_ID_TOEIC` : L'identifiant de votre canal/groupe TOEIC.
   * `TELEGRAM_CHAT_ID_WATCH` : L'identifiant de votre canal/groupe de Veille.

---

## 🚀 Utilisation en Local

### 1. Lancer la Veille Technologique
```bash
python security_audit.py --fetch-news
```

### 2. Lancer les Questions TOEIC
* **Défi du Matin :**
  ```bash
  python english_toeic_bot.py --morning
  ```
* **Défi du Soir :**
  ```bash
  python english_toeic_bot.py --evening
  ```

### 3. Exécuter un Audit de Logs
```bash
python security_audit.py mock_auth.log --threshold 5 --telegram
```

---

## 📅 Planification GitHub Actions

Les tâches s'exécutent automatiquement selon les planifications quotidiennes suivantes (Heure de Paris) :
* 📅 **08h00 :** Envoi du Défi TOEIC Matin (`toeic_morning.yml`)
* 📅 **09h00 :** Premier envoi de la Veille Techno (`cyber_watch.yml`)
* 📅 **20h00 :** Envoi du Défi TOEIC Soir (`toeic_evening.yml`)
* 📅 **23h05 :** Deuxième envoi de la Veille Techno (`cyber_watch.yml`)
