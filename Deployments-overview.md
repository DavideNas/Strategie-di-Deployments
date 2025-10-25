# Deployments Overview

Panoramica completa dei diversi tipi di **deployments** in ambito software, cloud e DevOps. Cercherò di essere chiaro e organizzato.

---

## 1. **Deployments tradizionali**

### a. **Manual Deployment**

* Lo sviluppatore o il team rilascia manualmente il software sul server.
* Pro: controllo totale.
* Contro: soggetto a errori, lento, difficile da scalare.

### b. **Automated Deployment**

* Viene usato uno script o un tool per automatizzare il rilascio.
* Pro: riduce errori, più veloce.
* Contro: richiede inizialmente setup e manutenzione.

---

## 2. **Deployment continuo (Continuous Deployment)**

* In un **CI/CD pipeline**, ogni cambiamento che passa i test viene automaticamente deployato in produzione.
* Vantaggi:

  * Aggiornamenti rapidi e frequenti.
  * Feedback immediato dagli utenti.
* Richiesta infrastruttura robusta e test automatici molto solidi.

---

## 3. **Tipi di Deployment basati su strategia**

Questi determinano **come** le nuove versioni del software vengono introdotte agli utenti.

### a. **Blue-Green Deployment**

* Due ambienti identici: **Blue** (attuale) e **Green** (nuovo).
* Il traffico viene spostato dall’ambiente Blue a quello Green.
* Vantaggi: rollback immediato in caso di problemi.

### b. **Canary Deployment**

* La nuova versione viene rilasciata solo a una piccola percentuale di utenti.
* Se funziona, si scala progressivamente al resto.
* Vantaggi: riduce rischi di impatto su tutti gli utenti.

### c. **Rolling Deployment**

* Le nuove versioni vengono distribuite gradualmente sui server.
* Nessun downtime completo.
* Tipico in cluster o servizi cloud.

### d. **Recreate Deployment**

* La versione corrente viene chiusa e poi viene avviata la nuova versione.
* Semplice, ma causa downtime.

### e. **A/B Testing Deployment**

* Rilascia due versioni diverse a due gruppi di utenti per testare nuove funzionalità.
* Aiuta a prendere decisioni basate sui dati reali.

---

## 4. **Deployments in container e microservizi**

* Con Kubernetes o Docker, le strategie si combinano con orchestratori.
* Kubernetes supporta nativamente:

  * **RollingUpdate** (predefinito)
  * **Recreate**
  * **Canary** (via strumenti esterni come Argo Rollouts)
  * **Blue-Green** (via ingress/controller)

---

## 5. **Altri tipi speciali**

* **Shadow Deployment**: il nuovo sistema riceve traffico in parallelo senza influenzare gli utenti reali. Utile per testare performance e logging.
* **Feature Toggles / Feature Flags**: il codice è deployato, ma le funzionalità sono attivate solo per certi utenti o condizioni.

---

### 💡 Sintesi visiva

| Tipo        | Caratteristica principale | Vantaggio                | Svantaggio                   |
| ----------- | ------------------------- | ------------------------ | ---------------------------- |
| Manual      | Deploy manuale            | Controllo totale         | Lento, soggetto a errori     |
| Automated   | Script/CI/CD              | Veloce, ripetibile       | Setup iniziale complesso     |
| Blue-Green  | 2 ambienti identici       | Rollback rapido          | Doppio ambiente              |
| Canary      | Graduale su utenti        | Riduce rischio           | Più complesso                |
| Rolling     | Graduale sui server       | Nessun downtime          | Può richiedere orchestration |
| Recreate    | Stop & start              | Semplice                 | Downtime totale              |
| A/B Testing | Gruppi utenti diversi     | Decisioni basate su dati | Solo per test funzionalità   |

---
