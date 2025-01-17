---
tags:
- Prozess
---
# Prozesse Odoo: App Finanzen
Installation Modul Finanzen `account_accountant`.

## Installation

Auswahl:
* Import CAMT Bank Statement `account_bank_statement_import_camt`
* SEPA Kreditübertragung `account_sepa`
* Auszug aus der Kontorechnung `account_invoice_extract`
* Account Invoice Extract Purchase `account_invoice_extract_purchase`
* Analytische Konten `analytic_enterprise`
* Budgetverwaltung `account_budget`
* Schweizer Buchhaltungsauswertungen `l10n_ch_reports`
	* Accounting Reports `account_reports`
* Lieferanten-Rechnung: Freigegeben zu zahlen `account_3way_match`
*  Management der Zahlungserinnerungen `account_followup`
*  Online Bank Statement Synchronization `account_online_synchronization`

### Optionen aktivieren

Navigation nach *Einstellungen > Finanzen* und Auswahl:
* Print Swiss QR Code #Odoo13 
* QR Codes #Odoo14
* Rechnungsdigitalisierung
* Kostenrechnung
* Kostenstellen-Tags

## Initialisierung

Arbeitsschritte:
*  Unternehmensdaten eintragen
*  Bankkonto erfassen, zum Beispiel
	*  IBAN: `CH3989144871696181962`
	*  Name: `UBS`
*  Buchungsperiode eröffnen
*  Kontenplan übernehmen

## Implementation

Auswahl:
* Journale und Sequenzen festlegen (siehe Odoo Wiki)

#Odoo14  
Die Sequenz in Odoo 14 wird über *Finanzen > Kunden > Rechungen* festgelegt. Dazu erstellen Sie eine erste Proformarechnung und wählen diese links zum Bearbeiten aus. Über das Menü *Aktion > Resequence* kann der nächste Wert `Rechnungsnummer` festgelegt werden. Dasselbe gilt auch für Eingangsrechnungen *Finanzen > Lieferanten > Rechnungen*

### Kontenplan einrichten

Arbeitsschritte:
* Kontennamen übersetzen

| Name                 | Übersetzung              |
| -------------------- | ------------------------ |
| Outstanding Receipts | Ausstehende Einzahlungen |
| Outstanding Payments | Ausstehende Auszahlungen |

### Steuern festlegen

Arbeitsschritte:
* Steuergruppen festlegen *Einstellungen > Finanzen > Steuern > configure your tax accounts*
* Steuern deaktivieren und neue Sätze erfassen *Finanzen > Konfiguration > Steuern*
* Taxgrid deaktiveren

### Eröffnungsbuchungen erstellen

Voraussetzungen:
* Buchhaltung in bisherigen `alten` System ist abgeschlossen
* Kontenplan in Odoo steht zur Verfügung

Arbeitsschritte:
* Festelegen Datum der Übernahme, üblich ist der 31.12. gemäss Statuten der Gesellschaft `Geschäftsjahr`
* Die Bestände der Konten 1000 Kassa, 1020 Bank, 1200 Vorrat Material, 1530 Fahrzeuge etc werden über das Konto 2990 Durchlaufkonto Eröffnungsbilanz erfasst
