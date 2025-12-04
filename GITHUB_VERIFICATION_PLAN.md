# GitHub Repository Verification Plan

**Status**: ⏳ Wartet auf Repository-Zugang  
**Erstellt**: 3. Dezember 2024  
**Zweck**: Verifizierung der Figma-Analyse gegen tatsächlichen Code

---

## Übersicht

Nach der vollständigen Figma-Analyse müssen wir die gefundenen Token-Namen und Patterns gegen den tatsächlichen SDX-Code verifizieren. Dies ist kritisch, um zu verstehen:

1. Wie Figma-Token-Namen in CSS-Variablen transformiert werden
2. Welches Token-System tatsächlich im Code verwendet wird
3. Ob es Code-only oder Figma-only Tokens gibt
4. Wie Component-Namen von Figma zu Web Components mappen

---

## Verifikations-Ziele

### 1. Token-Naming-Transformation

**Frage**: Wie werden Figma-Token-Namen zu CSS-Variablen?

**Beispiele zu testen**:
```
Figma: spacing/3
Code:  --spacing-3? --sdx-spacing-3? var(--spacing-3)?

Figma: fontSize/heading/M
Code:  --font-size-heading-m? --sdx-font-size-heading-m?

Figma: surface/ui/01
Code:  --surface-ui-01? --sdx-surface-ui-01?
```

**Zu prüfen**:
- [ ] Naming-Konvention (kebab-case, camelCase, etc.)
- [ ] Prefix-Konvention (`--sdx-` vs kein Prefix)
- [ ] Slash-zu-Dash-Transformation
- [ ] Groß-/Kleinschreibung-Handling

---

### 2. Token-System-Verifikation

**Frage**: Welches der 3 gefundenen Token-Systeme wird im Code verwendet?

**Systeme zu prüfen**:
1. **Primary System**: `spacing/3`, `fontSize/heading/M`
2. **SDX-Prefixed**: `sdx/font/size/h2`
3. **Legacy**: `space_old/baseline/2`

**Zu prüfen**:
- [ ] Welches System ist primär im Code?
- [ ] Sind SDX-prefixed Tokens im Code oder nur in Figma?
- [ ] Gibt es Legacy-Tokens noch im Code?
- [ ] Gibt es Migration-Warnungen oder Deprecation-Marker?

---

### 3. Token-Werte-Verifikation

**Frage**: Stimmen die Token-Werte zwischen Figma und Code überein?

**Zu prüfen**:
- [ ] Alle numerischen Werte (spacing, fontSize, etc.)
- [ ] Alle Color-Werte (hex, rgb, etc.)
- [ ] Alle Border-Radius-Werte
- [ ] Alle Font-Weight-Werte

**Beispiele**:
```
Figma: spacing/3 = 16px
Code:  --spacing-3 = 16px? ✓ oder unterschiedlich? ✗

Figma: color/brand/navy = #001155
Code:  --color-brand-navy = #001155? ✓
```

---

### 4. Component-Naming-Mapping

**Frage**: Wie mappen Figma-Component-Namen zu Web Component-Namen?

**Zu prüfen**:
- [ ] `Card_default` → `<sdx-card>`?
- [ ] `Button` (Type=Primary) → `<sdx-button theme="primary">`?
- [ ] `Inputfield` → `<sdx-input>`?
- [ ] `Checkbox` → `<sdx-checkbox>`?
- [ ] `Dropdown (select)` → `<sdx-select>`?

**Zu dokumentieren**:
- [ ] Vollständige Mapping-Tabelle Figma → Code
- [ ] Props/Attributes-Mapping
- [ ] Variant-Handling

---

### 5. Fehlende/Extra Tokens

**Frage**: Gibt es Tokens im Code, die nicht in Figma sind? Oder umgekehrt?

**Zu prüfen**:
- [ ] Code-only Tokens (nicht in Figma)
- [ ] Figma-only Tokens (nicht im Code)
- [ ] Unterschiedliche Token-Namen für gleiche Werte
- [ ] Zusätzliche Token-Skalen im Code

