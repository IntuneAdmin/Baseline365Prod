# Baseline365 — Static GitHub Pages edition

Een volledig statische baselinebibliotheek. Geen login, backend, database, OAuth, Cloudflare Worker of GitHub-token in de website.

## Structuur

```text
.
├── .github/workflows/deploy-pages.yml
└── site/
    ├── index.html
    └── baselines/
        ├── index.json
        ├── windows-11-core.json
        └── edge-standard.json
```

## Publiceren naar GitHub Pages

1. Push de inhoud van deze map naar de root van `IntuneAdmin/Baseline365Prod` op branch `main`.
2. Ga in GitHub naar **Settings → Pages**.
3. Kies **GitHub Actions** als Build and deployment source.
4. De workflow deployt de map `site/` automatisch bij wijzigingen.
5. De website is beschikbaar via de GitHub Pages URL van de repository.

## Een nieuwe baseline toevoegen

1. Maak een nieuw JSON-bestand in `site/baselines/`, bijvoorbeeld `windows-11-advanced.json`.
2. Gebruik de JSON-structuur van een bestaande baseline als uitgangspunt.
3. Voeg de bestandsnaam toe aan `site/baselines/index.json` onder `baselines`.
4. Commit beide bestanden naar `main`.
5. GitHub Actions bouwt en publiceert de website automatisch.

Iedere baseline is een zelfstandig JSON-bestand. `index.json` is alleen de catalogus die vertelt welke bestanden de website moet laden.

## JSON-formaat

Een baseline bevat:

- `id`: unieke, stabiele identifier
- `name`: zichtbare naam
- `category`: bijvoorbeeld Windows 11 of Microsoft Edge
- `tier`: Core, Standard of Advanced
- `version`: semantisch versienummer
- `status`: bijvoorbeeld Draft of Published (alleen gepubliceerde items opnemen in de catalogus)
- `description`: omschrijving
- `updated`: datum in YYYY-MM-DD
- `settings`: lijst met instellingen
- `changelog`: releasehistorie

Iedere setting ondersteunt:

- `id`, `name`, `value`, `category`, `description`, `rationale`, `implementation`, `mappings`

`value` mag een string, boolean, getal, array of object zijn. `mappings` kan strings of objecten met `framework` en `control` bevatten.

## Beheer en beveiliging

Deze website is volledig publiek en statisch. Er is bewust geen adminpagina of authenticatie. Beheer gebeurt rechtstreeks via GitHub (webinterface, Git of pull requests). Gebruik branch protection en pull requests als je wijzigingen eerst wilt reviewen. Iedereen kan de publieke baselinebestanden lezen en downloaden.

## Opmerking over de voorbeeldbaselines

De meegeleverde Windows 11- en Edge-baselines zijn voorbeelden van het gegevensformaat en de weergave. Ze zijn geen gevalideerde security-aanbevelingen en moeten inhoudelijk worden gecontroleerd voordat ze als productie-baselines worden gepubliceerd.
