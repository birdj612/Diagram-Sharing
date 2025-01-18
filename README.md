<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD056 -->

# A Snippet From My Current Sorting Config To Help Explain The Warehouse Layout

### Warehouse Layout Logic

```mermaid
%%{init: {
    'theme': 'dark',
    'look': 'classic',
    'themeVariables': {
        'textColor': '#ffffff',
        'fontSize': '16px',
        'fontFamily': 'Diavlo',
        'titleColor': '#ffffff',
        'clusterBorder': '#FF7F00',
        'nodeBorder': '#FF7F00',
        'lineColor': '#FF7F00',
        'mainBkg': '#222020',
        'clusterBkg': '#2121219c',
        'edgeLabelBackground':'#222020'
    },
    'flowchart': {
        'padding': 10,
        'diagramPadding': 50,
        'useMaxWidth': true,
        'nodeSpacing': 10,
        'rankSpacing': 30
    }
}}%%
graph TD
      Warehouse{{US WAREHOUSE LAYOUT}}
      Warehouse -...-> S1>PRIMARY ORDER:<br>FAMILY PROPERTIES]
      Warehouse -...-> S2>SECONDARY ORDER:<br>SUBFAMILY PROPERTIES]
      Warehouse -...-> S3>TERTIARY ORDER:<br>VARIANT PROPERTIES]

    subgraph FamilyGroups[FAMILIES]
      direction TB
      SpooledItems[SPOOLED ITEMS]
      HeavyBulky[HEAVY/BULKY ITEMS]
      Oddball[ODDBALL ITEMS]
      LongItems[LONG ITEMS]
      Delicate[DELICATE ITEMS]
      ChenilleWoolYarn[CHENILLE, WOOL & YARN ITEMS]
      Dubbing[DUBBING ITEMS]
      FurAndFeathers[FUR & FEATHERS]
      NewItems[NEW 'UNARRANGED' ITEMS]
      
      SpooledItems --> HeavyBulky
      HeavyBulky --> Oddball
      Oddball --> LongItems
      LongItems --> Delicate
      Delicate --> ChenilleWoolYarn
      ChenilleWoolYarn --> Dubbing
      Dubbing --> FurAndFeathers
      FurAndFeathers --> NewItems
    end

    subgraph SubfamilyGroups[SUBFAMILIES]
      direction TB
      Subfamily[SUBFAMILY]
      DefaultDirection[DEFAULT DIRECTION: <br> ASCENDING]
      ExceptionDirection[EXCEPTION DIRECTION: <br> DESCENDING]

      Subfamily --> DefaultDirection
      Subfamily --> ExceptionDirection
    end

    subgraph Variants[VARIANTS]
      direction TB
      Variant[VARIANT]
      VariantOrder[ORDER ALPHABETICALLY BY COLOR]

      Variant --> VariantOrder
    end
      
    S1 -.-> FamilyGroups
    S2 -.-> SubfamilyGroups
    S3 -.-> Variants
    
    class S1 info
    class S2 info
    class S3 info
    class Warehouse title

    classDef default stroke:#FF7F00,stroke-width:2px,rx:5,ry:5
    classDef info stroke:#FF7F00,stroke-width:.3px
    classDef title font-size:20px
```

## Terminology and Sku Variation I am Working on Documenting

### Sku Terminology WIP

```mermaid
---
config:
  theme: dark
  look: classic
  themeVariables:
    textColor: '#ffffff'
    fontSize: 16px
    fontFamily: Diavlo
    titleColor: '#ffffff'
    clusterBorder: '#FF7F00'
    nodeBorder: '#FF7F00'
    lineColor: '#FF7F00'
    mainBkg: '#222020'
    clusterBkg: '#2121219c'
    edgeLabelBackground: '#222020'
  flowchart:
    padding: 10
    diagramPadding: 50
    useMaxWidth: true
    nodeSpacing: 10
    rankSpacing: 35
    curve: basis
  layout: fixed
---
flowchart TB
    SKU{{"SKU"}} -.-> Digit1["1ST DIGIT: PACKAGE"] & Digit2_4["2-4TH DIGITS: FAMILY"] & Digit5_7["5-7TH DIGITS: SUBFAMILY"] & Digit8_10["8-10TH DIGITS: VARIANT"]
    Digit5_7 ---> Size1["DENIER SIZE:<br>030"] & Size2["MILLIMETER SIZE:<br>015"] & Size3["WORD SIZE:<br>BIG"] & Size4["NOT A SIZE?"]
     SKU:::title
    classDef default stroke:#FF7F00,stroke-width:1px,rx:200,ry:15,letter-spacing:1px
    classDef background fill:#222020,stroke:#FF7F00,stroke-width:0px,color:transparent
    classDef title font-size:30px

```