---

### 6. Responsive Patterns

**Frage**: Wie werden device-responsive Token-Patterns im Code implementiert?

**Zu prüfen**:
- [ ] Desktop/Mobile Token-Switching (z.B. `padding/3` mobile, `padding/4` desktop)
- [ ] Breakpoint-Definitionen
- [ ] Media Query-Patterns
- [ ] CSS Custom Properties für Responsive

---

## Repository-Struktur zu Erkunden

### Erwartete Verzeichnisse/Dateien

```
sdx-repository/
├── packages/
│   ├── components/          # Web Components
│   ├── tokens/              # Design Tokens
│   └── ...
├── docs/                    # Dokumentation
├── tokens.json              # Token-Definitionen?
├── tokens.css               # CSS Variables?
├── package.json
└── README.md
```

### Wichtige Dateien zu Finden

1. **Token-Definitionen**:
   - `tokens.json` oder ähnlich
   - `tokens.css` oder `variables.css`
   - TypeScript-Definitionen
   - Storybook-Token-Docs

2. **Component-Implementierungen**:
   - `sdx-button/`
   - `sdx-input/`
   - `sdx-checkbox/`
   - etc.

3. **Dokumentation**:
   - Storybook
   - README-Dateien
   - Usage-Examples

---

## Verifikations-Checkliste

### Phase 1: Repository-Exploration

- [ ] Repository klonen/öffnen
- [ ] Struktur verstehen
- [ ] Token-Dateien lokalisieren
- [ ] Component-Verzeichnisse finden
- [ ] Dokumentation durchsuchen

### Phase 2: Token-Analyse

- [ ] Token-Definitionsdatei(en) lesen
- [ ] CSS-Variable-Namen extrahieren
- [ ] Token-Werte extrahieren
- [ ] Naming-Patterns identifizieren
- [ ] System-Vergleich (Primary vs SDX vs Legacy)

### Phase 3: Component-Analyse

- [ ] Component-Namen sammeln
- [ ] Props/Attributes dokumentieren
- [ ] Variant-Handling verstehen
- [ ] Usage-Examples analysieren

### Phase 4: Vergleich & Mapping

- [ ] Figma-Tokens vs Code-Tokens vergleichen
- [ ] Naming-Transformation dokumentieren
- [ ] Component-Mapping-Tabelle erstellen
- [ ] Diskrepanzen identifizieren
- [ ] Gap-Analyse erstellen

### Phase 5: Dokumentation

- [ ] Verifikations-Report erstellen
- [ ] Token-Mapping-Tabelle erstellen
- [ ] Component-Mapping-Tabelle erstellen
- [ ] Empfehlungen aktualisieren
- [ ] TOKEN_SYSTEM_GUIDE.md aktualisieren

---

## Erwartete Ergebnisse

### Token-Mapping-Tabelle

| Figma Token | CSS Variable | Wert | Status | Notes |
|-------------|-------------|------|--------|-------|
| `spacing/3` | `--spacing-3` | 16px | ✅ Match | |
| `fontSize/heading/M` | `--font-size-heading-m` | 24px | ✅ Match | |
| `sdx/font/size/h2` | `???` | 32px | ❓ Unbekannt | Im Code gefunden? |
| `space_old/baseline/2` | `???` | 16px | ⚠️ Deprecated | Noch im Code? |

### Component-Mapping-Tabelle

| Figma Name | Web Component | Props/Attributes | Status |
|------------|---------------|------------------|--------|
| `Card_default` | `<sdx-card>` | - | ✅ Verified |
| `Button` (Primary) | `<sdx-button>` | `theme="primary"` | ✅ Verified |
| `Inputfield` | `<sdx-input>` | `type="text"` | ✅ Verified |

### Gap-Analyse

**Figma-only Tokens** (nicht im Code gefunden):
- `sdx/font/size/h2` - Nur in Figma?
- `sdx/border/radius-medium` - Nur in Figma?

