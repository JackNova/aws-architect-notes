# Sicurezza - AWS Framework di Architettura cloud



### 7 Principi di design

https://wa.aws.amazon.com/wat.pillar.security.it.html

**1. Implement a strong identity foundation**

La gestione dell'identità dovrebbe essere centralizzata. Bisogna evitare l'utilizzo di credenziali statiche utilizzate indefinitamente nel tempo o per grandi periodi. Ricorda sempre il 'principle of least privilege' nella separazione delle responsabilità.



**2. Enable traceability**

Bisogna reagire in tempo reale ed automaticamente. I sistemi di logging e monitoraggio delle risorse vanno integrati con sistemi che permettono di investigare e reagire automaticamente. 



**3. Apply security at all layers**

Sposa l'approccio 'defense in depth' attuando molteplici controlli ad ogni livello, es. edge network, VPC, load balancing, istanze e servizi di elaborazione, sistemi operativi, applicazioni,  e codice sorgente.



**4. Automate security best practices**

Adotta IaaC anche per i meccanismi di sicurezza. I controlli devono essere implementati come template rappresentati da codice sorgente sotto versionamento.



**5. Protect data in transit and at rest**

I dati vanno classificati a seconda di quanto sono 'sensibili' e dove appropriato bisogna utilizzare meccanismi di crittografia, tokenization (pseudonimizzazione) e controllo degli accessi.



**6. Prepare for security events**

Utilizza strumenti e meccanismi automatici per la gestione dei dati sensibili in modo da evitare l'errore umano.



**7. Prepare for security events**

Definisci dei protocolli di indagine e gestione degli incidenti e dei processi che siano allineati alle necessità business. Effettua delle simulazioni per verificare la risposta agli incidenti ed automatizza le fasi di rilevamento, investigazione e recupero.