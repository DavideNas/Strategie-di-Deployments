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

## Tabella Riassuntiva

Qua sotto una **tabella completa** con tutte le principali strategie di deployment, caratteristiche, vantaggi, svantaggi e **quando conviene usarle**. Niente grafici, solo spiegazioni chiare.

| Strategia di Deployment             | Come funziona                                                                 | Vantaggi                                          | Svantaggi                                        | Quando usarla                                                  |
| ----------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------ | -------------------------------------------------------------- |
| **Manual Deployment**               | Lo sviluppatore copia/rilascia manualmente il codice sul server               | Controllo totale, semplice da capire              | Lento, soggetto a errori, non scalabile          | Progetti molto piccoli o prototipi                             |
| **Automated Deployment**            | Script o tool automatizzano il rilascio                                       | Riduce errori, più veloce, ripetibile             | Richiede setup iniziale                          | Qualsiasi progetto serio che vuole affidabilità e ripetibilità |
| **Continuous Deployment (CD)**      | Ogni commit che passa i test viene deployato in produzione automaticamente    | Aggiornamenti rapidi, feedback immediato          | Richiede test solidi, infrastruttura robusta     | Sistemi con aggiornamenti frequenti e alta maturità DevOps     |
| **Blue-Green Deployment**           | Due ambienti identici: uno attivo (Blue), uno nuovo (Green)                   | Rollback immediato, zero impatto su utenti        | Doppia infrastruttura, più costoso               | Servizi critici che non possono avere downtime                 |
| **Canary Deployment**               | Nuova versione rilasciata a una piccola percentuale di utenti                 | Riduce rischio di bug su tutti gli utenti         | Complesso da gestire, monitoraggio necessario    | Servizi con grande base utenti, aggiornamenti frequenti        |
| **Rolling Deployment**              | Aggiornamento graduale sui server uno per uno                                 | Nessun downtime totale, aggiornamenti progressivi | Più complesso, richiede orchestrazione           | Sistemi distribuiti e cluster (es. Kubernetes)                 |
| **Recreate Deployment**             | Ferma la versione vecchia e avvia quella nuova                                | Semplice da implementare                          | Downtime totale                                  | Applicazioni non critiche, piccole infrastrutture              |
| **A/B Testing Deployment**          | Due versioni del software rilasciate a gruppi diversi                         | Decisioni basate su dati reali                    | Solo per test funzionalità, complesso da gestire | Nuove feature da validare con utenti reali                     |
| **Shadow Deployment**               | La nuova versione riceve traffico reale in parallelo senza impattare utenti   | Test di performance e logging realistico          | Richiede infrastruttura aggiuntiva               | Test prestazioni e stabilità prima di rilascio pubblico        |
| **Feature Toggles / Feature Flags** | Codice deployato, ma funzionalità attivate solo per certi utenti o condizioni | Deploy sicuro, rollback facile                    | Complesso da gestire se ci sono molte flags      | Introduzione graduale di nuove feature, testing controllato    |

---

### 💡 Consigli pratici per scegliere:

1. **Progetti piccoli o sperimentali** → Manual o Automated.
2. **Aggiornamenti frequenti e DevOps maturi** → Continuous Deployment + Feature Flags.
3. **Servizi critici, alta disponibilità** → Blue-Green o Canary.
4. **Cluster o microservizi** → Rolling Deployment.
5. **Testing di funzionalità o performance** → A/B Testing o Shadow Deployment.

---
