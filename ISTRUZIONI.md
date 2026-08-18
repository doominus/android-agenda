# Agenda Prenotazioni per Android — istruzioni

Questa cartella contiene tutto il necessario per trasformare la tua Agenda
Prenotazioni in una vera app installabile sul tablet Android, senza passare
dal Play Store. È la stessa identica app che usi da browser: stesso file,
stesso database Supabase, stessi dati. Cambia solo il modo in cui viene
avviata (un'icona sulla home invece del browser), e in più guadagna la
possibilità di essere installata "offline" sul dispositivo.

Non serve nessun account sviluppatore Google e non c'è nessun costo.

## Come funziona

Io non ho un computer con Android Studio in questo ambiente, quindi l'APK
(il file da installare sul tablet) viene compilato automaticamente da
GitHub, gratuitamente, ogni volta che carichi questi file su un repository
GitHub. È un sistema robusto e comune: tu carichi i file una volta, GitHub
li compila per te e ti restituisce l'app pronta da scaricare.

## Passo 1 — Crea un repository GitHub

Se non ne hai già uno dedicato a questo (quello che usi per il sito
`agenda.anticamaddalena.it` va bene comunque separato, per chiarezza):

1. Vai su github.com ed effettua l'accesso con il tuo account.
2. Clicca "New repository".
3. Dagli un nome, ad esempio `agenda-android`.
4. Puoi lasciarlo "Private" (privato) se preferisci: funziona lo stesso.
5. Crea il repository (non serve aggiungere nulla in automatico).

## Passo 2 — Carica questi file

Nella pagina del repository appena creato, usa "Add file" → "Upload files"
e trascina dentro **tutto il contenuto** di questa cartella, mantenendo la
struttura (compresa la sottocartella `.github/workflows/` con il file
`build-android.yml`, e la sottocartella `www/` con `index.html` dentro).

Se GitHub ti fa fatica a caricare cartelle da browser, in alternativa puoi
usare Git da riga di comando:

```
cd agenda-android
git init
git add .
git commit -m "Prima versione app Android"
git branch -M main
git remote add origin <URL del tuo repository>
git push -u origin main
```

## Passo 3 — Fai partire la compilazione

Il caricamento dei file avvia già automaticamente la compilazione. Per
controllare (o per farla ripartire in un altro momento):

1. Vai sulla scheda **Actions** in alto nel repository.
2. Vedrai un'esecuzione chiamata "Build Android APK" — clicca sopra.
3. Aspetta che finisca (di solito 3-6 minuti). Un pallino verde con la
   spunta significa che è andata a buon fine.

Se in futuro vuoi ricompilare senza aver cambiato nulla, apri la scheda
Actions, seleziona "Build Android APK" nel menu a sinistra e clicca
"Run workflow".

## Passo 4 — Scarica l'app

Quando l'esecuzione è completata (spunta verde), scorri in fondo alla
pagina di quell'esecuzione: troverai una sezione "Artifacts" con un file
chiamato `agenda-prenotazioni-android`. Cliccalo per scaricare uno zip che
contiene il file `app-debug.apk`.

## Passo 5 — Installa l'app sul tablet

1. Trasferisci il file `app-debug.apk` sul tablet Android (via email a te
   stesso, Google Drive, cavo USB, o scaricandolo direttamente dal tablet
   se apri GitHub dal tablet stesso).
2. Apri il file `.apk` sul tablet. Se è la prima volta, Android chiederà il
   permesso di installare app da fonti diverse dal Play Store: si chiama
   "Installa app sconosciute" — concedilo solo per l'app che stai usando
   per aprire il file (es. "File" o "Drive"). È normale e sicuro: succede
   con qualunque app installata fuori dal Play Store, e questa parla solo
   con il tuo database, non con nient'altro.
3. Conferma l'installazione. Comparirà l'icona "Agenda Prenotazioni" sulla
   home del tablet, pronta all'uso.

Da qui in poi la userai come qualsiasi altra app: login una volta, e resta
collegata. Funziona con lo stesso identico motore anti-perdita-dati offline
che ho appena aggiunto alla versione web.

## Aggiornare l'app in futuro

Quando in futuro aggiornerò l'app (nuove funzioni, correzioni), ti darò il
nuovo file `index.html`: basterà sostituire quello dentro `www/` nel tuo
repository GitHub (con "Add file" → "Upload files", sovrascrivendolo), e la
compilazione ripartirà da sola producendo un nuovo APK da scaricare e
installare di nuovo sul tablet (l'installazione aggiorna l'app esistente,
non serve disinstallarla prima).

## Cose da sapere

- Questo è un APK "debug": è il modo normale e più semplice per installare
  un'app fatta su misura per un solo uso interno come questo. Non ha nessuna
  limitazione pratica per il tuo caso — funziona esattamente come una app
  definitiva. L'unica differenza è che non può essere pubblicata sul Play
  Store così com'è, cosa che comunque non ti serve.
- La versione da browser (quella su `agenda.anticamaddalena.it`) continua a
  funzionare esattamente come prima, in parallelo. Puoi usare entrambe
  contemporaneamente su dispositivi diversi: sono sempre sincronizzate
  perché parlano allo stesso database.
- Se la compilazione su GitHub Actions dovesse fallire (pallino rosso invece
  che verde), apri quell'esecuzione, clicca sul passaggio che è andato in
  errore per vedere il messaggio, e mandamelo: lo correggo e ti preparo il
  file aggiornato.
