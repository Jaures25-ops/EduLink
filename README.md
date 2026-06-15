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
