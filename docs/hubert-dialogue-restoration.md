# Curated dialogue restoration audit

Source: `Pokemon_Hubert_Curated_Dialogue_Restoration.txt` supplied by the user.
Baseline: `4f946b09634647c4c75e700e2143d975dacf4c6c` on `master`.

## Result

54 of 57 candidates have verified source locations and restored custom text.
This includes all six explicitly required entries: 13, 32, 33, 34, 39, and 43.
Entry 26 restores the lab sign only; its concatenated city-name fragment is not independently assigned.
Entries 25 and 27 remain unresolved. Entry 49 is intentionally unchanged because
its only difference is the player/rival naming already handled by the game.

The prior automatic player name `Hubert`, rival name `Mo Light`, naming-screen
input, and save-name storage are unchanged. This change modifies text resources
and two text constants in `src/battle_message.c`; it does not change event
scripts, items, battles, maps, save layouts, or other gameplay logic.

## Matching and formatting

- Entries 01-24 coincide exactly with named original-text addresses in the local
  reference build's symbol map. Their labels and script callers were also checked.
  In particular, 01 is the Pallet Town technology NPC, 15 is the SPEAROW nickname
  sign, and 17-18 are the boy and youngster in Viridian's Pokemon Center.
- Relocated entries were matched by distinctive text, speaker/event context, and
  source references, rather than treating their old-ROM addresses as write targets.
- The old edited ROM itself is not attached in this task. Its repointed text
  pointers and exact control bytes cannot be independently recovered from the list.
- Decoder `[control/unknown]` markers and slash separators are never inserted.
  Text uses FireRed's `POKéMON`/`POKé BALLS` spelling, `\n` line breaks,
  `\l` scrolling, `\p` paragraphs, and `$` terminators.
- Player and rival references use `{PLAYER}` and `{RIVAL}`. The battle tutorial
  retains `{B_PLAYER_NAME}`, which is interpreted by the battle text engine.
  `Hubert Version`, `HubertTerTer`, and `Hunter` are deliberate title/streamer
  references in the supplied introduction, not manual player-name substitutions.
- The three introduction candidates form a continuous passage across the existing
  three intro pages. No missing continuation was invented; spacing and punctuation
  at the joins were normalized, including `push on. May`.
- Recovered spellings such as `defet`, `dont`, and `Melted Caugh Drops` are retained.
  The requested correction is rendered as `She's scared of me!` in entry 16.
- Entry 53 matches the old man's catching tutorial. Its missing opening is retained
  verbatim from the source (`Well, now, I've`) before the recovered `had my Hard Vodka`.
  Catching-tutorial behavior is unchanged.
- Shared kitchen and machine text (19-20) remain shared resources; the jokes appear
  wherever their existing flavor-text scripts are used.

## Entry-by-entry status

`Required` marks the six mandatory entries. Each source label remains reachable
through its existing event, intro, or battle-text reference.

