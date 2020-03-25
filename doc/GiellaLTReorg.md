# GiellaLT reorganisation before the move

The present layout of the language dirs in the GiellaLT infra has turned out to be too wieldy and hard to grasp. Because of that, a number of changes will be applied to the language directories before the move. They are as follows:

## The `src` directory

Before:

```
src/
├── filters
├── hyphenation
├── morphology
├── orthography
├── phonetics
├── phonology
├── syntax
├── tagsets
└── transcriptions
```

After:

```
src/
├── fst
│   ├── filters
│   ├── syllabification (from hyphenation)
│   ├── orthography
│   ├── phonetics
│   └── tagsets (if needed, maybe remove?)
└── cg3
```

`transcriptions` will be moved to `tools/` (and be renamed to `transcriptors`).

The idea is to switch from an organisation based on grammatical domain, to one based on language technology.

## The `tools` directory

Before:

```
tools/
├── analysers
├── grammarcheckers
├── hyphenators
│   ├── fstbased
│   └── patternbased
├── mt
│   ├── apertium
│   ├── cgbased
├── shellscripts
├── spellcheckers
│   ├── fstbased
│   │   ├── desktop
│   │   │   ├── foma
│   │   │   ├── hfst
│   │   │   └── weighting
│   │   └── mobile
│   │       ├── hfst
│   │       ├── vfst
│   │       └── weighting
│   └── listbased
└── tokenisers
```

After:

```
tools/
├── analysers
├── grammarcheckers
├── hyphenators
├── mt
│   ├── apertium
│   │   └── tagsets
│   └── cgbased
├── shellscripts
├── spellcheckers
├── transcriptors
└── tokenisers
```

## The `test` directory

It will be removed, and all tests will be moved to a separate test directory within the directory of the component the test is testing.

Before:

```
src/...
test/
├── src
│   ├── morphology
│   ├── orthography
│   ├── phonology
│   └── syntax
└── tools
    ├── hyphenators
    │   ├── fstbased
    │   └── patternbased
    ├── mt
    │   └── apertium
    └── spellcheckers
        └── fstbased
            ├── desktop
            │   └── hfst
            └── mobile
```

After:

```
./
├── src/
│   └── fst
│       └── test
└── tools/
    ├── analysers
    │   └── test
    ├── grammarcheckers
    │   └── test
    ├── hyphenators
    ├── ...
    ...
```