### Sku Variation From Standard WIP

<hr style="height:1px; solid #666;">

```mermaid
---
config:
  theme: dark
  look: classic
  fontFamily: diavlo
---
flowchart TB
    P2["EXCEPTION:<br>PACKAGE 2"] ---> F1["FAMILY"]
    P1["NORMAL:<br>PACKAGE 1"] -.-> EX1["EGGSTATIC:<br>BEGX"]
    P2 -.-> EX2["EGGSTATIC:<br>MEGX"]
    P1 ---> F1
    F1 --> SF1["SUBFAMILY"]
    SF1 --> V1["VARIANT"]
    P4["EXCEPTION:<br>PACKAGE 2"] ---> F2["FAMILY"]
    P3["NORMAL:<br>PACKAGE 1"] -.-> EX3["PROMOTIONAL STICKER SILVER:<br>BMCH000"]
    P4 -.-> EX4["FOAM VICE &amp; DISPLAY MAT:<br>WMCH000"]
    P3 ---> F2
    F2 --> SF2["SUBFAMILY"]
    SF2 --> NV["NO VARIANTS"]
    P6["EXCEPTION:<br>PACKAGE 2"] ---> F3["FAMILY"]
    P5["NORMAL:<br>PACKAGE 1"] -.-> EX5["NANO 300D SALTWATER &amp; HAIR STACKER:<br>SNAN300"]
    P6 -.-> EX6["NANO SILK 50D COLLECTION BOX:<br>DNAN050"]
    P5 ---> F3
    F3 --> NS["NO SUBFAMILIES"]
    Path4["ERRORS?"] --> P7["INCORRECT DIGITS<br>APROX: 17"] & P8["MISTAKE<br>APROX: ?"]
    P7 -.-> EX7["TAIL FIBRE FIBBETS CLARET:<br>BFIB000DCLT"]
    P8 -.-> EX8["DRY FLY POLYYARN BURGUNDY:<br>DDFPBOXBUG"]
    Path5["WEIRD?"] --> P9["NOT UPDATED AS VARIANTS?<br>APROX: 18"] & P10["DISCONTINUED?<br>APROX: 9"]
    P9 -.-> EX9["LEAD WIRE NATURAL"]
    P10 -.-> EX10["DRY FLY POLYYARN CADDIS GREY / BROWN:<br>SDFP000CGB"]
    Path6["MISMATCHED NAME APROX: 41"] -..-> EX11["1/69 HOLOGRAPHIC TINSEL:<br>ST69M69"]
    Root{{"SKU VARIATION"}} -..-> Path1["STANDARD"] & Path2["STANDARD<br>NO VARIANTS<br>APROX: 10"] & Path3["STANDARD<br>NO VARIANTS<br>NO SUBFAMILY<br>APROX: 15"] & Path4 & Path5 & Path6
    Path1 --> P1 & P2
    Path2 --> P3 & P4
    Path3 --> P5 & P6
    Path4@{ shape: rounded}
    Path5@{ shape: rounded}
    Path6@{ shape: rounded}
    Path1@{ shape: rounded}
    Path2@{ shape: rounded}
    Path3@{ shape: rounded}
     EX1:::EX
     EX2:::EX
     EX3:::EX
     EX4:::EX
     EX5:::EX
     EX6:::EX
     Path4:::centerText
     Path4:::path
     EX7:::EX
     EX8:::EX
     Path5:::centerText
     Path5:::path
     EX9:::EX
     EX10:::EX
     Path6:::path
     EX11:::EX
     Root:::title
     Path1:::centerText
     Path1:::path
     Path2:::path
     Path3:::path
    classDef centerText text-align:center
    classDef title font-size:50px
    classDef default stroke:#FF7F00,stroke-width:1px,rx:200,ry:30,letter-spacing:3px
    classDef background fill:#222020,stroke:#FF7F00,stroke-width:0px,color:transparent
    classDef EX stroke-dasharray:11,stroke:#ff6d1f,stroke-width:2px
    classDef path rx:200,ry:5
```

