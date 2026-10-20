# Hearts of Korea English Translation (Anime Modder's Edition)

British English localisation for the current **Hearts of Korea** revision. The translation covers the mod's Korean text, including national focuses, events, news, decisions, national spirits, names, equipment and the domestic influence panel.

The aim is faithful English that sounds natural to a British reader, including someone unfamiliar with Korean history and culture. Accuracy takes priority over speed. The original alternative history, characters, humour and gameplay information are preserved.

## Playing in English

This is a localisation submod and requires the underlying Hearts of Korea content. Select **English** as the game language to use these translations. After updating the files, restart the game to load the updated text.

The [mod descriptor](descriptor.mod) currently declares:

| Item | Declared value |
| --- | --- |
| Mod version | `1.0.0` |
| HOI4 version | `1.19.*` |
| Translation Workshop item ID | `3370616163` |

These are metadata values; the compatibility checks completed so far are described below.

The descriptor lists both of these dependency names:

- `하츠 오브 코리아 Hearts of Korea[1.19 호환](씹덕 모드 제작자 개정)`
- `하츠 오브 코리아 Hearts of Korea[Road to 56 호환]`

The current translation follows the Korean source in `C:\hoi\hearts_of_korea`. The intended combination of these dependencies, their launcher load order and Road to 56 compatibility have not been verified in game. The dependency list alone does not establish whether the two releases should be enabled together or used separately.

## Translation approach

- Translate the current Korean source in full, checking the surrounding events, focuses and scripts when meaning depends on context.
- Use natural British vocabulary, grammar and spelling. Established official names retain their recognised spelling.
- Preserve each speaker's voice, political perspective, irony and humour. Explain unfamiliar concepts through clear wording while retaining the Korean setting.
- Keep dates, quantities, costs, conditions, durations, cooldowns and cancellation rules precise.
- Preserve localisation keys and technical expressions, including variables, substitutions, colour codes, icons and escaped line breaks.
- Check existing English against the current Korean text before reusing it. The source mod's `english` directory contains substantial Korean text and is not a complete English translation.

## Update of 20 October 2026

This update was prepared against source commit:

```text
d4031aaa0c1f85bb89b0e6ca21d041beade8bd26
```

| Recorded result | Count |
| --- | ---: |
| English localisation files | 37 |
| Keys matching the current Korean source | 2,971 |
| Previously missing keys added | 1,112 |
| Existing translation values revised | 1,155 |
| Existing values retained after review | 704 |
| Obsolete keys removed | 205 |

The old Japanese localisation override was replaced by the current source's namespaced content. Outdated map-name overrides were also removed so that old identifiers would no longer rename unrelated locations.

The recorded static checks passed: matching source and English key sets, no duplicate keys, no untranslated Korean display text, UTF-8 BOM and English headers, preserved key versions, protected tokens, escaped quotation marks and line-break counts. Translators checked the Korean text and English wording, with additional independent review of the country events and selected existing files.

**In-game verification remains outstanding:** actual load order, dynamic text rendering, font display, text overflow, and save, DLC and Road to 56 configurations have not been tested for this update. Existing logs were retained as evidence from before the changes, rather than treated as a test of the updated translation.

One source inconsistency is preserved in `KOR_conquest_indu_desc`: its opening verse refers to the west, while its parenthetical explanation refers to the east. The translation retains both rather than choosing a direction without sufficient evidence.

## Project files

```text
localisation/
  english/
    *_l_english.yml
    replace/
      *_l_english.yml
AGENTS.md
descriptor.mod
README.md
thumbnail.png
```

English strings use the game's `l_english:` channel. British English is the writing convention within that channel.

## Working on the translation

Read [AGENTS.md](AGENTS.md) before editing. The current Korean source and its related design notes are held in:

```text
C:\hoi\hearts_of_korea\localisation\korean\
C:\hoi\hearts_of_korea\docs\
```

Use that current source as the translation baseline. Historical releases can help establish provenance, but do not override its text or settings.

Work in connected groups of focuses, spirits, decisions, tooltips and events. Compare the English with the Korean for meaning and completeness, then read the English independently for clarity and natural phrasing. Record unresolved source ambiguities and distinguish static checks from actual game observations.

Localisation `.yml` files must retain **UTF-8 with BOM**, the `l_english:` header and their existing technical syntax. HOI4 localisation is not ordinary YAML; generic YAML formatters must not rewrite these files.

Create all new test scripts, fixtures, temporary reports, copied logs, screenshots and test backups inside this project's dedicated external directory:

```text
C:\hoi\test\hok-english-translation-anime\<task-or-run-id>\
```

The 20 October update's backups and review records are stored locally in:

```text
C:\hoi\test\hok-english-translation-anime\20261020-full-update-01\
```

That directory includes `completion_report.json`, `validation.json` and the translators' review records. It is separate from the mod's runtime files.

When reporting a translation issue, include the localisation key if available, the English shown, the corresponding Korean passage and the relevant screen or event. This makes it possible to check meaning and context together.

## Credits

Hearts of Korea's original creators and contributors retain credit for its setting, writing, gameplay and assets. This project provides English localisation for the current revision. Existing attribution comments are retained in the localisation files.
