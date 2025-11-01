# DailyWorkTime

Applicazione fullstack (Backend + Frontend) per tracciare le ore di lavoro quotidiane.

Questo repository contiene due cartelle principali:

- `Backend` — server Node.js/TypeScript (TypeORM, Express)
- `Frontend` — applicazione Vue 3 con Vite

## Quick start (Docker Compose)

Assicurati di avere Docker e Docker Compose installati e in esecuzione. Dalla root del progetto esegui:

```
# Builda le immagini e avvia i servizi in foreground
docker compose up --build

# Per avviare in background
docker compose up --build -d

# Fermare e rimuovere i container
docker compose down
```

Porte esposte (default nel `docker-compose.yml`):
- Backend: http://localhost:3000
- Frontend: http://localhost:5173

> Nota: il backend deve avere un entrypoint che avvii il server (es. `dist/index.js`). Se `Backend/src/index.ts` è vuoto, aggiungi lì il codice server prima di buildare.

## Sviluppo (locale)

Backend

```powershell
cd Backend
# usa ts-node-dev per sviluppo con reload (richiede dipendenze installate)
npm install
npm run dev # se definisci uno script dev (es. "dev": "ts-node-dev --respawn src/index.ts")
```

Frontend

```powershell
cd Frontend
npm install
npm run dev
```

## Note tecniche
- Il `Backend/Dockerfile` è multi-stage: compila TypeScript con `npx tsc` e poi esegue `node dist/index.js`.
- Il `Frontend/Dockerfile` builda l'app Vite e la serve con `nginx`.
- Se vuoi aggiungere un database (Postgres), posso aggiornare `docker-compose.yml` con un servizio `db` e volumi persistenti.

## License
Questo progetto è rilasciato sotto la licenza MIT — vedi il file `LICENSE`.