### I Also Want to Figure Out How the Product System Hierarchy Works, and Update the Terminology WIP

<hr style="height:1px; solid #666;">

```mermaid
---
config:
  theme: dark
  layout: fixed
  look: classic
  fontFamily: diavlo
---
flowchart TD
    A["PRODUCT?"] --> B1["ALSO PRODUCT?<br>ALSO VARIANT?<br>ITEM?"] & n4["ALSO PRODUCT?<br>ALSO VARIANT?<br>ITEM?"]
    B1 --> C1["FAMILY"]
    C1 --> D1["SUBFAMILY"] & n1["SUBFAMILY"]
    D1 --> E1["VARIANT"] & E2["VARIANT"]
    n1 --> n2["VARIANT"] & n3["VARIANT"]
    n4 --> n5["FAMILY"]
    n5 --> n6["SUBFAMILY"] & n7["SUBFAMILY"]
    n6 --> n8["VARIANT"] & n9["VARIANT"]
    n7 --> n10["VARIANT"] & n11["VARIANT"]
    n4@{ shape: rect}
    n1@{ shape: rect}
    n2@{ shape: rect}
    n3@{ shape: rect}
    n5@{ shape: rect}
    n6@{ shape: rect}
    n7@{ shape: rect}
    n8@{ shape: rect}
    n9@{ shape: rect}
    n10@{ shape: rect}
    n11@{ shape: rect}
    classDef default stroke:#FF7F00,stroke-width:1px,rx:200,ry:20,letter-spacing:3px
```

<hr style="height:1px; solid #666;">

```mermaid
---
config:
  theme: dark
  layout: dagre
  look: classic
  fontFamily: diavlo
  themeVariables:
    fontFamily: diavlo
---
flowchart TD
    A["NANO SILK 30D 18/0"] --> B1["NANO SILK 30D 18/0 BLACK"] & n4["NANO SILK 30D 18/0 BRICK BEIGE"]
    B1 --> C1["NAN"]
    C1 --> D1["030"]
    D1 --> E1["BLACK"]
    n5["NAN"] --> n6["030"]
    n6 --> n7["BRICK BEIGE"]
    n4 --> n5
    n8["PRODUCT?"] --> n9["ALSO PRODUCT?<br>ALSO VARIANT?<br>ITEM?"] & n10["ALSO PRODUCT?<br>ALSO VARIANT?<br>ITEM?"]
    n9 --> n11["FAMILY"]
    n11 --> n12["SUBFAMILY"]
    n12 --> n13["VARIANT"]
    n14["FAMILY"] --> n15["SUBFAMILY"]
    n15 --> n16["VARIANT"]
    n10 --> n14
    A@{ shape: rect}
    n4@{ shape: rect}
    n5@{ shape: rect}
    n6@{ shape: rect}
    n7@{ shape: rect}
    n8@{ shape: rect}
    n9@{ shape: rect}
    n10@{ shape: rect}
    n11@{ shape: rect}
    n12@{ shape: rect}
    n13@{ shape: rect}
    n14@{ shape: rect}
    n15@{ shape: rect}
    n16@{ shape: rect}
    classDef default stroke:#FF7F00,stroke-width:1px,rx:200,ry:30,letter-spacing:3px
```

---

## 1. Primary Order

### This is the main sorting config that defines the order of product families

