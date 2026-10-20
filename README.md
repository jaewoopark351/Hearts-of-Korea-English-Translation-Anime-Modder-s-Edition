# Hearts of Korea English Translation (Anime Modder's Edition)

British English localisation for the current **Hearts of Korea** revision. The translation covers the mod's Korean text, including national focuses, events, news, decisions, national spirits, names, equipment and the domestic influence panel.

The aim is faithful English that sounds natural to a British reader, including someone unfamiliar with Korean history and culture. Accuracy takes priority over speed. The original alternative history, characters, humour and gameplay information are preserved.

## Playing in English

This is a localisation submod and requires the underlying Hearts of Korea content. Select **English** as the game language and enable the standard HoK revision followed by this translation. Keep **Korean Language** and the legacy English translation disabled for an English playthrough. After updating the files, restart the game to load the updated text.

The [mod descriptor](descriptor.mod) currently declares:

| Item | Declared value |
| --- | --- |
| Mod version | `1.0.0` |
| HOI4 version | `1.19.*` |
| Current translation Workshop item ID | `3823285419` |

The current release is [Hearts of Korea English Translation (Anime Modder's Edition)](https://steamcommunity.com/sharedfiles/filedetails/?id=3823285419). Item `3370616163` belongs to the legacy English translation and is not this release's upload target. These are metadata values; the compatibility checks completed so far are described below.

The descriptor lists both of these dependency names:

- `하츠 오브 코리아 Hearts of Korea[1.19 호환](씹덕 모드 제작자 개정)`
- `하츠 오브 코리아 Hearts of Korea[Road to 56 호환]`

The current translation targets the standard Korean source in `C:\hoi\hearts_of_korea`, published as [Hearts of Korea for HOI4 1.19](https://steamcommunity.com/sharedfiles/filedetails/?id=3793992662). Both dependency names exactly match the corresponding local mod descriptors and are retained as ordering entries. Their presence is not a declaration that the two base variants belong in the same playset or that this translation is compatible with both.

The local launcher configuration checked on 20 October has the standard HoK revision first and this translation second, with English selected. Korean Language, the legacy English translation and the Road to 56 variant are not enabled in that configuration. Subsequent game runs confirmed English output in sampled country selection, focus, national spirit, decision and event screens. The detailed scope and limitations are recorded in the [implementation and game verification report](docs/2026-10-20-implementation.md).

### Playsets to verify

| Test | Enabled content | Status |
| --- | --- | --- |
| A: standard English baseline | Current standard HoK revision and this translation; English language; Korean Language and the legacy translation disabled | Sampled English output confirmed; country-history follow-up below; introductory event overflow unresolved |
| B: Korean Language comparison | Test A with Korean Language added before the two HoK entries | Mixed Korean and English reproduced; unsuitable for an English playthrough |
| C: Road to 56 | The Road to 56, its HoK compatibility port and a separately reviewed English build; English language | Not tested in game; current standard build has static compatibility conflicts |

The installed Korean Language mod supplies English-channel Korean text and overlaps 79 translation keys, including country, party and place names. It also supplies fonts and interface files. In Test B, the main menus and some map labels became Korean while the sampled HoK country, party and focus names remained English. This is an observed result for that configuration, not a claim that all 79 overlaps were individually checked or that every load order behaves identically. The original HoK descriptor's dependency is preserved.

**Road to 56 requires separate compatibility work.** Its HoK port contains 27 keys absent from the standard source, and several shared state IDs refer to different places. For example, this translation names `STATE_1028` Hamgyeong, while the installed Road to 56 names it Dalarna. If this translation takes precedence, it can therefore rename unrelated regions. The RT56 dependency entry is retained, but this build should not be treated as a verified RT56 translation.

### Country history and long events

The country-selection history panel now has a larger text area and a scrollbar. The candidate allowed all three paragraphs of Korea's English history to be read at 1920×1080. The identical GUI file passed the deployed 1280×720 check with English selected, windowed mode, UI scale 1.0 and only the standard HoK and this translation enabled. Korea's final paragraph was accessible by dragging the scrollbar; Germany's shorter two-paragraph history fitted, and the country-selection button worked. These results cover the sampled country-history panel. The [UI verification report](docs/2026-10-20-ui-verification.md) records the conditions and evidence.

**The long introductory event still overflows.** Event-window trials C1, C2 and C3 did not provide usable access to both the complete text and the choices; C2 and C3 truncated the body. No event-window override was adopted. The country-history change does not resolve this event problem, and full release verification remains incomplete.

## Translation approach

- Translate the current Korean source in full, checking the surrounding events, focuses and scripts when meaning depends on context.
- Use natural British vocabulary, grammar and spelling. Established official names retain their recognised spelling.
- Preserve each speaker's voice, political perspective, irony and humour. Explain unfamiliar concepts through clear wording while retaining the Korean setting.
- Keep dates, quantities, costs, conditions, durations, cooldowns and cancellation rules precise.
- Preserve localisation keys and technical expressions, including variables, substitutions, colour codes, icons and escaped line breaks.
- Check existing English against the current Korean text before reusing it. The source mod's `english` directory contains substantial Korean text and is not a complete English translation.

## Update of 20 October 2026

This update was prepared against branch `feat/korean-focus-expansion-ai` in `C:\hoi\hearts_of_korea`, at source commit:

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

At the initial update stage, game display was untested. Later runs on HOI4 `1.19.3.0.c01a (b244)` confirmed sampled English text and reproduced a long-event overflow. They do not establish complete coverage of all branches, dynamic expressions, saved games, DLC combinations or Road to 56. Earlier logs and subsequent test logs are kept as separate evidence.

### Release audit of 20 October 2026

The local source still matches the commit above. The installed game's launcher metadata reports HOI4 `1.19.3.0`; the older `1.19.2` development records are not a test of this translation on the installed version.

The audit corrected the current Workshop ID in this README. The project's `descriptor.mod` and the registered local `.mod` already contained the correct ID, `3823285419`, and were preserved. Public Steam metadata identifies the new item as an HOI4 mod; matching upload dates do not prove that published source files are identical to the local Git commit.

Two English strings received small corrections: the RagnaROK option's ordinary status annotation now uses parentheses, and a past-tense error in the 1946 election event was corrected. The parenthesis change avoids confusion with dynamic-localisation notation; an actual engine error from the former brackets has not been reproduced. Valid variables and scripted expressions were left intact.

At the release-audit stage, game display checks could not proceed because the Windows Computer Use connection was unavailable. The connection subsequently recovered and allowed the A/B tests above. The historical [release audit](docs/2026-10-20-release-audit.md) retains its original NOT TESTED results; the [later implementation report](docs/2026-10-20-implementation.md) records the actual runs.

One source inconsistency is preserved in `KOR_conquest_indu_desc`: its opening verse refers to the west, while its parenthetical explanation refers to the east. The translation retains both rather than choosing a direction without sufficient evidence.

The later review compared all 2,971 Korean and English values and corrected 14 values in 10 files, including reinforcements described as volunteers, an ambiguous reference to communism, missing equipment wording and unclear policy descriptions. The subsequent country-history GUI change preserves those 37 localisation files and 2,971 keys. Unresolved source and script discrepancies are listed in the [source review notes](docs/source-review-notes.md). [Road to 56 support has a separate design](docs/rt56-compatibility-design.md); no RT56 build has been released by this work.

## Project files

```text
localisation/
  english/
    *_l_english.yml
    replace/
      *_l_english.yml
interface/
  frontendgamesetupview.gui
AGENTS.md
docs/
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

For RT56-specific work, use `C:\hoi\hearts_of_korea_Road_to_56` as the separate read-only Korean source. Keep its keys, state IDs and source version separate from the standard release.

Work in connected groups of focuses, spirits, decisions, tooltips and events. Compare the English with the Korean for meaning and completeness, then read the English independently for clarity and natural phrasing. Record unresolved source ambiguities and distinguish static checks from actual game observations.

Localisation `.yml` files must retain **UTF-8 with BOM**, the `l_english:` header and their existing technical syntax. HOI4 localisation is not ordinary YAML; generic YAML formatters must not rewrite these files.

The GUI override is the complete installed HOI4 `1.19.3` `interface/frontendgamesetupview.gui`, with only the shared country-history widget changed: `maxHeight` from `30` to `190`, and `scrollbartype = "standardtext_slider"` added. It applies to the country-selection history widget across countries. Other GUI definitions retain their installed bytes, and no `eventwindow.gui` is included. Future game updates require comparing this whole-file override with the new installed file and reapplying the small change. Compatibility with other UI mods that replace the same file is untested.

Create all new test scripts, fixtures, temporary reports, copied logs, screenshots and test backups inside this project's dedicated external directory:

```text
C:\hoi\test\hok-english-translation-anime\<task-or-run-id>\
```

The 20 October update's backups and review records are stored locally in:

```text
C:\hoi\test\hok-english-translation-anime\20261020-full-update-01\
```

That directory includes `completion_report.json`, `validation.json` and the translators' review records. It is separate from the mod's runtime files.

The later release audit, including its pre-change copies, scanner, dependency and Workshop identity reports, is stored in:

```text
C:\hoi\test\hok-english-translation-anime\20261020-release-audit-01\
```

The full text review and later UI investigations have separate local evidence folders:

```text
C:\hoi\test\hok-english-translation-anime\20261020-implementation-01\
C:\hoi\test\hok-english-translation-anime\20261020-implementation-02\
C:\hoi\test\hok-english-translation-anime\20261020-implementation-03\
```

Keep reports, logs, screenshots and backups as evidence. Remove one-off diagnostic code and temporary test mods after their work is finished, following `AGENTS.md`; preserve reusable tools and user files.

When reporting a translation issue, include the localisation key if available, the English shown, the corresponding Korean passage and the relevant screen or event. This makes it possible to check meaning and context together.

## Credits

Hearts of Korea's original creators and contributors retain credit for its setting, writing, gameplay and assets. This project provides English localisation for the current revision. Existing attribution comments are retained in the localisation files.
