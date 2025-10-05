# Татар теле өчен langdata

Бу каталог татар телен тану өчен кирәкле тел-специфик ресурсларны
җыеп тора. Файллар Tesseract тренировкалау кораллары белән куллану өчен
әзерләнгән һәм GitHub Actions эш агымында `tat.traineddata` артефактына
җыела.

## Каталогтагы төп файллар
- `tat.training_text` — татар телендә тематик һәм заманча лексикадан
  торган корпус.
- `tat.wordlist`, `tat.training_text.unigram_freqs`,
  `tat.training_text.bigram_freqs`, `tat.word.bigrams` — корпус нигезендә
  алынган сүзлек һәм статистика.
- `tat.numbers` һәм `tat.punc` — саннар һәм тыныш билгеләре үрнәкләре,
  Tesseract сүзлекләрен төзү өчен кирәк.
- `tat.unicharset` — татар тексты өчен актуаль символлар җыелмасы. Ул
  рус һәм казакъ ресурсларыннан алынган `Cyrillic.unicharset`,
  `Common.unicharset` һәм `Latin.unicharset` нигезендә автомат рәвештә
  төзелде.
- `tat.xheights` — кирилл шрифтлары өчен х-биеклек мәгълүматы. Файл
  `Cyrillic.xheights` нигезендә алынган.
- `tat.test_texts.txt` — тану сыйфатын тикшерү өчен кыска тест җөмләләр.

## `tat.traineddata` төзү
Локаль мохиттә эксперименталь пакет җыю өчен түбәндәге пәрманнарны
кулланыгыз (Tesseract 5 һәм аның тренинг утилиталары урнаштырылган булу
тиеш):

```bash
mkdir -p build
combine_lang_model \
  --input_unicharset tat/tat.unicharset \
  --script_dir . \
  --words tat/tat.wordlist \
  --numbers tat/tat.numbers \
  --puncs tat/tat.punc \
  --output_dir build \
  --lang tat \
  --version_str "tat langdata"
```

Җыелган `build/tat/tat.traineddata` файлы репозиторийга өстәлми, әмма
GitHub Actions артефакты буларак саклана.
