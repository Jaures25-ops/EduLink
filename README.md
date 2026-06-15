Très bonne question. En examen ou en projet, les enseignants aiment souvent voir que tu maîtrises aussi **Git et GitHub**.

# 1. PREMIÈRE CONNEXION VS CODE ↔ GITHUB

## Vérifier Git

Dans le terminal :

```bash
git --version
```

### Pourquoi ?

Vérifier que Git est installé.

Exemple :

```bash
git version 2.43.0
```

---

# 2. CONFIGURER TON NOM

Une seule fois sur ton PC :

```bash
git config --global user.name "Ngongang Jaures"
```

---

# 3. CONFIGURER TON EMAIL

Le même email que GitHub :

```bash
git config --global user.email "tonmail@gmail.com"
```

---

# 4. VÉRIFIER LA CONFIGURATION

```bash
git config --list
```

Tu dois voir :

```text
user.name=Ngongang Jaures
user.email=tonmail@gmail.com
```

---

# 5. INITIALISER GIT DANS TON PROJET

Supposons :

```text
MonProjet
│
├── front
└── api
```

Entre dans le projet :

```bash
cd MonProjet
```

Puis :

```bash
git init
```

### Pourquoi ?

Créer le dépôt Git local.

Un dossier caché est créé :

```text
.git
```

---

# 6. VOIR LES FICHIERS MODIFIÉS

```bash
git status
```

Exemple :

```text
Untracked files:
front/
api/
```

---

# 7. AJOUTER TOUS LES FICHIERS

```bash
git add .
```

### Pourquoi ?

Préparer les fichiers pour l'enregistrement.

---

# 8. FAIRE UN COMMIT

```bash
git commit -m "Premier commit"
```

### Pourquoi ?

Créer un point de sauvegarde.

---

# 9. CRÉER UN REPOSITORY SUR GITHUB

Sur GitHub :

Clique :

```text
New Repository
```

Nom :

```text
MonProjet
```

Puis :

```text
Create Repository
```

---

# 10. CONNECTER LE PROJET LOCAL AU REPO GITHUB

GitHub te donne généralement :

```bash
git remote add origin https://github.com/tonCompte/MonProjet.git
```

Exemple :

```bash
git remote add origin https://github.com/jauresnsotang/MonProjet.git
```

---

# 11. VÉRIFIER LA CONNEXION

```bash
git remote -v
```

Résultat :

```text
origin  https://github.com/...
origin  https://github.com/...
```

---

# 12. ENVOYER LE PROJET SUR GITHUB

Première fois :

```bash
git branch -M main
```

Puis :

```bash
git push -u origin main
```

---

# 13. APRÈS UNE MODIFICATION

Quand tu modifies ton projet :

Voir les changements :

```bash
git status
```

Ajouter :

```bash
git add .
```

Créer un commit :

```bash
git commit -m "Ajout route users"
```

Envoyer :

```bash
git push
```

---

# 14. RÉCUPÉRER UN PROJET GITHUB

Si le dépôt existe déjà :

```bash
git clone https://github.com/user/projet.git
```

Exemple :

```bash
git clone https://github.com/jauresnsotang/MonProjet.git
```

Git crée automatiquement :

```text
MonProjet
│
├── front
└── api
```

---

# 15. METTRE À JOUR UN PROJET

```bash
git pull
```

### Pourquoi ?

Télécharger les dernières modifications depuis GitHub.

---

# 16. IGNORER CERTAINS FICHIERS

Créer :

```text
.gitignore
```

Contenu :

```text
node_modules/
dist/
.env
```

### Pourquoi ?

Ne pas envoyer :

```text
node_modules
dist
```

sur GitHub.

---

# 17. SUPPRIMER UN REPOSITORY GITHUB

⚠️ Attention : suppression définitive.

Sur GitHub :

```text
Repository
↓
Settings
↓
Tout en bas
↓
Danger Zone
↓
Delete this repository
```

GitHub demande :

```text
nomDuCompte/nomDuRepo
```

Exemple :

```text
jauresnsotang/MonProjet
```

Puis :

```text
Delete Repository
```

---

# 18. SUPPRIMER UNIQUEMENT LE LIEN GITHUB D'UN PROJET LOCAL

Si tu veux garder le projet mais retirer GitHub :

```bash
git remote remove origin
```

Vérification :

