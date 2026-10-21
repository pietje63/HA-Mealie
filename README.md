# Mealie + MealieShopper voor Home Assistant OS

Dit pakket is een startpunt om MealieShopper als Home Assistant-app te installeren op Home Assistant OS (bijvoorbeeld Home Assistant Green).

## Mealie: gebruik de bestaande community-app

Mealie heeft al een onderhouden Home Assistant-app in de communityrepository. Gebruik die liever dan een tweede, eigen Mealie-verpakking te onderhouden:

1. Ga in Home Assistant naar **Instellingen → Apps** (op oudere versies: **Instellingen → Add-ons**).
2. Open de App Store en kies het menu rechtsboven → **Repositories**.
3. Voeg deze repository toe:
   `https://github.com/hassio-addons/repository`
4. Zoek **Mealie** en installeer die app.
5. Start Mealie en maak in Mealie een API-token aan voor de Home Assistant-integratie.
6. Voeg daarna via **Instellingen → Apparaten & diensten → Integratie toevoegen** de officiële **Mealie**-integratie toe.

De officiële Mealie-integratie ondersteunt Mealie 3.2.0 en hoger.

## MealieShopper

De map `mealieshopper/` bevat de Home Assistant-app-configuratie voor de bestaande upstream Docker-image. Er wordt geen eigen Docker-image gebouwd.

### Wat deze configuratie doet

- Gebruikt `ghcr.io/helmerznl/mealieshopper:1.5.3`.
- Ondersteunt `aarch64` (Home Assistant Green) en `amd64`.
- Bewaart de applicatiegegevens in de persistente app-map `/data`.
- Publiceert de interne poort `8000` op hostpoort `5959`.
- Laat de eerste-start-wizard van MealieShopper de beveiliging en de koppelingen instellen.

### Installeren als lokale app

Deze map is bedoeld voor Home Assistant OS met Supervisor:

1. Maak een back-up van Home Assistant.
2. Kopieer de map `mealieshopper` naar de lokale apps/add-ons-map van Home Assistant OS, zodat `config.yaml` direct in die map staat.
3. Open de App Store en herlaad/ververs lokale apps als dat nodig is.
4. Installeer **MealieShopper** en start de app.
5. Open `http://<IP-adres-van-Home-Assistant>:5959`.

Als je geen lokale apps kunt beheren in jouw installatie, plaats deze map dan in een eigen GitHub-repository en voeg die repository-URL toe via de App Store → Repositories. Neem in die repository de map `mealieshopper/` en `repository.yaml` op.

### Eerste configuratie

Volg de installatiehulp van MealieShopper. Gebruik het adres waarop MealieShopper Mealie kan bereiken en maak in Mealie een API-token aan. Als Mealie als Home Assistant-app draait, is de interne app-hostnaam vaak geschikt voor container-naar-containerverkeer; controleer de URL die bij jouw Mealie-app hoort.

MealieShopper is bereikbaar via poort 5959 op het Home Assistant-hostadres. HTTPS/passkeys vereisen een correct ingestelde domeinnaam en HTTPS-proxy; begin desgewenst met gebruikersnaam en wachtwoord op je vertrouwde thuisnetwerk.

## Belangrijke beperkingen van deze eerste versie

- Dit is een **starterconfiguratie**, geen installatie die al op jouw Home Assistant Green is uitgevoerd of daar getest.
- De configuratie gebruikt de versie-tag `1.5.3` van de upstream-image. Als de registry die tag niet aanbiedt voor jouw architectuur, moet de image-tag of de build-aanpak worden aangepast.
- De app-configuratie gebruikt de upstream-image rechtstreeks; omgevingsvariabelen zijn niet als Home Assistant-opties aangeboden. De standaardinstallatiewizard is bedoeld om de eerste koppelingen in de webinterface te regelen.
- De app gebruikt geen Ingress in deze eerste versie. Dat voorkomt dat we zonder testen aannemen dat login, cookies, passkeys en URL-detectie achter de Home Assistant-proxy goed werken.
- Home Assistant OS/Supervisor is vereist voor het installeren van apps/add-ons. Dit werkt niet op een gewone Home Assistant Container-installatie.

## Bestanden

```text
repository.yaml
mealieshopper/
  config.yaml
```
