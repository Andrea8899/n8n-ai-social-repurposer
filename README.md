\# Local AI Social Content Catalyst (n8n + Gemma)



Ciao! Questo è un progetto pratico che ho sviluppato per risolvere un problema noioso ma costoso: \*\*il tempo perso a convertire lo stesso contenuto per i vari canali social\*\*. 



Questo flusso automatizzato, creato su \*\*n8n\*\*, prende un testo grezzo (un articolo tecnico, il lancio di un prodotto o delle note interne) e usa un modello di Intelligenza Artificiale locale (\*\*Google Gemma tramite LM Studio\*\*) per trasformarlo all'istante in post pronti per LinkedIn, X (Twitter) e Instagram.



\---



\## 💼 Perché questo progetto serve davvero a un'azienda?



Quando propongo questa soluzione ai clienti, mi concentro su tre vantaggi enormi:



1\. \*\*Costo dei Token = 0€:\*\* Girando interamente su modelli open-source locali, l'azienda non deve pagare abbonamenti o API a consumo (come OpenAI o Anthropic). L'automazione è gratis per sempre.

2\. \*\*Privacy dei dati al 100%:\*\* Molte aziende hanno paura di dare in pasto all'AI i propri dati sensibili o i dettagli di prodotti non ancora usciti. Qui i dati non escono mai dal computer o dal server aziendale (pieno rispetto del GDPR).

3\. \*\*Risparmio di tempo reale:\*\* Un lavoro di copywriting e formattazione che di solito richiede un'ora di copia-incolla e adattamento viene ridotto a meno di 15 secondi.



\---



\## 🛠️ Come è costruita l'infrastruttura



Per non dipendere da servizi cloud costosi, ho strutturato il flusso così:

\* \*\*Orchestratore:\*\* n8n (installato in locale tramite Docker)

\* \*\*Motore AI:\*\* Google Gemma (eseguito in locale su LM Studio)

\* \*\*Esposizione Webhook:\*\* ngrok (per far comunicare in sicurezza il flusso locale con l'esterno)

\* \*\*Logica personalizzata:\*\* Nodi di codice (JavaScript/Python) per pulire il testo prima di passarlo all'AI.



\---



\## 🚀 Come funziona il flusso (Passo dopo passo)



1\. \*\*Ingresso (Webhook):\*\* Il flusso riceve il testo grezzo o l'articolo di partenza.

2\. \*\*Pulizia e Formattazione:\*\* Uno script pulisce il testo, analizza la lunghezza e prepara le istruzioni esatte per l'AI.

3\. \*\*Elaborazione Locale (LM Studio):\*\* I dati vengono inviati all'endpoint locale (`http://localhost:1234/v1`). Gemma elabora il testo seguendo delle regole di copywriting precise (il "gancio", la divisione in paragrafi, il tono di voce).

4\. \*\*Smistamento Output:\*\* Il flusso genera 3 varianti mirate:

&#x20;  \* \*\*LinkedIn:\*\* Professionale, spazioso, con elenchi puntati per massima leggibilità.

&#x20;  \* \*\*X (Twitter):\*\* Tagliato rigidamente in blocchi per creare un thread sotto i 280 caratteri.

&#x20;  \* \*\*Instagram:\*\* Più accattivante, con una selezione di hashtag coerenti.



\---



\## 📦 Come provarlo sul tuo computer



\### Prerequisiti

\* Docker installato e attivo.

\* LM Studio con il modello \*\*Gemma\*\* caricato e il Local Server avviato sulla porta `1234`.

\* ngrok per esporre il webhook se vuoi testarlo con servizi esterni.



\### Configurazione Rapida

1\. Clona questa repository:

```bash

&#x20;  git clone \[https://github.com/IL\_TUO\_USERNAME/local-ai-social-content-catalyst.git](https://github.com/IL\_TUO\_USERNAME/local-ai-social-content-catalyst.git)

&#x20;  cd local-ai-social-content-catalyst

