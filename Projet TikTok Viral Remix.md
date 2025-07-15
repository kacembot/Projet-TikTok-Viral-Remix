# Projet TikTok Viral Remix

## 1. Description
Automatisation complète du scraping et remix viral de vidéos football sur TikTok, avec montage de 30 s et publication sur Discord (fallback Telegram).
## 2. Plan d’exécution rapide

1. Préparation locale  
2. Création du repo GitHub  
3. Liaison et déploiement Railway  
4. Import du workflow n8n  
5. Test opérationnel (envoi d’un prompt)  
6. Monitoring & alertes

## 3. Architecture
- n8n orchestration (Docker Compose sur Railway)
- Services dans `docker-compose.yml` :
  - n8n (+ FFmpeg, PySceneDetect)
  - Redis pour queue
- Service Python (MoviePy + OpenCV) sur Railway pour rendu viral

## 4. Fichiers du dépôt
tiktok-workflow/
├── docker-compose.yml
├── Dockerfile              # n8n + FFmpeg + PySceneDetect
├── render.py               # service Python MoviePy
├── workflow.json           # définition JSON du workflow n8n
├── README.md               # documentation principale
└── .env.example            # DISCORD_BOT_TOKEN, TELEGRAM_BOT_TOKEN, DISCORD_CHANNEL_ID, TELEGRAM_CHAT_ID

## 5. Workflow n8n
1. Webhook Trigger reçoit `prompt` libre
2. Fetch Top 24 h / 7 j / 30 j via `tiktok-scraper`
3. Merge Results par ID
4. Download Videos
5. PySceneDetect détecte cuts/transitions
6. MoviePy Render (service Python HTTP) assemble et applique effets viraux
7. Post to Discord (node Discord)
8. If Discord Fails → Post to Telegram (node Telegram)

## 6. Agents GPT recommandés
| Fonction                              | Agent GPT                  |
| ------------------------------------- | -------------------------- |
| Supervision globale                   | ULTRA_TIKTOK_CEREBRUM      |
| Orchestration Docker & CI/CD          | ULTRA_DEVOPS_COORDINATOR   |
| Audit & mapping du workflow n8n       | ULTRA_WORKFLOW_AUDITOR     |
| Monitoring logs & alertes             | ULTRA_MONITOR_GUARDIAN     |
| Montage vidéo & effets viraux         | ULTRA_MEDIA_ENGINEER       |
| Analyse données & scoring viral       | ULTRA_DATA_INSIGHTER       |
| Création et ajustement de prompts     | ULTRA_PROMPT_ENGINEER      |
| Documentation et guides               | ULTRA_DOC_ENGINE           |

## 7. Mise en place locale
1. Clone ce repo en local.
2. Duplique `.env.example` → `.env` et remplis tes secrets.
3. Place `workflow.json` (export n8n) à la racine.
4. Lance :
   ```bash
   docker-compose up --build -d
   ```
5. Va dans n8n UI → Settings → Workflows → Import from clipboard → colle le contenu de `workflow.json`

## 8. Déploiement Railway
1. Push sur GitHub (branche main)
2. Lie ton repo à Railway
3. Dans Railway Dashboard, configure les variables d’environnement
4. Railway build & déploie automatiquement n8n + service Python + Redis

## 9. Présentation des Agents GPT
Chaque agent GPT spécialisé apporte une expertise pointue :
- ULTRA_TIKTOK_CEREBRUM : supervision globale, oriente vers le bon agent à chaque étape
- ULTRA_DEVOPS_COORDINATOR : initialise dossier, fichiers, GitHub & CI/CD
- ULTRA_WORKFLOW_AUDITOR : audite et importe le JSON n8n, valide la structure
- ULTRA_MONITOR_GUARDIAN : configure logs & alertes sur Discord/Telegram
- ULTRA_MEDIA_ENGINEER : teste et ajuste FFmpeg, PySceneDetect & MoviePy
- ULTRA_DATA_INSIGHTER : définit KPIs, met en place dashboard
- ULTRA_PROMPT_ENGINEER : affine le prompt TikTok pour viralité max
- ULTRA_DOC_ENGINE : maintien et mise à jour de la documentation
