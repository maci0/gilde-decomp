🧱 Naming Format:
```php
<series>-<edition>-<patch>-<lang>-<region>-<dist>-<media>
```

📚 Components Explained:
Component	Example	Description
series	gilde	Always gilde for this project (short, consistent tag)
edition	base, gold, exp, demo	Game edition: base game, gold (exp+base), expansion standalone, demo
patch	v1.03, v2.06, v1.05b3	Precise patch version (can include b for beta if applicable)
lang	de, en, fr, ru	Primary language of the build
region	de, us, uk, eu, ru, int	Region or market for release (or int if international/unknown)
dist	retail, steam, gog, coverdisk, beta, iso, redump	Distribution method
media	cd, dvd, digital, bin, exe	Format or physical medium



| Game Version | Patch Version    | Language       | Main EXE                        | Notes                                                                                       | Media   | Identifier                        |
|--------------|------------------|----------------|----------------------------------|---------------------------------------------------------------------------------------------|---------|-----------------------------------|
| 1.0          | Base / Unpatched | German (DE)    | Guild.exe                        | Original retail DE release; no TL.exe or Server.dll observed in early builds               | retail  | guild-base-1.0-de                 |
| 1.0          | Base / Unpatched | English (UK)   | Europa1400.exe                   | Early JoWooD UK release; renamed main EXE; no TL or server files present                   | retail  | guild-base-1.0-en-uk              |
| 1.01         | Patch 1.01       | German (DE)    | Guild.exe                        | Minor updates; not widespread, usually overwritten by later patches                        | patch   | guild-base-1.01-de                |
| 1.03         | Patch 1.03       | English (EU/US)| Guild.exe                        | Shipped in UK/US boxed editions; server.dll present for LAN play                           | retail  | guild-base-1.03-en-int            |
| 1.03c        | Patch 1.03c      | Russian (RU)   | Guild.exe (localized strings)    | Custom Russian translation & localized build from Russobit-M                               | retail  | guild-base-1.03c-ru               |
| 1.04a        | Patch 1.04a      | German (DE)    | Guild.exe                        | Released shortly before add-on launch; improved voice files                                | patch   | guild-base-1.04a-de               |
| 1.05b3       | Beta Patch 3     | English (US/UK)| Guild.exe                        | Final patch for base game (Beta); widely used in GOG/Steam classic releases                | patch   | guild-base-1.05b3-en-int          |
| 1.05b3       | Beta Patch 3     | French (FR)    | Guild.exe                        | Rare French-language Beta patch, available via forums (JoWooD France)                      | patch   | guild-base-1.05b3-fr              |
| 2.0          | Gold + Add-on    | German (DE)    | Gold.exe / Europa1400Gold.exe   | Base expansion release; no TL.exe observed yet                                              | retail  | guild-gold-2.0-de                 |
| 2.0          | Gold + Add-on    | English (INT)  | Gold.exe                         | Some international discs labeled “Gold”; includes merged content                           | retail  | guild-gold-2.0-en-int             |
| 2.05         | Patch 2.05       | German (DE)    | Gold.exe                         | Some DE versions shipped with TL.exe optimized for hardware T&L                            | patch   | guild-gold-2.05-de                |
| 2.05         | Patch 2.05       | English (INT)  | Gold.exe                         | Some EN builds included TL.exe, others did not (regional variance)                         | patch   | guild-gold-2.05-en-int            |
| 2.06         | Final Patch      | German (DE)    | Gold.exe                         | Final and most stable version; used by Steam, GOG, etc.                                    | patch   | guild-gold-2.06-de                |
| 2.06         | Final Patch      | English (INT)  | 7d1f178f6463ab41f90987451187a93056814293832a5d2c76444dbd087e3ae8  Europa1400Gold.exe
6fe7a24c93192f6511bc8595eb82fd166db44f6cbeaf7c2f036838f3b6b4af45  Europa1400Gold_TL.exe
3cc2ce9049e41ab6d0eea042df4966fbf57e5e27c67fb923e81709d2683609d1  Server/server.dll
33399b878747d9a985f0f928ba3369e58aa5b2c346d845e8d29ed91a7921f194  d3_resource.dll
50e335fc9994d22d661591a44017c46bf7ff5bc31c6008558a897b4fcff8f0d4  d8_resource.dll
              | English final version found in official digital distribution                               | gog     | guild-gold-2.06-en-int-gog        |
| 2.06         | Final Patch      | English (INT)  | Europa1400Gold.exe              | English final version found in official digital distribution                               | steam   | guild-gold-2.06-en-int-steam      |
| 2.06         | Final Patch      | French (FR)    | Gold.exe                         | French Gold rarely seen physically, likely derived from EN binaries                        | retail  | guild-gold-2.06-fr                |
| 2.06         | Final Patch      | Russian (RU)   | Gold.exe                         | Some GOG builds include Russian Gold; presence of TL.exe unverified                        | digital | guild-gold-2.06-ru-gog            |