**Code-only Tokens** (nicht in Figma gefunden):
- `--spacing-5` - Existiert im Code?
- `--padding-2` - Existiert im Code?

**Naming-Diskrepanzen**:
- Figma: `surface/ui/01` → Code: `--surface-ui-01` oder `--sdx-surface-ui-01`?

---

## Tools & Methoden

### Repository-Analyse

1. **Code-Suche**:
   ```bash
   # Finde alle CSS-Variablen
   grep -r "var(--" packages/
   
   # Finde Token-Definitionen
   find . -name "*token*" -o -name "*variable*"
   
   # Finde Component-Namen
   grep -r "sdx-" packages/components/
   ```

2. **JSON-Analyse** (falls Token-Dateien JSON sind):
   - Parse Token-Definitionen
   - Extrahiere Namen und Werte
   - Vergleiche mit Figma-Liste

3. **TypeScript-Analyse** (falls TypeScript-Definitionen existieren):
   - Type-Definitionen lesen
   - Token-Interfaces extrahieren

### Vergleichs-Tools

1. **Token-Vergleich**:
   - Figma-Token-Liste vs Code-Token-Liste
   - Name-Matching
   - Wert-Matching
   - System-Identifikation

2. **Component-Vergleich**:
   - Figma-Component-Namen vs Code-Component-Namen
   - Props/Attributes-Mapping
   - Variant-Mapping

---

## Offene Fragen für Verifikation

### Technisch

1. **Token-Format**:
   - [ ] JSON, CSS Variables, TypeScript, oder andere?
   - [ ] Wo werden Tokens definiert?
   - [ ] Wie werden sie in Components verwendet?

2. **Naming-Konvention**:
   - [ ] Welches Prefix-System wird verwendet?
   - [ ] Wie werden Slashes transformiert?
   - [ ] Groß-/Kleinschreibung-Regeln?

3. **Token-System**:
   - [ ] Welches System ist primär?
   - [ ] Sind SDX-prefixed Tokens im Code?
   - [ ] Gibt es Legacy-Tokens noch?

4. **Component-Naming**:
   - [ ] Wie werden Figma-Namen zu Code-Namen?
   - [ ] Props/Attributes-Konventionen?
   - [ ] Variant-Handling?

### Dokumentation

1. **Token-Dokumentation**:
   - [ ] Gibt es eine Token-Dokumentation?
   - [ ] Wo ist sie?
   - [ ] Ist sie aktuell?

2. **Component-Dokumentation**:
   - [ ] Storybook vorhanden?
   - [ ] Usage-Examples?
   - [ ] API-Dokumentation?

---

## Nächste Schritte Nach Verifikation

1. **TOKEN_SYSTEM_GUIDE.md aktualisieren**:
   - Verifizierte Token-Namen
   - Bestätigte CSS-Variable-Namen
   - Code-basierte Empfehlungen

2. **Component-Mapping-Dokument erstellen**:
   - Vollständige Figma → Code Tabelle
   - Props/Attributes-Guide
   - Usage-Examples

3. **Gap-Report erstellen**:
   - Figma-only Tokens
   - Code-only Tokens
   - Naming-Diskrepanzen
   - Empfehlungen für SDX Team

4. **Test-Szenarien aktualisieren**:
   - Basierend auf verifizierten Tokens
   - Realistische Component-Usage
   - Code-basierte Erwartungen

---

## Verifikations-Report-Template

```markdown
# SDX Token & Component Verification Report

**Date**: [Date]
**Repository**: [URL]
**Version**: [Version]

## Summary
- Tokens verified: X/Y
- Components verified: X/Y
- Discrepancies found: X

## Token Verification
[Token comparison table]

## Component Verification
[Component mapping table]

## Findings
[Key findings and discrepancies]

## Recommendations
[Updated recommendations based on code verification]
```

---

**Status**: ⏳ Wartet auf Repository-Zugang  
**Bereit für**: Repository-Analyse sobald Zugang gewährt wird