```bash
git remote -v
```

Plus rien ne s'affiche.

---

# MÉMO EXAMEN GIT / GITHUB

```bash
# Initialiser Git
git init

# Voir état
git status

# Ajouter fichiers
git add .

# Commit
git commit -m "message"

# Connecter GitHub
git remote add origin URL

# Vérifier
git remote -v

# Envoyer première fois
git branch -M main
git push -u origin main

# Envoyer ensuite
git push

# Récupérer
git pull

# Cloner
git clone URL

# Supprimer lien GitHub
git remote remove origin
```

Si ton examen porte sur NodeJS + TypeScript + Fastify, je te conseille aussi d'apprendre par cœur les **20 commandes terminal les plus utilisées** (Node, npm, TypeScript, Git, Fastify, SQLite) sur une seule fiche A4. C'est souvent ce qui fait gagner 30 à 40 minutes pendant la composition.

Là tu raisonnes exactement comme il faut pour l'examen.

Ne cherche pas à mémoriser uniquement les commandes. Il faut savoir :

```text
QUAND ?
OÙ ?
POURQUOI ?
DANS QUEL FICHIER ?
```

Je vais te faire le guide que j'aurais donné à un étudiant ingénieur avant une composition.

# 0. CE QUE LE PROF VEUT VOIR

Quand il donne :

```text
Base de données :
- utilisateurs
- produits
- commandes

Développer une application web.
```

Il veut voir :

```text
Frontend
    ↓
Fetch
    ↓
API Fastify
    ↓
SQLite
```

---

# 1. CREATION DU PROJET

## Où ?

Dans le terminal.

## Commande

```bash
mkdir MonProjet
```

### Pourquoi ?

Créer le dossier principal.

---

Entrer dans le dossier :

```bash
cd MonProjet
```

---

Créer les sous-dossiers :

```bash
mkdir front
mkdir api
```

---

Résultat :

```text
MonProjet
│
├── front
│
└── api
```

---

# 2. INITIALISER NODE

## Se placer dans api

```bash
cd api
```

---

Commande :

```bash
npm init -y
```

### Pourquoi ?

Créer :

```text
package.json
```

C'est le cerveau du projet.

Il contient :

```json
{
  "name":"api",
  "version":"1.0.0"
}
```

et la liste des dépendances.

---

# 3. INSTALLER TYPESCRIPT

Commande :

```bash
npm install -D typescript
```

---

Pourquoi ?

Pour écrire :

```ts
let age:number = 20;
```

au lieu de :

```js
let age = 20;
```

---

# 4. CREER LA CONFIG TYPESCRIPT

Commande :

```bash
npx tsc --init
```

---

Fichier créé :

```text
api
│
├── tsconfig.json
```

---

Modifier :

```json
{
  "rootDir":"./src",
  "outDir":"./dist"
}
```

---

Pourquoi ?

```text
src  -> contient ton code TS
dist -> contient le JS généré
```

---

# 5. CREER LE DOSSIER SRC

Commande :

```bash
mkdir src
```

---

Créer :

```text
src
│
└── index.ts
```

---

# 6. PREMIER CODE

Fichier :

```text
src/index.ts
```

Code :

```ts
console.log("Bonjour");
```

---

# 7. TRANSPILER

Commande :

```bash
npx tsc
```

---

Pourquoi ?

Transforme :

```ts
index.ts
```

en

```js
index.js
```

---

Résultat :

```text
dist
│
└── index.js
```

---

# 8. EXECUTER

Commande :

```bash
node dist/index.js
```

---

Pourquoi ?

Node exécute uniquement du JavaScript.

Jamais du TypeScript.

---

# 9. INSTALLER FASTIFY

Commande :

```bash
npm i fastify
```

---

Pourquoi ?

Créer une API.

---

# 10. CREER LE SERVEUR

Fichier :

```text
src/index.ts
```

Code :

```ts
import Fastify from "fastify";

const fastify = Fastify();

fastify.listen({
    port:8080
});
```

---

Pourquoi ?

Créer le serveur.

---

# 11. CREER UNE ROUTE

Toujours dans :

```text
src/index.ts
```

```ts
fastify.get("/", (request, reply)=>{

    reply.send("Bonjour");

});
```

---

Quand l'utilisateur tape :

```text
localhost:8080
```

il reçoit :

```text
Bonjour
```

