# Mobile Deploymnets (Play Store)

Se parliamo di **app mobile** su store come **Google Play**, il contesto è diverso rispetto al deployment server o container, perché non puoi “switchare” versioni in tempo reale sui dispositivi degli utenti come in un servizio web. Qui le strategie di deployment sono vincolate dalle policy dello store, ma ci sono comunque diverse possibilità.

---

## 1. **Tipi di deploy su Google Play**

| Tipo di Deploy                       | Come funziona                                                                                 | Vantaggi                                                                          | Svantaggi                                               | Quando usarlo                                          |
| ------------------------------------ | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------ |
| **Internal Testing**                 | La nuova versione è disponibile solo a un gruppo interno di tester (fino a 100 tester)        | Feedback rapido, test bug interni                                                 | Solo pochi utenti                                       | Testing iniziale rapido prima di beta                  |
| **Closed Testing / Beta**            | La versione è disponibile a un gruppo selezionato di utenti tramite link o lista              | Test su un pubblico più ampio, raccolta feedback                                  | Utenti limitati, visibilità ridotta                     | Beta test con utenti reali prima del rilascio pubblico |
| **Open Beta**                        | Tutti gli utenti possono iscriversi per testare la nuova versione prima del rilascio pubblico | Feedback da un pubblico ampio                                                     | Possibili bug visibili a molti                          | Beta pubblica, test compatibilità su più device        |
| **Production Release**               | La versione è disponibile a tutti gli utenti                                                  | Distribuzione ufficiale                                                           | Aggiornamenti immediati a tutti gli utenti, rischio bug | Rilascio stabile dopo test                             |
| **Staged Rollout (Gradual Release)** | Il rilascio viene fatto solo a una percentuale degli utenti (es. 5%, 10%)                     | Limita il rischio di bug su tutti gli utenti, puoi monitorare crash e performance | La versione non raggiunge subito tutti                  | Aggiornamenti critici o nuove feature importanti       |
| **Internal App Sharing**             | Caricamento rapido dell’APK/AAB per tester interni senza passare per approvazione             | Test rapidissimo, comodo per debug                                                | Solo tester con link diretto                            | Debug veloce e test interni                            |

---

## 2. **Strategie pratiche in contesto mobile**

1. **Internal / Closed Testing** → equivalente a **Canary / Shadow deployment**: solo alcuni utenti ricevono la nuova versione.
2. **Open Beta** → test su scala più ampia, simile a **Canary a percentuale maggiore**.
3. **Staged Rollout** → la strategia più vicina a un **Canary deployment** web: si rilascia gradualmente, monitorando crash, ANR, feedback.
4. **Production Release** → equivalente al deployment **Blue-Green / Rolling completo**: tutti ricevono l’update, rischi maggiori se non testato bene.

---

## 3. **Strumenti di supporto**

* **Google Play Console**: gestione di testing, staged rollout, monitoraggio crash (Crashlytics)
* **Firebase App Distribution**: distribuzione rapida a tester senza passare per Play Store
* **CI/CD per mobile**:

  * **Fastlane**: automatizza build, test e deploy verso Play Store
  * **Bitrise / Codemagic**: pipeline mobile complete per iOS/Android
* **Monitoring**:

  * Firebase Crashlytics, Google Play Console pre-launch reports, Analytics

---

💡 **Nota pratica**:
Su mobile, a differenza del web, **non puoi switchare istantaneamente versioni sugli utenti**. Per ridurre i rischi si usano **staged rollout, beta testing e feature flags lato client**.
Molte app moderne combinano **staged rollout + feature flags** per introdurre nuove funzionalità senza dover aspettare che tutti aggiornino.

---
