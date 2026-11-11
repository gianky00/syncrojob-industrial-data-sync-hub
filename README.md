# SyncroJob — Piattaforma Integrata per la Gestione Dati di Cantiere & RPA

![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=flat-square&logo=python&logoColor=white)
![GUI](https://img.shields.io/badge/GUI-PySide6%20(Qt6)-41CD52?style=flat-square&logo=qt&logoColor=white)
![Database](https://img.shields.io/badge/Database-SQLite3-003B57?style=flat-square&logo=sqlite&logoColor=white)
![RPA](https://img.shields.io/badge/Automation-Selenium%20%2F%20Playwright-43B02A?style=flat-square)
![Code Quality](https://img.shields.io/badge/Quality-Ruff%20%7C%20MyPy%20Strict-0F172A?style=flat-square)

**SyncroJob** è un'applicazione desktop modulare progettata per centralizzare, automatizzare e validare i flussi informativi tecnici e contabili di cantiere (contabilità strumentale, ordini d'acquisto, timesheet, permessi di lavoro, presenze e parco strumenti campione).

---

## Architettura & Funzionalità Principali

### 1. Automazione RPA & Sincronizzazione Differenziale
- **Portali Operativi & Fornitori:** Estrazione e caricamento automatizzato di timesheet, stato avanzamento Ordini d'Acquisto (OdA) e timbrature giornaliere.
- **Gestione Permessi di Lavoro (PdL):** Ricerca, download e allineamento automatico dello stato di programmazione dei PdL.
- **Motore di Sincronizzazione Differenziale (`SQL EXCEPT`):** Allineamento transazionale su tabelle temporanee SQLite per calcolare con esattezza le sole righe nuove o modificate rispetto ai fogli di calcolo e ai database locali.

### 2. Moduli Operativi Integrati

| Modulo | Funzione Tecnica |
| :--- | :--- |
| **Contabilità Strumentale** | Gestione consuntivazione tecnica, associazione voci di listino/prezziario e controllo avanzamento. |
| **Certificati Campione** | Registro digitale, tracciabilità metrologica e monitoraggio scadenze degli strumenti di riferimento. |
| **Storico & Dettagli OdA** | Interrogazione rapida e sincronizzazione degli Ordini d'Acquisto di commessa. |
| **Scarico & Carico Timesheet** | Acquisizione massiva e validazione dei consuntivi orari in formato PDF ed Excel. |
| **Anagrafica & Timbrature** | Verifica presenze giornaliere, quadratura ore lavorate e allineamento squadre operative. |
| **Autopilot Scheduler** | Pianificatore integrato per l'esecuzione non presidiata dei task di sincronizzazione periodica. |

### 3. Affidabilità, Tracciabilità & UI
- **Audit Trail Immutabile:** Tracciamento crittografico (`SHA-256 hash chaining`) delle operazioni di sincronizzazione e modifica dati.
- **Diagnostica & Resilienza:** Gestione strutturata dei log con `Loguru` e `faulthandler` per il salvataggio immediato dello stacktrace in caso di anomalie.
- **Interfaccia Utente Moderna:** Costruita in **PySide6 (Qt6)** con componenti custom, dialoghi standardizzati, tema dinamico e notifiche contestuali.

---

## Stack Tecnologico

| Livello | Tecnologie Utilizzate |
| :--- | :--- |
| **Core & Tipizzazione** | Python 3.12+, Pydantic v2 (JSON Schema Validation), AST Context Generation |
| **Interfaccia Grafica** | PySide6 (Qt6), Custom Modern Widgets |
| **Persistenza Dati** | SQLite3 (Database relazionali multi-dominio con query differenziali) |
| **Browser RPA & Office** | Selenium WebDriver, OpenPyXL, Pandas, Win32COM (Excel/VBA Automation) |
| **Quality Gate & Test** | Ruff, MyPy (`--strict`), Refurb, Pre-commit, Pytest |

---

## Setup & Sviluppo

### Requisiti
- **Sistema Operativo:** Windows 10 / 11 (64-bit)
- **Runtime:** Python 3.12+ e gestore pacchetti `uv`
- **Browser:** Google Chrome (per i worker RPA)

### Installazione Ambiente

```powershell
git clone https://github.com/gianky00/syncrojob-industrial-data-sync-hub.git
cd syncrojob-industrial-data-sync-hub

# Creazione ambiente virtuale e installazione dipendenze
uv venv
uv sync
```

### Comandi Principali

```powershell
# Avvio dell'applicazione desktop
uv run syncrojob

# Esecuzione della suite di test
python -m tests.run_robust_test

# Controllo qualità codice (Linter + Type Checking Strict)
uv run ruff check src/
uv run mypy --strict src/
```

---

## Autore
Progettato e sviluppato da **Giancarlo Allegretti** — *Industrial Automation, Instrumentation & AI Software Engineering*.
