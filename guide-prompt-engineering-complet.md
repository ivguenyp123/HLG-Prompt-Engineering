# Guide Complet du Prompt Engineering
## De Débutant Absolu à Expert Tech

**Pour qui ?** Ce guide s'adresse à des débutants complets en prompting, qui évoluent vers des métiers de l'informatique (développeur, DevOps, Tech Lead, Data Engineer, etc.) et qui ont besoin de maîtriser l'IA comme outil de travail quotidien.

**Durée estimée :** 20-40 heures de pratique pour atteindre un niveau expert

---

## 📚 Table des Matières

1. [Introduction](#introduction)
2. [Niveau 1 : Fondamentaux](#niveau-1)
3. [Niveau 2 : Bases Solides](#niveau-2)
4. [Niveau 3 : Intermédiaire](#niveau-3)
5. [Niveau 4 : Avancé](#niveau-4)
6. [Niveau 5 : Expert Tech](#niveau-5)
7. [Niveau 6 : Pro DevOps](#niveau-6)
8. [Cas d'Usage Réels](#cas-usage)
9. [Erreurs Courantes](#erreurs)
10. [Exercices Pratiques](#exercices)
11. [Intégration Workflow](#workflow)
12. [Ressources & Conclusion](#ressources)

---

## Introduction {#introduction}

### Qu'est-ce qu'un Prompt ?

Un **prompt**, c'est le texte que tu donnes à une IA pour lui demander quelque chose. C'est ton instruction, ta demande.

**Analogie :** L'IA est un collègue super compétent mais nouveau dans ton équipe. Il ne connaît pas tes conventions de code, tes contraintes projet, ton architecture. Le prompt, c'est ta façon de lui expliquer le contexte et ce que tu attends.

### Pourquoi c'est Critique en Tech ?

L'IA devient un outil quotidien pour :
- Générer du code (boilerplate, tests, scripts)
- Debugger (analyser logs, identifier bugs)
- Documenter (README, API docs)
- Automatiser (pipelines CI/CD)
- Architecturer (design patterns, choix tech)

**Exemple concret de la différence :**

```
❌ Prompt débutant : "Crée un script Python"
→ Résultat : Script générique inutilisable

✅ Prompt expert : "Crée un script Python 3.11+ qui lit un CSV avec 
pandas, valide le schéma (colonnes: name, email, date), nettoie les 
emails (lowercase), exporte en JSON ISO 8601, avec logs structurés, 
type hints, docstrings Google style, et tests pytest pour 3 cas."
→ Résultat : Code production-ready
```

### Progression en 6 Niveaux

1. **Fondamentaux** : Structure de base d'un prompt
2. **Bases Solides** : Role-playing, contexte, exemples
3. **Intermédiaire** : Prompts structurés, chaînage
4. **Avancé** : Décomposition, meta-prompting
5. **Expert Tech** : Architecture, code review, optimisation
6. **Pro DevOps** : CI/CD, IaC, monitoring, incident response

---

## Niveau 1 : Fondamentaux {#niveau-1}

### 1.1 Structure de Base (Les 4 Piliers)

Tout prompt efficace contient :

1. **CONTEXTE** : Qui ? Quoi ? Pourquoi ? Dans quel environnement ?
2. **TÂCHE** : Que veux-tu exactement ?
3. **CONTRAINTES** : Limites, standards, format, outils
4. **FORMAT** : Comment présenter le résultat

**Exemple Décomposé :**

```
[CONTEXTE] 
Je travaille sur une API REST en Node.js avec Express.
Notre équipe utilise JWT pour l'authentification.

[TÂCHE] 
Crée un middleware d'authentification JWT.

[CONTRAINTES]
- Node.js 18+, Express 4.x
- Library: jsonwebtoken
- Gestion d'erreurs avec try/catch
- Secret JWT dans variable d'environnement

[FORMAT] 
Code complet avec imports, fonction middleware commentée, 
exemple d'utilisation sur une route, gestion des 3 cas : 
token valide, invalide, absent.
```

### 1.2 Règle d'Or : Spécificité

❌ **Vague :** `Crée un script bash`

✅ **Spécifique :**
```
Crée un script bash qui :
- Vérifie si Docker est installé (command -v docker)
- Si absent : affiche erreur et exit 1
- Si présent : affiche la version
- Teste si daemon Docker tourne (docker ps)
- Utilise couleurs (vert=OK, rouge=erreur)
- Ajoute en-tête avec date/heure
```

**Checklist de Spécificité :**
- [ ] Versions mentionnées ?
- [ ] Contraintes techniques explicites ?
- [ ] Format de sortie défini ?
- [ ] Cas d'erreur considérés ?
- [ ] Standards précisés ?

### 1.3 Verbes d'Action

**Pour Créer :** crée, génère, développe, implémente, code

**Pour Analyser :** analyse, identifie, diagnostique, debug, trouve

**Pour Transformer :** refactorise, optimise, convertis, migre

**Pour Expliquer :** explique, documente, commente, détaille

**Pour Comparer :** compare, évalue, benchmark, critique

**Pour Tester :** teste, valide, vérifie, simule

### 1.4 Template de Démarrage

```
CONTEXTE :
[Ton rôle, projet, stack technique, contraintes]

TÂCHE :
[Ce que tu veux précisément]

CONTRAINTES :
- [Langage/version]
- [Outils/frameworks]
- [Standards/conventions]
- [Limites/restrictions]

FORMAT ATTENDU :
[Structure de la réponse souhaitée]
```

**Exercice Pratique :**

Améliore ce prompt : `Crée un Dockerfile`

**Solution :**
```
CONTEXTE : App Node.js 18, Express, npm, port 3000

TÂCHE : Crée un Dockerfile optimisé production

CONTRAINTES :
- Image alpine pour taille minimale
- Multi-stage build
- Layer caching optimisé (COPY package*.json avant COPY .)
- User non-root pour sécurité
- Healthcheck sur /health
- Variables d'env : NODE_ENV, PORT

FORMAT : Dockerfile complet + commentaires expliquant chaque section
```

---

## Niveau 2 : Bases Solides {#niveau-2}

### 2.1 Role-Playing

Assigner un rôle change radicalement la qualité.

❌ **Sans rôle :**
```
Comment améliorer les performances de ma DB ?
```

✅ **Avec rôle contextualisé :**
```
Tu es un DBA senior PostgreSQL avec 10 ans d'expérience sur des 
apps >10M requêtes/jour.

Ma table users (50M lignes) a des SELECT lents (>2s) sur la colonne 
email. Pas d'index dessus. Traffic : 5000 req/s en pic.

Propose 3 solutions par ordre de priorité avec :
- Implémentation SQL concrète
- Impact attendu
- Risques et précautions
- Temps de mise en œuvre
```

### 2.2 Contexte Technique Riche

Plus de contexte = meilleure réponse.

**Contexte Riche :**
```
STACK : Node.js 18, Express, MongoDB 6.0, Docker sur AWS ECS
PROBLÈME : GET /users/:id retourne en 1.5s (objectif < 200ms)
OBSERVATIONS :
- Pas de cache
- Logs : query Mongo prend 1.2s
- Modèle User a 15 champs, on en utilise 5
- 2M documents
- Pas d'index sur _id

CONTRAINTES : Pas de budget infra, deploy weekend only

Propose un plan d'optimisation étape par étape avec impact estimé.
```

**Checklist du Bon Contexte :**
- [ ] Versions exactes
- [ ] Métriques actuelles
- [ ] Objectifs chiffrés
- [ ] Contraintes (temps, budget, compatibilité)
- [ ] Ce qui a été tenté

### 2.3 Few-Shot Prompting (Exemples)

Montre des exemples de ce que tu veux.

```
Je veux des tests Jest pour mes fonctions JavaScript. Voici le style :

EXEMPLE 1 :
describe('calculateTotal', () => {
  it('should return sum of positive numbers', () => {
    expect(calculateTotal([1, 2, 3])).toBe(6);
  });
  
  it('should return 0 for empty array', () => {
    expect(calculateTotal([])).toBe(0);
  });
});

EXEMPLE 2 :
describe('validateEmail', () => {
  it('should accept valid email', () => {
    expect(validateEmail('test@example.com')).toBe(true);
  });
});

Maintenant, crée des tests dans ce style pour :

function findUserById(users, id) {
  return users.find(user => user.id === id) || null;
}

Couvre : utilisateur trouvé, ID inexistant, tableau vide, ID null.
```

### 2.4 Chain of Thought (Raisonnement Étape par Étape)

Demande à l'IA de décomposer.

```
Mon conteneur Docker ne démarre pas :
"exec user process caused: exec format error"

Analyse en suivant ces étapes :

1. IDENTIFIER : Que signifie cette erreur ?
2. CAUSES : Liste 5 causes potentielles
3. DIAGNOSTIC : Pour chaque cause, donne une commande de vérification
4. SOLUTION : Propose une solution pour la cause la plus probable
5. PRÉVENTION : Comment éviter ça à l'avenir ?

Détaille ton raisonnement.
```

### 2.5 Itération

Ton premier prompt n'est jamais le meilleur.

```
Itération 1 : "Crée un script Python de scraping"
→ Trop générique

Itération 2 : "Script Python qui scrape les titres sur 
https://news.ycombinator.com avec BeautifulSoup"
→ Mieux mais pas de gestion d'erreurs

Itération 3 : "Le script précédent est bien, mais ajoute :
- Timeout 10s avec retry 3 fois
- Sauvegarde en CSV avec date
- User-Agent personnalisé
- Logging niveau INFO"
→ Production-ready ✅
```

### 2.6 Contraintes Explicites

Définis ce que tu NE veux PAS.

```
Crée une fonction JS de validation de mot de passe.

RÈGLES :
- Min 8 caractères
- 1 majuscule, 1 minuscule, 1 chiffre, 1 spécial

CONTRAINTES :
- Pas de regex compliquée (je veux comprendre)
- Pas de librairie externe
- Pas de eval()
- Code commenté ligne par ligne

FORMAT :
- Fonction pure, return boolean
- Objet détails avec règles cassées si invalide
- Tests unitaires simples
```

---

## Niveau 3 : Intermédiaire {#niveau-3}

### 3.1 Prompts Structurés avec Délimiteurs

Utilise XML-like ou Markdown pour clarté.

```
<context>
Application Flask 2.3, Python 3.11, déployée sur Heroku.
Endpoint qui upload des fichiers images.
</context>

<task>
Ajoute validation pour :
1. Vérifier type image (JPEG, PNG, WebP)
2. Limiter à 5MB
3. Retourner 400 si validation échoue
</task>

<current_code>
```python
@app.route('/upload', methods=['POST'])
def upload_file():
    file = request.files['image']
    filename = secure_filename(file.filename)
    file.save(os.path.join(app.config['UPLOAD_FOLDER'], filename))
    return jsonify({'success': True})
```
</current_code>

<constraints>
- Utilise Pillow pour vérifier le type réel
- Ne casse pas le comportement existant
- Logs des erreurs
- Messages en français
</constraints>

<output_format>
1. Code modifié complet
2. Exemple de réponse d'erreur JSON
3. Tests curl pour cas valide et invalide
</output_format>
```

### 3.2 Persona avec Contraintes de Communication

```
Tu es un mentor backend patient et pédagogue. Tu expliques les 
concepts complexes avec des analogies simples.

Explique-moi la différence entre synchrone et asynchrone en Node.js :

1. Avec une analogie du quotidien (restaurant, poste...)
2. Avec 2 exemples de code côte à côte
3. Quand utiliser l'un ou l'autre

Maximum 300 mots. Ton amical.
```

### 3.3 Templates Réutilisables

**Template Code Review :**

```
## CODE REVIEW REQUEST

Langage : [Python/Java/JS]
Contexte : [Description du module]

Code :
```[language]
[TON CODE]
```

Points d'attention :
- [ ] Sécurité
- [ ] Performance
- [ ] Maintenabilité
- [ ] Tests

Format :
1. Score global /10
2. Points forts (2-3)
3. Points d'amélioration avec code corrigé
4. Risques identifiés
```

### 3.4 Negative Prompting

Dis ce que tu NE veux PAS.

```
Crée un endpoint Express pour créer un utilisateur.

CE QUE JE VEUX :
- Validation avec Joi
- Hash password avec bcrypt
- Return 201 avec user (sans password)

CE QUE JE NE VEUX PAS :
- Pas de MongoDB direct (on a un UserService)
- Pas de validation manuelle if/else
- Pas de password en clair dans logs
- Pas de console.log pour debug
- Pas de var, utilise const/let
```

### 3.5 Sequential Prompting

Découpe les tâches complexes.

Au lieu de : "Crée une app To-Do complète avec React, Express, Mongo, auth, tests, deploy"

Fais :

**Prompt 1 - Architecture :**
```
Je veux créer une app To-Do. Propose une architecture :
- Stack frontend
- Stack backend
- Base de données
- Authentification
- Hosting
Justifie chaque choix. Contrainte : gratuit/low-cost.
```

**Prompt 2 - Schema DB :**
```
On a choisi MongoDB. Définis le schéma Mongoose pour :
- Users (email, password, createdAt)
- Todos (title, description, completed, userId, dates)
Avec validations, index, relations.
```

**Prompt 3 - Backend Endpoints :**
```
Voici le schéma : [COLLE RÉSULTAT 2]
Crée les endpoints Express pour CRUD Todos avec auth JWT.
```

---

## Niveau 4 : Avancé {#niveau-4}

### 4.1 Context Window Management

Pour gros fichiers (2000 lignes), ne colle pas tout.

**Mauvais :** Colle 2000 lignes, "Trouve les bugs"

**Bon - Étape 1 :**
```
Voici ma structure :
src/
├── models/ (User.js 150L, Post.js 120L)
├── controllers/ (userController.js 300L ← PROBLÈME ICI)
├── routes/
└── services/

Erreurs 500 sur endpoints users. Problème semble venir de 
userController.js.

Avant de voir le code, pose-moi 5 questions pour cibler le diagnostic.
```

**Étape 2 :**
```
[APRÈS LES QUESTIONS]
Voici la fonction problématique (50 lignes seulement) :
[CODE CIBLÉ]
```

### 4.2 Meta-Prompting

Fais générer le prompt par l'IA.

```
Génère un prompt template pour créer des scripts Bash de monitoring 
système (CPU, RAM, disk, network) avec alertes.

Le template doit inclure :
- Un rôle approprié
- Sections contextuelles
- Format de sortie structuré
- Exemples few-shot
```

### 4.3 Constraint Satisfaction

Donne des contraintes contradictoires, force le compromis.

```
Crée une fonction de rate limiting pour mon API Express.

CONTRAINTES (certaines conflictuelles, trouve le meilleur équilibre) :
1. Performance : 10k req/s sans latence
2. Persistance : survivre au redémarrage
3. Simplicité : pas de dépendance si possible
4. Précision : par user, par IP, par endpoint
5. Coût : gratuit/low-cost
6. Scalabilité : multi-instance (load balancer)

Propose 2 solutions :
- Solution A : Optimisée simplicité/performance
- Solution B : Optimisée précision/scalabilité

Pour chaque : code, trade-offs, scénarios d'usage
```

### 4.4 Systematic Decomposition

Pour problèmes ultra-complexes.

```
PROBLÈME :
Migrer app monolithe PHP 5.6 (200k lignes, 10 ans) vers microservices 
Node.js/Python. Prod ne peut pas s'arrêter. 6 mois.

DÉCOMPOSITION :

1. ANALYSE :
   - Quels sont les sous-problèmes ?
   - Dépendances entre eux ?
   - Ordre de résolution optimal ?

2. PRIORISATION :
   - Par criticité, difficulté, dépendances

3. PLAN D'ACTION :
   - Pour chaque sous-problème : input, output, approche, tests

Commence par l'analyse. Ne code rien encore.
```

---

## Niveau 5 : Expert Tech {#niveau-5}

### 5.1 Architecture Decision Records (ADR)

```
# ARCHITECTURE DECISION REQUEST

## Contexte
App de messagerie temps réel.
- 50k users actifs/jour
- 500k messages/jour
- Stack : PHP monolithe + MySQL + polling HTTP/2s
- Latence messages 3-5s
- Serveurs surchargés en heures de pointe

## Problème
Migrer vers architecture temps réel performante sans tout recoder.

## Critères de Décision
1. Latence messages < 100ms (poids 10/10)
2. Coût infra < $500/mois (poids 8/10)
3. Compatibilité mobile iOS/Android (poids 9/10)
4. Effort migration < 3 mois, 2 devs (poids 7/10)
5. Scalabilité 500k users dans 2 ans (poids 8/10)

## Contraintes
- Team : 2 devs backend, 1 dev mobile
- Budget : $500/mois max
- Timeline : 3 mois
- Clients existants : compatibilité requise

## Demande
Propose 3 options architecturales avec :
1. Approche high-level (diagramme Mermaid/ASCII)
2. Trade-offs (matrice critères vs options)
3. Stack technique suggérée
4. Risques identifiés
5. Migration path depuis existant
6. Recommandation finale justifiée
```

### 5.2 Code Review Expert

```
# EXPERT CODE REVIEW

Tu es un Tech Lead senior, 15 ans d'XP. Reviews rigoureuses et constructives.

Code :
```[language]
[CODE]
```

Review Checklist (note /10 chaque catégorie) :

1. Correctness & Logic
2. Security (injection, données sensibles, validation inputs)
3. Performance (complexité algo, N+1, memory leaks)
4. Error Handling
5. Testing (testabilité)
6. Maintainability (self-documenting, fonctions < 50L, SRP)
7. Standards & Best Practices

Output :
- ✅ Approuvé / ⚠️ Avec commentaires / ❌ Changements requis
- Score global /70
- Critical Issues (bloquants)
- Major Issues
- Minor Issues
- Positives
- Suggested Refactoring
```

### 5.3 Performance Optimization

```
# PERFORMANCE OPTIMIZATION

Code :
```python
def get_user_dashboard(user_id):
    user = db.query("SELECT * FROM users WHERE id = %s", user_id)
    posts = []
    for friend_id in user['friends']:
        friend_posts = db.query("SELECT * FROM posts WHERE user_id = %s", friend_id)
        posts.extend(friend_posts)
    for post in posts:
        post['comments'] = db.query("SELECT * FROM comments WHERE post_id = %s", post['id'])
        post['likes'] = db.query("SELECT COUNT(*) FROM likes WHERE post_id = %s", post['id'])
    return {'user': user, 'posts': sorted(posts, key=lambda x: x['created_at'])[:50]}
```

Métriques actuelles :
- Temps réponse : 3.2s
- Queries DB : 250-500 par requête
- Load : 100 req/s en pic

Objectifs :
- Temps réponse < 200ms (p95)
- Queries < 10
- Supporter 1000 req/s

Profiling : 95% du temps dans queries DB

Analyse :
1. Identification Bottlenecks (top 3 par impact)
2. Quick Wins (impact élevé, effort faible)
3. Optimisations Majeures
4. Trade-offs
5. Plan d'Action Priorisé
```

### 5.4 Documentation Technique Auto-Générée

```
Génère un README.md pro pour ce projet.

Structure :

1. Titre et Badges (build, coverage, version, license)
2. Features (principales, ce qui rend unique)
3. Tech Stack (langages, frameworks, dépendances)
4. Getting Started
   - Prerequisites
   - Installation (step-by-step)
   - Configuration (env vars)
   - Running (dev, prod, tests)
5. Usage (exemples de code, screenshots si pertinent)
6. Architecture (diagramme Mermaid, explication composants)
7. Development
   - Project Structure (tree commenté)
   - Running Tests
   - Code Style
8. Deployment
9. Contributing
10. License
11. Contact/Support

Format : Markdown propre, prêt à commit.
```

---

## Niveau 6 : Pro DevOps {#niveau-6}

### 6.1 CI/CD Pipeline Generation

```
# CI/CD PIPELINE REQUEST

Project :
- Lang/Framework : Node.js 18, Express
- Tests : Jest, coverage > 80%
- Build : TypeScript compile
- Deploy : AWS ECS
- Environments : dev, staging, prod

Platform : GitLab CI

Requirements :

Triggers :
- Push sur branches
- MR
- Tags v*.*.*

Stages : lint → test → build → security → deploy-dev → deploy-staging → deploy-prod

Quality Gates :
- Coverage > 85%
- Linting : zero errors
- Security : no CRITICAL
- Build : successful

Deployments :
- Dev : auto sur develop
- Staging : auto sur main
- Prod : manuel via tag + approval

Notifications : Slack #deploys

Caching : dependencies, Docker layers

Secrets : GitLab CI variables

Contraintes :
- Pipeline < 8 min
- Zero-downtime deploy (blue-green)
- Auto-rollback si healthcheck fail 3x

Output :
1. .gitlab-ci.yml complet
2. Scripts si nécessaires
3. Doc des secrets à configurer
4. Procédure rollback
5. Troubleshooting guide
```

### 6.2 Infrastructure as Code

```
# IaC REQUEST

Goal : Deploy scalable web app avec database

Cloud : AWS
Tool : Terraform

Components :
- Compute : ECS Fargate, auto-scaling
- Networking : VPC, subnets (public/private), ALB, security groups
- Storage : RDS PostgreSQL, S3
- Monitoring : CloudWatch, alerting

Requirements :
- Environment : prod
- HA : yes, multi-AZ
- DR : backup daily, RTO/RPO < 1h
- Budget : < $500/month
- Compliance : GDPR

Output :
1. Main .tf files (modularized)
2. Variables file with doc
3. Outputs (endpoints, connection strings)
4. README (prerequisites, deploy, destroy, cost estimation)
5. State management strategy
```

### 6.3 Observability Stack

```
# OBSERVABILITY STACK

App : Microservices, Node.js + Python, Kubernetes
Traffic : 1000 req/min (3000 en pic)

Requirements :

Metrics (System + Business) :
- System : CPU, RAM, request rate, latency (p50/p95/p99), error rate
- Business : orders/hour, signups/day, conversion funnel

Logging :
- Structured JSON logs
- Levels : DEBUG, INFO, WARN, ERROR
- Correlation IDs pour tracing
- Retention : 30 jours

Tracing :
- End-to-end request tracing
- Service dependency map

Alerting :
- Critical : service down, error rate >5%, latency >1s p95
- Warning : autres conditions

Dashboards :
- Health overview
- Per-service deep dive
- Business metrics

Tech Stack : Prometheus + Loki + Jaeger + Grafana

Output :
1. Architecture (Mermaid diagram)
2. Config files (Prometheus, Fluentd, Jaeger)
3. Instrumentation code (exemples par langage)
4. Alerting rules
5. Dashboard templates JSON
6. Runbook (interpréter métriques et alertes)
```

### 6.4 Runbook Template

```
# RUNBOOK: [SERVICE NAME]

Service Description :
- Purpose : [À quoi sert ce service]
- Dependencies : [Services/DBs/APIs]
- SLA : [99.9% uptime, latency < 200ms]

Architecture : [Mermaid diagram]

Key Metrics :
| Metric | Normal | Warning | Critical |
|--------|---------|---------|----------|
| Request Rate | 100-500 | <50 ou >1000 | <10 ou >2000 |
| Latency p95 | <200ms | >500ms | >1000ms |

---

## INCIDENT RESPONSE

### 1. Service is Down (HTTP 5xx)

Symptoms : Healthcheck failing, 500s, alertes

Immediate Actions (< 5 min) :
1. Check pods : kubectl get pods -n prod
2. Check recent deploys : git log -10
3. If recent deploy : Rollback
   ```
   kubectl rollout undo deployment/[name] -n prod
   ```
4. Check logs : kubectl logs -f deployment/[name]

Investigation (< 15 min) :
- External dependencies (DB, Redis, APIs)
- Resource constraints (OOMKilled?)
- Recent config changes

Escalation (if not resolved in 15 min) :
- Primary : @tech-lead (Slack/Phone)
- Secondary : @senior-dev

Communication Template :
```
🚨 INCIDENT - [Service] DOWN
Status: Investigating
Impact: [User impact]
Started: [Time]
Actions: [List]
Next update: 15 min
```

---

### 2. High Latency

[Similar structure]

---

## Useful Commands

Check Health : `curl https://[service]/health`
Tail Logs : `[command]`
DB Connection : `[command]`
Metrics Dashboard : [Link]

---

## Postmortem Template

```markdown
# Postmortem: [Incident]

Summary : [One paragraph]

Impact :
- Duration : [start - end]
- Affected users : [%]

Root Cause : [Detailed]

Timeline :
- HH:MM - [Event]

Resolution : [What fixed it]

Action Items :
- [ ] [Action 1] - Owner: @name - Due: date
```
```

### 6.5 Secrets Management Audit

```
# SECRETS AUDIT

Current State :

Inventory (tous les endroits où des secrets existent) :
- [ ] Code source (git history)
- [ ] Config files (.env)
- [ ] CI/CD variables
- [ ] Container env vars
- [ ] Kubernetes secrets
- [ ] Developer machines
- [ ] Documentation
- [ ] Logs

Secret Types :
- DB credentials
- API keys
- JWT signing keys
- Encryption keys
- SSL/TLS certs

Risk Assessment (pour chaque secret) :
- Exposure : où stocké ? qui y accède ?
- Impact : si compromis ?
- Rotation : dernier changement ?

---

Remediation Plan :

Phase 1 (< 24h) :
1. Scan git history (truffleHog, gitleaks)
2. Rotate exposed secrets
3. Remove secrets from code

Phase 2 (< 1 week) :
1. Implement tool (Vault, AWS Secrets Manager, etc.)
2. Migrate secrets
3. Update CI/CD
4. Document process

Phase 3 (< 1 month) :
1. Rotation policy (DB: 90d, API keys: 180d)
2. Monitoring (alert on unauthorized access)
3. Developer training

---

Implementation :
[Config détaillée de l'outil]

Code Changes :
```language
// Before
const DB_PASSWORD = "hardcoded";

// After
const DB_PASSWORD = await secretsManager.getSecret("db-password");
```

Validation :
- [ ] No secrets in git
- [ ] All secrets in management tool
- [ ] Access logged
- [ ] Rotation enforced
```

---

## Cas d'Usage Réels {#cas-usage}

### 7.1 Migration de Technologie

```
# MIGRATION PLAN: [OLD TECH] → [NEW TECH]

Executive Summary :
- What : [Description]
- Why : [Raisons business/tech]
- When : [Timeline]
- Risk : [Low/Medium/High]

Current State :
- Tech Stack : [Details]
- Scale : [Métriques]
- Pain Points : [Liste]

Target State :
- New Stack : [Details]
- Benefits : [Avec métriques]

Migration Strategy : Strangler Fig (3 mois)

Phase 1 - Preparation (2 weeks) :
- Setup new stack en parallèle
- Dual-write adapter
- Feature flags
- Monitoring

Phase 2 - Shadow Mode (2 weeks) :
- Route copy traffic (no user impact)
- Compare responses
- Fix discrepancies

Phase 3 - Canary (2 weeks) :
- 5% → 25% → 50% traffic

Phase 4 - Full Migration (2 weeks) :
- 100% traffic

Phase 5 - Cleanup (2 weeks) :
- Remove feature flags
- Remove old code

Risk Management :
| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| Data loss | Low | CRITICAL | Dual-write, backups |

Success Metrics :
- Zero data loss
- Downtime < 5 min total
- Performance improved by X%
```

### 7.2 Incident Postmortem

```
# Postmortem: [Incident Title]

Date : 2024-11-18
Authors : [@name1, @name2]
Severity : SEV-1

---

Summary : [2-3 phrases pour non-tech stakeholders]

TL;DR :
- What broke : [Service]
- Impact : X users, Y minutes
- Root cause : [One sentence]
- Fix : [One sentence]

---

Impact :

User Impact :
- Affected : X% users (N users)
- Duration : [Start] to [End] (N min)
- Symptoms : [Ce que users ont vécu]

Business Impact :
- Revenue : ~$X lost
- SLA : Breached [if applicable]

---

Timeline (UTC) :

| Time | Event |
|------|-------|
| 14:23 | 🔴 Deployment v2.4.0 started |
| 14:26 | ⚠️ Error spike 0.1% → 15% |
| 14:27 | 🚨 PagerDuty alert |
| 14:28 | 👀 @alice investigating |
| 14:35 | 🔍 Identified: DB migration broke FK constraints |
| 14:38 | 🔄 Rollback decision |
| 14:43 | ✅ Service recovered |

Total : 20 min

---

Root Cause Analysis (5 Whys) :

1. Why did service fail ? → DB queries errored
2. Why did queries fail ? → FK constraint violations
3. Why violations ? → Migration added FK, data had orphaned records
4. Why orphaned records ? → Previous bug allowed it
5. Why didn't we catch ? → Staging DB was clean

Root Cause : Migration conflicted with dirty data. Staging ≠ prod data quality.

---

What Went Well 👍 :
1. Fast detection (3 min)
2. Clear ownership
3. Successful rollback

What Went Wrong 👎 :
1. No data validation before migration
2. Staging parity issue
3. No gradual rollout

---

Action Items :

Immediate (This Week) :
- [ ] Clean orphaned data - @bob - Nov 20
- [ ] Test rollback - @alice - Nov 21

Short-term (This Month) :
- [ ] Pre-migration validation script - @charlie - Nov 30
- [ ] Improve staging data - @david - Dec 5
- [ ] Canary for DB changes - @alice - Dec 10

Long-term (Next Quarter) :
- [ ] Automated data quality checks - @emily - Jan 15
- [ ] Migration risk scoring - @frank - Jan 30

---

Lessons Learned :
1. Always validate data before adding constraints
2. Staging must mirror prod data characteristics
3. DB changes need gradual rollout too

---

Postmortem reviewed by : @tech-lead, @vp-eng
Date finalized : 2024-11-20
```

---

## Erreurs Courantes {#erreurs}

### Erreur 1 : Prompt Trop Vague

❌ `Aide-moi à coder`

✅ Solution : Ajoute contexte, tâche précise, contraintes, format

### Erreur 2 : Contexte Insuffisant

❌ `Mon code ne marche pas`

✅ Solution : Donne stack, code, erreur, environnement, ce qui a été tenté

### Erreur 3 : Demander Trop en Une Fois

❌ `Crée une app e-commerce complète avec tout`

✅ Solution : Décompose en 5-10 prompts séquentiels

### Erreur 4 : Oublier les Contraintes

❌ `Crée un script de backup`

✅ Solution : Précise versions, format, sécurité, gestion erreurs

### Erreur 5 : Ne Pas Itérer

❌ [Reçoit réponse imparfaite] "Bon, ça ira..."

✅ Solution : TOUJOURS itérer 2-3 fois minimum

### Erreur 6 : Copier-Coller Sans Comprendre

❌ [Copie code IA] [Colle direct en prod] [💥]

✅ Solution : Checklist avant utilisation :
- [ ] Je comprends chaque ligne
- [ ] Testé localement
- [ ] Edge cases vérifiés
- [ ] Adapté à mon contexte
- [ ] Tests ajoutés

### Erreur 7 : Ignorer les Bonnes Pratiques

❌ `Crée un endpoint` → [Code sans validation, sans tests]

✅ Solution : Toujours demander code "production-ready" avec validation, logs, tests, doc

### Erreur 8 : Versions Vagues

❌ `Crée un Dockerfile` → [Reçoit Python 3.7, ton app = 3.11]

✅ Solution : TOUJOURS préciser versions exactes

### Erreur 9 : Négliger la Performance

❌ `Filtre des users` → [Code O(n²)]

✅ Solution : Mentionne le scale dès le début

### Erreur 10 : Oublier la Maintenance

❌ [Code sans doc, sans tests]

✅ Solution : Pense long terme, demande doc + tests + exemples

---

## Exercices Pratiques {#exercices}

### Débutant (30 min)

Transforme ces prompts faibles :

1. `Écris du code Java`
2. `Mon API est lente`
3. `Aide avec Docker`
4. `Explique Git`

### Intermédiaire (1h)

Crée un template réutilisable pour une tâche que tu fais souvent.

### Avancé (2h)

Bug en production : app crashe de façon intermittente. Crée une série de 5-7 prompts pour diagnostiquer.

### Expert (4-6h)

Conçois l'architecture d'une plateforme de streaming vidéo (mini-YouTube) via prompting uniquement. Livrables : ADR, diagramme, stack justifiée, estimation coûts, plan de migration.

---

## Intégration Workflow {#workflow}

### Dans l'IDE

```typescript
/**
 * Sort User objects by multiple criteria with priority
 * 
 * Requirements:
 * - Primary: status (active > inactive > suspended)
 * - Secondary: created_at (newest first)
 * - Tertiary: name (alphabetical)
 * - Immutable (don't modify original)
 * - Performance: O(n log n)
 */
function sortUsersByPriority(users: User[]): User[] {
  // L'IA complète ici
}
```

### Code Review Avant PR

```
Fais une code review rigoureuse.

CONTEXT : [Feature description]
STACK : [Technologies]

CODE :
[Files]

REVIEW : Security, Correctness, Performance, Maintainability, Testing, Style

FORMAT : CRITICAL/MAJOR/MINOR issues, code corrigé, score /10
```

### Debugging Workflow

**Étape 1 - Collecte :**
```
Je dois debugger [problème]. Dis-moi quelles infos tu as besoin.
```

**Étape 2 - Analyse :**
[Fournis les infos demandées]

**Étape 3 - Solutions :**
```
Propose 3 solutions possibles avec probabilité de succès pour chaque.
```

**Étape 4 - Implémentation :**
```
On essaie la solution 1. Donne-moi le code/commandes exactes.
```

---

## Ressources & Conclusion {#ressources}

### Progression Recommandée

**Semaine 1-2 : Fondamentaux**
- Pratique structure 4 piliers
- Ajoute contraintes systématiquement
- Utilise role-playing

**Semaine 3-4 : Intermédiaire**
- Templates réutilisables
- Sequential prompting
- Few-shot learning

**Mois 2 : Avancé**
- Meta-prompting
- Systematic decomposition
- Context window management

**Mois 3+ : Expert**
- ADR via prompting
- Pipelines CI/CD complets
- Optimisations complexes

### Checklist du Prompt Parfait

- [ ] Contexte complet (stack, versions, scale)
- [ ] Tâche précise et non ambiguë
- [ ] Contraintes explicites (tech + business)
- [ ] Format de sortie défini
- [ ] Exemples si pattern spécifique
- [ ] Gestion d'erreurs mentionnée
- [ ] Standards/best practices précisés

### Principe d'Or

**"Un prompt expert, c'est comme une spec technique complète : quelqu'un qui ne connaît pas le projet doit pouvoir tout comprendre et implémenter."**

### Pour Aller Plus Loin

- Expérimente quotidiennement
- Itère toujours (minimum 2-3 fois)
- Crée ta bibliothèque de templates
- Partage avec ton équipe
- Adapte les techniques à ton domaine

### Conclusion

Le prompt engineering n'est pas de la "magie" - c'est une compétence technique qui s'apprend et se pratique. Plus tu es précis, structuré, et contextuel, meilleurs seront tes résultats.

**L'IA est ton collègue super compétent. Traite-le comme tel : donne-lui le contexte complet, les contraintes claires, et les attentes précises. Tu ne serais pas vague avec un humain - ne le sois pas avec une IA.**

Bon prompting ! 🚀

---

**Version :** 1.0  
**Dernière mise à jour :** Novembre 2024  
**License :** Creative Commons BY-SA 4.0  
**Contribuer :** [Tes retours sont les bienvenus]