| Entry | Old-ROM offset | Source text label | Result |
| --- | --- | --- | --- |
| 01 | `0x17D80D` | `PalletTown_Text_CanStoreItemsAndMonsInPC` | Restored |
| 02 | `0x17D895` | `PalletTown_Text_TownSign` | Restored |
| 03 | `0x17DABB` | `ViridianCity_Text_CanCarryMonsAnywhere` | Restored |
| 04 | `0x17DB78` | `ViridianCity_Text_ViridiansGymLeaderReturned` | Restored |
| 05 | `0x17DC99` | `ViridianCity_Text_GoShoppingInPewterOccasionally` | Restored |
| 06 | `0x17DD03` | `ViridianCity_Text_ThisIsPrivateProperty` | Restored |
| 07 | `0x18329D` | `Route1_Text_WorkAtPokeMartTakeSample` | Restored |
| 08 | `0x18343A` | `Route1_Text_RouteSign` | Restored |
| 09 | `0x18D43E` | `PalletTown_PlayersHouse_1F_Text_MovieOnTVFourBoysOnRailroad` | Restored |
| 10 | `0x18D492` | `PalletTown_PlayersHouse_1F_Text_MovieOnTVGirlOnBrickRoad` | Restored |
| 11 | `0x18D53B` | `PalletTown_PlayersHouse_2F_Text_PressLRForHelp` | Restored |
| 12 | `0x18D60A` | `PalletTown_RivalsHouse_Text_ErrandForGrandpaThisWillHelp` | Restored |
| 13 | `0x18EAF4` | `PalletTown_ProfessorOaksLab_Text_EmailMessage` | Restored; required |
| 14 | `0x18F004` | `PalletTown_ProfessorOaksLab_Text_OakNeedYourHelpTooNeedToSeePokedexes` | Restored |
| 15 | `0x18F33D` | `ViridianCity_House_Text_SpearowNameSpeary` | Restored |
| 16 | `0x190384` | `ViridianCity_PokemonCenter_1F_Text_FeelFreeToUsePC` | Restored |
| 17 | `0x1903E5` | `ViridianCity_PokemonCenter_1F_Text_PokeCenterInEveryTown` | Restored |
| 18 | `0x190450` | `ViridianCity_PokemonCenter_1F_Text_PokeCentersHealMons` | Restored |
| 19 | `0x1C0E40` | `Text_Kitchen` | Restored |
| 20 | `0x1C1060` | `Text_PowerPlantMachine` | Restored |
| 21 | `0x1C5A04` | `gPikachuIntro_Text_Page1` | Restored |
| 22 | `0x1C5AEB` | `gPikachuIntro_Text_Page2` | Restored |
| 23 | `0x1C5BB9` | `gPikachuIntro_Text_Page3` | Restored |
| 24 | `0x1C5C78` | `gOakSpeech_Text_WelcomeToTheWorld` | Restored |
| 25 | `0x71A23D` | Unresolved TRAINER TIPS sign | Deferred: no original text or pointer identifying which sign |
| 26 | `0x71A26C` | `PalletTown_Text_OakPokemonResearchLab` | Lab sign restored; adjacent fragment unresolved |
| 27 | `0x71A2C0` | Likely `Text_DishesPlatesNeatlyLinedUp` | Deferred: recovered text begins mid-word; full wording unavailable |
| 28 | `0x71A2E7` | `PalletTown_PlayersHouse_1F_Text_LookingGreatTakeCare` | Restored |
| 29 | `0x71A35A` | `PalletTown_PlayersHouse_1F_Text_AllGirlsLeaveOakLookingForYou` | Restored |
| 30 | `0x71A3D2` | `PalletTown_PlayersHouse_1F_Text_AllBoysLeaveOakLookingForYou` | Restored |
| 31 | `0x71A44A` | `ViridianCity_Text_WantToKnowAboutCaterpillarMons` | Restored |
| 32 | `0x71A4C1` | `gOakSpeech_Text_SoYourNameIsPlayer` | Restored; required |
| 33 | `0x71A4EE` | `gOakSpeech_Text_ConfirmRivalName` | Restored; required |
| 34 | `0x71A503` | `gOakSpeech_Text_RememberRivalsName` | Restored; required |
| 35 | `0x71A68B` | `PalletTown_PlayersHouse_2F_Text_PlayedWithNES` | Restored |
| 36 | `0x71A6DA` | `PalletTown_PlayersHouse_1F_Text_YouShouldTakeQuickRest` | Restored |
| 37 | `0x71A70A` | `PalletTown_RivalsHouse_Text_HiBrothersAtLab` | Restored |
| 38 | `0x71A74B` | `PalletTown_RivalsHouse_Text_LikeMeToGroomMon` | Restored |
| 39 | `0x71A852` | `PalletTown_ProfessorOaksLab_Text_OakThreeMonsChooseOne` | Restored; required |
| 40 | `0x71A9B2` | `PalletTown_ProfessorOaksLab_Text_OakWhichOneWillYouChoose` | Restored |
| 41 | `0x71AB96` | `PalletTown_ProfessorOaksLab_Text_RivalLetsCheckOutMons` | Restored |
| 42 | `0x71AC87` | `gText_WinEarnsPrizeMoney` | Restored |
| 43 | `0x71AD10` | `PalletTown_ProfessorOaksLab_Text_RivalGoToughenMyMon` | Restored; required |
| 44 | `0x71AD6F` | `PalletTown_ProfessorOaksLab_Text_OakBattleMonForItToGrow` | Restored |
| 45 | `0x71ADCB` | `PalletTown_ProfessorOaksLab_Text_OakHaveSomethingForMe` | Restored |
| 46 | `0x71AE79` | `PalletTown_ProfessorOaksLab_Text_OakCustomBallIOrdered` | Restored |
| 47 | `0x71AF00` | `PalletTown_ProfessorOaksLab_Text_OakTakeTheseWithYou` | Restored |
| 48 | `0x71AF2F` | `PalletTown_ProfessorOaksLab_Text_ReceivedPokedexFromOak` | Restored |
| 49 | `0x71B270` | `PalletTown_ProfessorOaksLab_Text_RivalIllCompleteThePokedex` | Unchanged: source already matches except dynamic rival name |
| 50 | `0x71B32D` | `gText_ForPetesSake` | Restored |
| 51 | `0x71B415` | `ViridianCity_Text_GrandpaHasntHadCoffeeYet` | Restored |
| 52 | `0x71B463` | `ViridianCity_Text_CitySign` | Restored |
| 53 | `0x71B4A9` | `ViridianCity_Text_ShowYouHowToCatchMons` | Restored |
| 54 | `0x71B5F4` | `ViridianCity_Text_WeakenMonsFirstToCatch` | Restored |
| 55 | `0x71B6E5` | `ViridianCity_Text_GymClosedWonderWhoLeaderIs` | Restored |
| 56 | `0x71B743` | `ViridianCity_Text_GymSign` | Restored |
| 57 | `0x71B75F` | `ViridianCity_Mart_Text_ShopDoesGoodBusinessInAntidotes` | Restored |

