# RedHat Cockpit

***

<img src="media/icon_cockpit.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van Redhat Cockpit, een webbased UI voor het beheer van Redhat servers.<br/> 
Indien gedetecteerd, worden plugins voor Podman en KVM virtuele machines automatisch geinstalleerd.<br/>

De UI is na installatie bereikbaar via `https://<servernaam/ip>:9090`<br/>
Website leverancier: `https://project-cockpit.org`<br/>
<br/>


***

# Diensten:

action: **install**<br/>
Installatie van laatste Cockpit versie. Basis configuratie van Cockpit.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **uninstall**<br/>
De-installatie van RedHat Cockpit. Verwijderen configuratie folder.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **configure**<br/>
Her-configuratie van RedHat Cockpit. ROADMAP.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>



Bij installatie worden volgende configuratie instellingen gedaan:<br />
- Tonen banner tekst bij login pagina.<br />
  Tekst in banner_cockpit.txt bestand in ./media folder.<br/>
- Aanpassen custom logo bij login pagina.<br/>
  Logo in media folder, media/logo_cockpit.png bestand.<br/>


***


## Voorbereidingen
(geen).<br/>


## Afhankelijkheden
(geen).<br/>


## Installatie en configuratie
Installatie via action 'install'. (Her-)configuratie via action 'configure'.<br/>
Voorbeeld voor installatie RedHat Cockpit:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: cockpit
      vars:
        action : install

```


## Overige informatie
De UI is bereikbaar via `https://<servernaam/ip>:9090`. Gebruikersnaam voor login dient lid te zijn van lokale administrator groep. 


## Licentie
MIT


## Auteur
Marcel Venema