```javascript
familyOrder: [
// first are the spooled items as they are the heaviest and fit best at the bottom
    "NAN", // nanosilk
    "CWT", // classic waxed thread 240yd + 3/0 120yd
    "CWX", // classic waxed thread 110yd
    "DBY", // dirty bug yarn
    "DFP", // dry fly polyyarn
    "GMF", // gel core body micro fritz
    "MGL", // micro glint nymph tinsel
    "MMT", // micro metal hybrid thread, tinsel & wire
    "FBR", // fluoro brite
    "WIR", // wire
    "LED", // lead free wire and adhesive flat lead foil sheet
    "LPB", // lead wire
    "CKY", // cheeky uv
    "STL", // straggle legs
    "STS", // straggle string
    "STI", // ice chenille straggle
    "OTN", // french tinsel
    "FBD", // flat braid
    "FLO", // fly tying floss
    "PDG", // perdigon body
    "SPY", // spyder thread
    "SLK", // pure silk
    "STE", // stainless steel fly & brush wire
    "T16", //
    "T32", //
    "T69", //
    "PQS", // peacock quill subs

// second are the heavy/bulky items
    // dispensers,
    // collections,
    "EDB", // empty dubbing boxes and flash storage pot
    "SPC", // 10 Spool storage case
    "FPB", // hi float plastazote foam block
    "FFT", // flat fly tyers foam
    "FFD", // double decker foam
    "TBD", // tungsten slotted beads

// third are the oddball items
    // merch
    // tools
    // stickers
    "MCH", // merch
    "WAX", // wax
    "UVT", // uv tools
    "TRD", // empty spool display box
    "6FG", // six finger scissors
    "CLP", // fly display clips
    // Ect.

// fourth are the long items that may need to be placed in a particular way to fit in the box
    // multicards
    "GMC", // game changer chenille pack
    "CSH", // synthetic cashmere monkey
    "KKF", // semperFlash krystal
    "H69", // SemperFlash Holographic 1/69
    "H32", // SemperFlash Holographic 1/32
    "SFM", // SemperFlash fucking multi
    "PSW", // streamer wing
    "SFB", // semperFlash blends + baitfish wing
    "PFB", // predator fibres
    "SLW", // synthetic lumi wing

// fifth are the more delicate items so they have a solid flat-ish surface under them and soft products on top
    "IBT", // inferno goose biots
    "NBT", // natural range goose biots
    "SJC", // synthetic jungle cock
    "JCB", // jungle cock bulk
    "THX", // sandys thorax magic colour enhancing tape
    "ORG", // sparkle organza
    "PQL", // transparent peccary + true peccary + perfect quills
    "EYE", // 3d epoxy eyes
    "BSP", // bodyspan spandex elastic
    "FIB", // tail fibre fibbets
    "MCD", // mylar cord
    "SKN", // semperSkin shrimp
    "SLG", // siliLegs

// sixth are the chenille, wool, and yarn items
    "BRB", // body n rib
    "SST", // swiss straw synthetic raffia
    "WOL", // wool
    "PYN", // polyyarn
    "EGG", // egg yarn
    "EGX", // eggStatic
    "FCH", // fry chenille '30mm xxl'
    "TGD", // gold tinsel fleck
    "TSV", // silver tinsel fleck
    "TSP", // copper tinsel fleck
    "CSP", // metallic tinsel chenille
    "MOP", // mopster mop chenille
    "TCH", // plush translucent chenille
    "CAM", // camo chenille
    "XST", // extreme string
    "GHC", // guard hair chenille
    "SCH", // solid chenille
    "WCH", // worm chenille
    "CHS", // suede chenille 1mm
    "SC2", // suede chenille 1.5mm
    "SC3", // suede chenille 2mm
    "PSC", // pearl chenille
    "ICE", // ice chenille

// seventh are the dubbing items
    "IDB", // ice dubbing
    "KPK", // kapok dubbing
    "SCD", // scud dubbing
    "SKD", // sparkle dubbing
    "SFD", // superfine dubbing
    "BOM", // boom dubbing
    "SEA", // semperSeal subs

// eighth fur and feathers
    "CFR", // semperFur
    "SRZ", // synthetic rabbit zonker strips

// ninth are the newer items we haven't had time to rearrange yet
    "SPH", // synthetic peacock herl
    "MAR", // synthetic marabou
    "CMN", // competition chenille
    "CMP", // competition uv chenille
    "EDG", // edgeBrite
    "GFR", // semperFut grizzle
    "HKC", // hackle chenille
    "HKU", // uv hackle chenille
    "KP2", // kapok fusion dubbing
    "KV2", // kapok fusion uv dubbing
    "Lat", // latex sheet
    "SBK", // scud back
    "LAT", // latex sheet
]
```

## 2. Secondary Order

### The subfamilies are sorted in ascending or descending order within the family groups

```javascript
  defaultDirection: "ascending", // Default sort direction for families
  exceptionDirection: {
    FFD: "descending", // double decker foam
    PQS: "descending", // peacock quill subs
    OTN: "descending", // french tinsel
  },
```

## 3. Tertiary Order

### The variants are sorted alphabetically according to the color
