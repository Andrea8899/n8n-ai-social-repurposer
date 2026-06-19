# Multi-Model Social Content Catalyst (n8n + AI OpenSource/No OpenSource)

Ciao! Questo è un progetto pratico che ho sviluppato per risolvere un problema noioso ma costoso: **il tempo perso a convertire lo stesso contenuto per i vari canali social**. 

Questo flusso automatizzato, creato su **n8n**, prende un testo grezzo (un articolo tecnico, il lancio di un prodotto o delle note interne) e lo trasforma all'istante in post pronti per LinkedIn, X (Twitter) e Instagram.

### 🔌 Massima flessibilità (Locale o Cloud)
Il flusso è stato progettato per essere **totalmente agnostico**. Significa che puoi decidere tu quale "cervello" AI collegare:
* **Pronto all'uso in Locale:** Configurato per girare a costo zero e in totale privacy sul tuo computer usando modelli open-source (**Google Gemma, Llama 3 o Mistral via LM Studio/Ollama**).
* **Pronto per il Cloud:** Può essere collegato in 2 minuti alle API commerciali dei grandi provider (**OpenAI ChatGPT, Anthropic Claude, Groq**, ecc.) semplicemente cambiando l'URL dell'endpoint e inserendo la tua chiave API.

---

## 💼 Perché questo progetto serve davvero a un'azienda?

Quando propongo questa soluzione ai clienti, mi concentro su tre vantaggi enormi:

1. **Flessibilità dei costi:** Se configurato con un modello locale, il costo dei token è pari a 0€. Se si sceglie il cloud, si pagano solo i token consumati senza intermediari.
2. **Privacy dei dati flessibile:** Scegliendo la modalità locale, le informazioni sensibili o i dettagli di prodotti non ancora rilasciati non escono mai dai server aziendali (pieno rispetto del GDPR).
3. **Risparmio di tempo reale:** Un lavoro di copywriting e formattazione che di solito richiede un'ora di copia-incolla e adattamento viene ridotto a meno di 15 secondi.

---

## 🛠️ Come è costruita l'infrastruttura

* **Orchestratore:** n8n (installato tramite Docker)
* **Esposizione Webhook:** ngrok (per far comunicare in sicurezza il flusso locale con servizi esterni)
* **Logica personalizzata:** Nodi di codice (JavaScript) per pulire il testo prima di passarlo all'AI.
* **Connessione AI:** Nodo HTTP Request configurato secondo lo standard OpenAI (compatibile con LM Studio, Ollama, OpenAI, Groq, ecc.).

---

## 🚀 Come funziona il flusso (Passo dopo passo)

1. **Ingresso (Webhook):** Il flusso riceve il testo grezzo o l'articolo di partenza.
2. **Pulizia e Formattazione:** Uno script pulisce il testo, analizza la lunghezza e prepara le istruzioni esatte per l'AI.
3. **Elaborazione AI (Il "Cervello"):** I dati vengono inviati all'LLM scelto tramite chiamata API standard. L'AI elabora il testo seguendo delle regole di copywriting precise (il gancio, la divisione in paragrafi, il tono di voce).
4. **Smistamento Output:** Il flusso genera 3 varianti mirate:
   * **LinkedIn:** Professionale, spazioso, con elenchi puntati per massima leggibilità.
   * **X (Twitter):** Tagliato rigidamente in blocchi per creare un thread sotto i 280 caratteri.
   * **Instagram:** Più accattivante, con una selezione di hashtag coerenti.

---

## 📦 Come configurare i modelli (Guida alla scelta)

A seconda di come vuoi far girare l'automazione, configura il nodo **HTTP Request** di n8n in uno di questi modi:

### Opzione A: Modello Locale Open-Source (Gratis & Privato)
Questa è la configurazione nativa con cui viene scaricato il flusso:
* **URL dell'endpoint:** `http://host.docker.internal:1234/v1/chat/completions` (se usi LM Studio) oppure `http://host.docker.internal:11434/v1/chat/completions` (se usi Ollama).
* **Authentication:** Nessuna (`None`).
* **Header:** Non necessario.
* **Modello consigliato:** `gemma`, `llama3` o `mistral`.

### Opzione B: OpenAI (ChatGPT)
Se preferisci la potenza dei modelli cloud di OpenAI:
* **URL dell'endpoint:** `https://api.openai.com/v1/chat/completions`
* **Authentication:** Seleziona `Header Authentication`. 
  * *Name:* `Authorization`
  * *Value:* `Bearer LA_TUA_API_KEY_OPENAI`
* **Nel corpo del JSON:** Cambia `"model": "gemma"` in `"model": "gpt-4o"` (o `gpt-3.5-turbo`).

### Opzione C: Groq (Cloud ultra-veloce ed economico)
Se vuoi usare modelli open-source nel cloud a una velocità pazzesca e costi quasi nulli:
* **URL dell'endpoint:** `https://api.groq.com/openai/v1/chat/completions`
* **Authentication:** Seleziona `Header Authentication`.
  * *Name:* `Authorization`
  * *Value:* `Bearer LA_TUA_API_KEY_GROQ`
* **Nel corpo del JSON:** Cambia `"model": "gemma"` in `"model": "llama3-8b-8192"` o `"model": "mixtral-8x7b-32768"`.

---

### 📝 Come personalizzare l'Input (Usa il tuo testo)

Il flusso contiene attualmente un testo tecnico di esempio (relativo a una libreria Python chiamata "FastQuery") per consentire un test immediato a costo zero. 

Per elaborare i tuoi contenuti, ti basta seguire questi passaggi:
1. Apri il flusso su n8n e fai doppio clic sul primo nodo di input (il nodo **Code JavaScript** o il nodo iniziale in cui viene definito il testo).
2. Sostituisci il valore della variabile del testo (es. `testo_da_elaborare`) con l'articolo, la nota o il comunicato che desideri trasformare.
3. Clicca su **Execute Workflow**. Il sistema pulirà le stringhe, interrogherà il modello locale Gemma e genererà automaticamente il file `.txt` con i tuoi post personalizzati.

---

## 💾 Come provarlo sul tuo computer

1. Clona questa repository:
```bash
   git clone [https://github.com/Andrea8899/n8n-ai-social-repurposer.git](https://github.com/Andrea8899/n8n-ai-social-repurposer.git)
   cd n8n-ai-social-repurposer
