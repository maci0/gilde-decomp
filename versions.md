# 📦 Europa 1400: The Guild – Version Identification & Preservation Schema

## 🧱 Naming Format

```
<series>-<edition>-<patch>-<lang>-<region>-<dist>-<media>
```

## 📚 Components Explained

| Component | Example                        | Description                                                                 |
|-----------|--------------------------------|-----------------------------------------------------------------------------|
| series    | `gilde`                        | Always `gilde` for this project (short, consistent tag)                    |
| edition   | `base`, `gold`, `exp`, `demo`  | Game edition: base game, gold (exp+base), expansion standalone, demo       |
| patch     | `v1.03`, `v2.06`, `v1.05b3`     | Precise patch version (can include `b` for beta if applicable)             |
| lang      | `de`, `en`, `fr`, `ru`         | Primary language of the build                                               |
| region    | `de`, `us`, `uk`, `eu`, `ru`, `int` | Region or market for release (or `int` if international/unknown)    |
| dist      | `retail`, `steam`, `gog`, `coverdisk`, `beta`, `iso`, `redump` | Distribution method |
| media     | `cd`, `dvd`, `digital`, `bin`, `exe` | Format or physical medium                                            |


| Game Version                                | Binaries                                       | Notes                                                                        | Release Date   | Media   | Identifier                            |
|:--------------------------------------------|:-----------------------------------------------|:-----------------------------------------------------------------------------|:---------------|:--------|:--------------------------------------|
| BASE Edition V1.0 (DE/DE, Retail, CD)       |            | Original retail DE release; no TL.exe or Server.dll observed in early builds | 2002-11-14     | cd      | gilde-base-v1.0-de-de-retail-cd       |
| BASE Edition V1.0 (EN/UK, Retail, CD)       | | Early JoWooD UK release; renamed main EXE; no TL or server files present     | 2002-11-29     | cd      | gilde-base-v1.0-en-uk-retail-cd       |
| BASE Edition V1.01 (DE/DE, Retail, CD)      |           | Minor updates; not widespread, usually overwritten by later patches          | 2002-12-10     | cd      | gilde-base-v1.01-de-de-retail-cd      |
| BASE Edition V1.03 (EN/US, Retail, CD)      |           | Shipped in UK/US boxed editions; server.dll present for LAN play             | 2003-01-15     | cd      | gilde-base-v1.03-en-us-retail-cd      |
| BASE Edition V1.03C (RU/RU, Retail, CD)     |          | Custom Russian translation & localized build from Russobit-M                 | 2003-01-25     | cd      | gilde-base-v1.03c-ru-ru-retail-cd     |
| BASE Edition V1.04A (DE/DE, Retail, CD)     |          | Released shortly before add-on launch; improved voice files                  | 2003-02-15     | cd      | gilde-base-v1.04a-de-de-retail-cd     |
| BASE Edition V1.05B3 (EN/US, Retail, CD)    |         | Final patch for base game (Beta); widely used in GOG/Steam classic releases  | 2003-03-01     | cd      | gilde-base-v1.05b3-en-us-retail-cd    |
| BASE Edition V1.05B3 (FR/FR, Beta, DIGITAL) |         | Rare French-language Beta patch, available via forums (JoWooD France)        | 2003-03-01     | digital | gilde-base-v1.05b3-fr-fr-beta-digital |
| GOLD Edition V2.0 (DE/DE, Retail, DVD)      |              | Base expansion release; no TL.exe observed yet                               | 2003-03-20     | dvd     | gilde-gold-v2.0-de-de-retail-dvd      |
| GOLD Edition V2.0 (EN/UK, Retail, DVD)      |             | Some international discs labeled “Gold”; includes merged content             | 2003-04-01     | dvd     | gilde-gold-v2.0-en-uk-retail-dvd      |
| GOLD Edition V2.05 (DE/DE, Retail, DVD)     |            | Some DE versions shipped with TL.exe optimized for hardware T&L              | 2003-04-15     | dvd     | gilde-gold-v2.05-de-de-retail-dvd     |
| GOLD Edition V2.05 (EN/UK, Retail, DVD)     |             | Some EN builds included TL.exe, others did not (regional variance)           | 2003-04-20     | dvd     | gilde-gold-v2.05-en-uk-retail-dvd     |
| GOLD Edition V2.06 (DE/DE, Retail, DVD)     |            | Final and most stable version; used by Steam, GOG, etc.                      | 2003-05-05     | dvd     | gilde-gold-v2.06-de-de-retail-dvd     |
| GOLD Edition V2.06 (EN/US, Retail, DVD)     |             |                                                                              | nan            | dvd     | gilde-gold-v2.06-en-us-retail-dvd     |
| GOLD Edition V2.06 (EN/INT, Steam, DIGITAL) |             | English final version found in official digital distribution                 | 2009-10-15     | digital | gilde-gold-v2.06-en-int-steam-digital |
| GOLD Edition V2.06 (EN/INT, GoG, DIGITAL)   | ```7d1f178f6463ab41f90987451187a93056814293832a5d2c76444dbd087e3ae8  Europa1400Gold.exe``` <br> ```6fe7a24c93192f6511bc8595eb82fd166db44f6cbeaf7c2f036838f3b6b4af45  Europa1400Gold_TL.exe``` <br> ```3cc2ce9049e41ab6d0eea042df4966fbf57e5e27c67fb923e81709d2683609d1  Server/server.dll``` <br> ```33399b878747d9a985f0f928ba3369e58aa5b2c346d845e8d29ed91a7921f194  d3_resource.dll``` <br> ```50e335fc9994d22d661591a44017c46bf7ff5bc31c6008558a897b4fcff8f0d4  d8_resource.dll``` | English final version found in official digital distribution on GoG              | 2012-01-26     | digital | gilde-gold-v2.06-en-int-gog-digital   |
| GOLD Edition V2.06 (FR/FR, Retail, DVD)     |             | French Gold rarely seen physically, likely derived from EN binaries          | 2003-06-01     | dvd     | gilde-gold-v2.06-fr-fr-retail-dvd     |
| GOLD Edition V2.06 (RU/RU, Retail, DVD)     |             | Some GOG builds include Russian Gold; presence of TL.exe unverified          | 2004-01-10     | dvd     | gilde-gold-v2.06-ru-ru-retail-dvd     |
| EXP Edition V2.0 (DE/DE, Retail, ISO)       |              |                                                                              | nan            | iso     | gilde-exp-v2.0-de-de-retail-iso       |
| DEMO Edition V0.99 (EN/INT, Beta, DIGITAL)  |             |                                                                              | nan            | digital | gilde-demo-v0.99-en-int-beta-digital  |
| BASE Edition V1.01 (DE/DE, Redump, CD)      |          |                                                                              | nan            | cd      | gilde-base-v1.01-de-de-redump-cd      |
