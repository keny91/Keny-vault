#target-machine


### Requirements 

- ~=4GB ram?


### Deploy from base golden Image

Contains minimal configuration. And the orchestrator (make sure is picked from variable) is registered to be reached via ssh (locally).

### Autobootstrap script

Handshake with the orchestrator (local).
### Modules

sudo apt-get install --reinstall libpam0g libpam-modules libpam-modules-bin

### Docker processes?


- PiHole [Docker]
- WireGuard [Docker] Tener nuestro propio VPN server y sin anuncios
(Requires config for each device)
- Duckdns [Docker] Autorefrescar IP externa (Automatizar generar un dominio?)
- HomeAssistant [Docker]
- Health check script. Signals (external domian, port 10123). A service will register incidences.
### Config 



### Tests before final delivery

Reachable gateways.
Confirmation of configuration.
Active and responsive services and scripts

### After the fact hardening

Once working.