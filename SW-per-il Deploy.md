## Software per il Deployments

Entriamo nel lato **pratico del deployment**, cioè come si porta un software, servizio o applicazione dall’ambiente di sviluppo alla produzione. 
Ecco una panoramica completa, suddivisa per **tipologia di applicazione e strumenti tipici**.

---

## 1. **Deployment di applicazioni tradizionali (monolitiche)**

### a. **Software installabile / on-premise**

* **Cosa si fa**: si crea un pacchetto (installer, zip, rpm/deb) e si copia sul server o sui PC degli utenti.
* **Strumenti comuni**:

  * `rsync`, `scp` per copiare file su server Linux
  * `MSI`, `EXE` per Windows
  * Script Bash o PowerShell per automatizzare installazioni
* **Workflow pratico**:

  1. Compilazione/packaging
  2. Test in ambiente staging
  3. Copia su server di produzione
  4. Avvio/applicazione del servizio

---

### b. **Web application monolitica**

* **Cosa si fa**: il codice viene caricato sul server web (Apache, Nginx, IIS) e configurato.
* **Strumenti comuni**:

  * FTP/SFTP per piccole app
  * CI/CD con Jenkins, GitHub Actions, GitLab CI
  * Docker per creare container portabili
* **Workflow pratico**:

  1. Build del progetto (compilazione, minificazione)
  2. Deploy su server staging
  3. Test QA
  4. Deploy su produzione (manuale o automatico)

---

## 2. **Deployment di microservizi e container**

### a. **Docker**

* **Cosa si fa**: ogni servizio è impacchettato in un container con tutte le dipendenze.
* **Strumenti pratici**:

  * `docker build` → crea l’immagine
  * `docker push` → invia l’immagine a un registry (Docker Hub, GitHub Container Registry)
  * `docker run` / `docker-compose up` → avvia i container
* **Workflow**:

  1. Build immagine Docker
  2. Test locale o in staging
  3. Push su registry
  4. Deploy su server o orchestratore (Kubernetes, Docker Swarm)

### b. **Kubernetes**

* **Cosa si fa**: orchestratore per gestire container su cluster.
* **Strumenti pratici**:

  * `kubectl apply -f deployment.yaml` per aggiornare un Deployment
  * Helm charts per gestione semplificata di app complesse
* **Strategie pratiche**:

  * Rolling Update: aggiorna gradualmente i pod
  * Canary / Blue-Green: configurazione avanzata con ingress controller

---

## 3. **Deployment di serverless / cloud-native**

### a. **Funzioni Serverless (AWS Lambda, Azure Functions, Google Cloud Functions)**

* **Cosa si fa**: il codice è caricato direttamente sul cloud senza preoccuparsi di server.
* **Strumenti pratici**:

  * CLI (`aws lambda deploy`, `gcloud functions deploy`)
  * Framework come Serverless Framework o Terraform per infrastruttura-as-code
* **Workflow pratico**:

  1. Scrittura della funzione
  2. Test locale
  3. Deploy tramite CLI o pipeline CI/CD

### b. **App Web / Servizi Cloud (AWS, Azure, GCP)**

* **Cosa si fa**: deploy diretto su PaaS (Elastic Beanstalk, App Service, Cloud Run)
* **Strumenti pratici**:

  * Interfaccia web / CLI
  * CI/CD per deploy automatico dal repository
* **Vantaggi pratici**:

  * Gestione infrastruttura automatica
  * Scalabilità automatica
  * Integrazione con monitoring e logging

---

## 4. **Strumenti di deployment comuni e pratici**

| Strumento                                           | Tipo                     | Cosa fa                                                 |
| --------------------------------------------------- | ------------------------ | ------------------------------------------------------- |
| **Jenkins / GitHub Actions / GitLab CI**            | CI/CD                    | Automatizza build, test, deploy                         |
| **Docker / Docker Compose**                         | Container                | Impacchetta e avvia applicazioni con dipendenze         |
| **Kubernetes / Helm**                               | Orchestratore            | Gestisce deployment scalabili e strategie avanzate      |
| **Ansible / Chef / Puppet**                         | Configuration Management | Automatizza provisioning e deploy di server             |
| **Terraform / Pulumi**                              | Infrastructure as Code   | Crea e gestisce infrastruttura cloud in modo ripetibile |
| **AWS Elastic Beanstalk / App Service / Cloud Run** | PaaS                     | Deploy e scaling automatico per applicazioni cloud      |

---

### 5. **Esempio pratico di workflow moderno**

1. Scrivo codice → commit su Git
2. CI/CD esegue test automatici
3. Build immagine Docker e push su registry
4. Pipeline applica aggiornamenti su staging (Rolling Update)
5. Test QA
6. Promozione su produzione (Canary o Blue-Green)
7. Monitoraggio e rollback se necessario

---
