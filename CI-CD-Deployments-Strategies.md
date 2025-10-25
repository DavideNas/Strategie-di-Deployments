# CI/CD Deployments

Entriamo nel cuore: **la pipeline CI/CD**. 

Nelle pipeline moderne, le strategie **Canary** e **Blue-Green** sono le più **comuni e strutturate** per la produzione, specialmente con microservizi o applicazioni cloud-native, ma in realtà le pipeline CI/CD possono supportare **molte altre strategie**.  
Vediamo perché e come.

---

## 1. **Che cos’è una pipeline CI/CD**

* **CI (Continuous Integration)**: ogni commit viene integrato nel repository e testato automaticamente.
* **CD (Continuous Delivery/Deployment)**: il codice che passa i test viene automaticamente preparato (delivery) o deployato (deployment) in staging o produzione.
* La pipeline è composta da **stages** tipici:

  1. Build
  2. Test unitari e integrati
  3. Analisi qualità codice (lint, static analysis)
  4. Packaging / creazione artefatti
  5. Deploy su staging
  6. Test end-to-end / QA
  7. Deploy in produzione (qui entrano le strategie di deployment)

---

## 2. **Perché spesso si parla di Canary e Blue-Green**

* Sono le più adatte a **minimizzare rischi** in produzione:

  * **Blue-Green**: rollback istantaneo, zero downtime, semplice da capire.
  * **Canary**: permette di testare nuove versioni con utenti reali, scala gradualmente, ideale per grandi sistemi distribuiti.
* La maggior parte dei tool CI/CD moderni (Jenkins, GitLab CI, ArgoCD, Spinnaker) ha **integrazione nativa o plugin** per queste due strategie.

---

## 3. **Altre strategie utilizzabili nella pipeline CI/CD**

| Strategia             | Come si integra nella pipeline                                                       | Vantaggi                                    | Svantaggi                                            |
| --------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------- | ---------------------------------------------------- |
| **Rolling Update**    | Deploy graduale dei pod/servizi dopo stage di build e test                           | Aggiornamento continuo senza downtime       | Complesso su sistemi distribuiti senza orchestratore |
| **Recreate**          | Stop dell’app precedente e start della nuova                                         | Semplice da configurare nella pipeline      | Downtime totale, rischioso in produzione             |
| **Feature Flags**     | Deploy del codice con feature disattivata, attivabile dinamicamente                  | Permette test controllato e rollback rapido | Gestione complessa delle flags                       |
| **Shadow Deployment** | La pipeline deploya la nuova versione in parallelo a quella live, senza utenti reali | Test di performance e logging realistico    | Richiede infrastruttura aggiuntiva                   |
| **A/B Testing**       | Pipeline rilascia due versioni contemporaneamente a gruppi differenti di utenti      | Decisioni basate su dati reali              | Richiede integrazione analytics e gestione utenti    |

---

## 4. **Come la pipeline gestisce strategia e automazione**

* Dopo i test, la pipeline decide **la modalità di rilascio**:

  * Con Blue-Green: crea un nuovo ambiente e poi switch del traffico.
  * Con Canary: aggiorna solo una parte dei server o degli utenti.
  * Con Rolling: aggiorna i nodi uno alla volta.
* Tutto è **codificato** in pipeline YAML o script CI/CD:

  ```yaml
  deploy_staging:
    stage: deploy
    script:
      - helm upgrade --install myapp ./charts --set image.tag=$CI_COMMIT_SHA
  deploy_production:
    stage: deploy
    script:
      - kubectl apply -f canary-deployment.yaml
  ```
* L’idea chiave è che **la pipeline automatizza tutto**: build, test, packaging e deploy con strategia scelta.

---

💡 **In sintesi**:
Non ho citato altre strategie prima perché Canary e Blue-Green sono quelle **più sicure e strutturate** per ambienti produttivi con pipeline CI/CD, mentre le altre sono o più semplici (Recreate) o più particolari (Shadow, Feature Flags, A/B). Ma una pipeline ben costruita può supportarle tutte: la scelta dipende **dal rischio accettabile, dalla complessità dell’infrastruttura e dal tipo di applicazione**.

---