---

# 12. INSTALLER SQLITE

Commande :

```bash
npm i better-sqlite3
```

---

Types :

```bash
npm i -D @types/better-sqlite3
```

---

Pourquoi ?

Parler avec la base.

---

# 13. CREER DOSSIER DATABASE

```bash
mkdir database
```

---

Résultat :

```text
database
│
└── db.sqlite
```

---

# 14. CONNECTER SQLITE

Dans :

```text
src/index.ts
```

```ts
import Sqlite3 from "better-sqlite3";

const db =
new Sqlite3("./database/db.sqlite");
```

---

Pourquoi ?

Connexion à la base.

---

# 15. GET TYPE EXAMEN

## Sujet

```text
Afficher la liste des étudiants
```

---

Route :

```ts
fastify.get("/students",
(req, reply)=>{

    const query =
    db.prepare(
    "SELECT * FROM students"
    );

    const students =
    query.all();

    reply.send(students);

});
```

---

# 16. GET PAR ID

Sujet :

```text
Afficher un étudiant
```

---

```ts
fastify.get(
"/students/:id",

(req, reply)=>{

 const { id } =
 req.params as {id:string};

 const query =
 db.prepare(
 "SELECT * FROM students WHERE id=?"
 );

 const student =
 query.get(id);

 reply.send(student);

});
```

---

# 17. POST TYPE EXAMEN

Sujet :

```text
Ajouter un étudiant
```

---

```ts
fastify.post(
"/students",

(req, reply)=>{

 const {
    nom,
    email
 } =
 req.body as {
    nom:string,
    email:string
 };

 const query =
 db.prepare(`
 INSERT INTO students
 (nom,email)
 VALUES (?,?)
 `);

 query.run(
    nom,
    email
 );

 reply.code(201).send();

});
```

---

# 18. PUT TYPE EXAMEN

Sujet :

```text
Modifier étudiant
```

---

```ts
fastify.put(
"/students/:id",

(req, reply)=>{

 const {id} =
 req.params as {id:string};

 const {nom} =
 req.body as {nom:string};

 const query =
 db.prepare(`
 UPDATE students
 SET nom=?
 WHERE id=?
 `);

 query.run(
 nom,
 id
 );

 reply.send();

});
```

---

# 19. DELETE TYPE EXAMEN

Sujet :

```text
Supprimer étudiant
```

---

```ts
fastify.delete(
"/students/:id",

(req, reply)=>{

 const {id} =
 req.params as {id:string};

 const query =
 db.prepare(`
 DELETE FROM students
 WHERE id=?
 `);

 query.run(id);

 reply.send();

});
```

---

# 20. CORS

Erreur classique :

```text
Access-Control-Allow-Origin
```

---

Installer :

```bash
npm i @fastify/cors
```

---

Dans :

```ts
import cors from "@fastify/cors";

fastify.register(cors);
```

---

Pourquoi ?

Autoriser :

```text
front
 ↓
api
```

à communiquer.

---

# 21. FETCH FRONTEND

Dans :

```text
front/js/main.js
```

---

GET :

```js
const response =
await fetch(
"http://localhost:8080/students"
);

const data =
await response.json();
```

---

POST :

```js
await fetch(
"http://localhost:8080/students",
{
 method:"POST",

 headers:{
  "Content-Type":
  "application/json"
 },

 body:JSON.stringify({
   nom:"Jaures",
   email:"test@gmail.com"
 })
});
```

---

# CE QUE TU DOIS RETENIR POUR LA COMPOSITION

Quand tu vois une table :

```sql
students
```

Tu sais immédiatement faire :

```text
GET /students

GET /students/:id

POST /students

PUT /students/:id

DELETE /students/:id
```

Quand tu vois :

```sql
orders.user_id
→ users.id
```

Tu sais immédiatement qu'il faut une :

```sql
INNER JOIN
```

Quand tu vois :

```text
Frontend
```

Tu penses :

```js
fetch()
```

Quand tu vois :

```text
Backend
```

Tu penses :

```ts
fastify.get()
fastify.post()
fastify.put()
fastify.delete()
```

Quand tu vois :

```text
Base de données
```

Tu penses :

```ts
db.prepare()
query.all()
query.get()
query.run()
```

Si tu maîtrises ce schéma mental, tu peux reconstruire presque toute l'épreuve même sous pression.
