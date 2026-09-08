# Volleybal Tracker met Azure synchronisatie

## Architectuur
- Frontend: Azure Static Web Apps
- API: beheerde Azure Functions in map `api`
- Opslag: Azure Table Storage, tabel `VolleybalSync`
- Offline: localStorage plus service worker; openstaande wijzigingen worden na terugkeer van internet verstuurd

## Vereiste Azure instellingen
Maak een Storage Account. Voeg in de Static Web App onder Configuration de applicatie-instellingen toe:
- `VOLLEYBALL_STORAGE_CONNECTION`: connection string van het Storage Account
- `SYNC_HASH_SALT`: een lange willekeurige geheime waarde

## Workflow
Gebruik in het bestaande Azure workflowbestand:
- `app_location: /`
- `api_location: api`
- `output_location: dist`

Behoud de bestaande naam van het Azure deployment-token-secret. De meegeleverde workflow gebruikt een algemene placeholder en moet dus aan jouw bestaande secretnaam worden aangepast, of kopieer alleen `api_location: api` naar jouw bestaande workflow.

## Gebruik
Vul op ieder apparaat dezelfde Team-ID en synchronisatiecode in. Kies `Koppelen / ophalen`. De synchronisatiecode moet minimaal 8 tekens lang zijn en moet als wachtwoord worden behandeld.

## Conflictmodel
Deze versie synchroniseert de volledige actuele dataset per team/code. De laatst opgeslagen versie wint. Gebruik tijdens een live wedstrijd bij voorkeur één apparaat voor invoer; andere apparaten kunnen de gegevens ophalen.
