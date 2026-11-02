# Internationalization Evidence

Verified 2026-10-21.

- [W3C Internationalization Quick Tips](https://www.w3.org/International/quicktips/index) recommends UTF-8, declared language, semantic markup, translatable content, local form formats, visible locale navigation, RTL direction, and validation. It is a concise route to deeper W3C guidance, not a complete checklist.
- [W3C: Declaring language in HTML](https://www.w3.org/International/questions/qa-html-language-declarations) recommends `lang` on the `html` element, language changes on containing elements, BCP 47 tags, and `dir` for bidirectional content.
- [Unicode CLDR](https://cldr.unicode.org/) provides curated locale data and algorithms for dates, numbers, currencies, units, plural rules, collation, and other regional behavior. Release 48.2 was the latest stable line shown when verified; 49 was beta.
- [ECMA-402](https://tc39.es/ecma402/) specifies JavaScript internationalization APIs such as locale negotiation and formatting. The online document tracks a future edition; verify browser support for the concrete APIs used.
- Use the project's accessibility and compatibility skills for language announcements, direction, keyboard behavior, glyphs, and target-environment testing.

## Data Modeling Boundary

Store instants and time zones according to the domain need; a UTC timestamp alone may not preserve a future local appointment. Store monetary amount and currency explicitly; formatting does not perform exchange. Store canonical identifiers separately from translated labels. Treat human names, addresses, and sort order as culturally variable data, not fixed field templates.