## Remaining investigation

- **25 / 0x71A23D:** “TRAINER TIPS / Ice Bow is the worst META deck.” Multiple
  TRAINER TIPS signs exist, including two in Viridian City. The recovered entry
  contains no original wording, event identity, or usable pointer. Need the old
  edited ROM's referencing event/pointer, or the exact sign location, before placement.
- **27 / 0x71A2C0:** “aper plates saved up to / be used again.” This likely replaces
  the shared dishes/plates flavor text, but the beginning and any preceding sentence
  are missing. Need the full intended wording or the original edited ROM. The native
  dishes text is left intact rather than inventing a prefix.
- **26 / 0x71A26C (trailing fragment only):** “VIRDIDDYAN CITY” immediately follows
  the complete research-lab wording with no decoded separator. Only the unique lab
  sign is changed here. Entry 52 independently restores the verified Viridian city
  sign, but the provenance of this extra concatenated fragment remains unverified.
- **49 / 0x71B270:** Investigated and excluded as a name-only candidate: the existing
  National Dex scene already contains the supplied “Gramps, calm down” and
  “ONE ISLAND first…” dialogue, with `{RIVAL}` providing Mo Light. No rewrite is needed.

## Validation

- Fresh source snapshot compiled successfully with the existing agbcc compiler and
  ARM binutils: `make -j4 GAME_VERSION=FIRERED GAME_LANGUAGE=ENGLISH GAME_REVISION=0 MODERN=0 COMPARE=0`.
- A final repeat build completed successfully with nothing left to compile.
- Verified the exact encoded bytes of all 54 restored strings at their linked ROM
  symbol addresses, including dynamic placeholders and text control bytes.
- Verified both fixed name strings, 16 MiB ROM size, and GBA header checksum.
- Checked dialogue widths against the normal, male, and female Latin font tables,
  expanding names to Hubert and Mo Light. Intro checks include its extra letter
  spacing and existing eight-line limit. All checked lines fit their text windows.
- Confirmed `src/oak_speech.c`, `src/new_game.c`, `src/naming_screen.c`, and
  `include/global.h` are byte-for-byte unchanged from the baseline.
- Confirmed the only changed C lines are the two battle text constants.
- `git diff --check` passed. No emulator playthrough or visual inspection has been
  performed; intro/name confirmation, both TV variants, signs, and the postgame
  National Dex dialogue should be checked in an emulator.
- No compiled ROM, intermediate build files, or recovery scripts are committed.

ROM SHA-256 (local verification only): `070b5cde69654a3a7eeca878d3a3e0cd17f150a72cae2f54e461afcaed88a25d`.
