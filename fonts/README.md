# Local font assets

These files preserve RelativityRush's existing Google Fonts typography without any external font request during app use. Only the normal-style Latin subsets are bundled; unsupported characters use the font stack's existing system fallback. The two sans-serif families use variable weight files, and Space Mono uses its two original static weights. Font files are copied without local modification.

| Family | Weights | Local file | Size |
|---|---|---|---:|
| DM Sans | 400–700 | [dm-sans-latin-variable.woff2](./dm-sans-latin-variable.woff2) | 36,932 bytes |
| Manrope | 400–800 | [manrope-latin-variable.woff2](./manrope-latin-variable.woff2) | 24,836 bytes |
| Space Mono | 400 | [space-mono-latin-400.woff2](./space-mono-latin-400.woff2) | 16,520 bytes |
| Space Mono | 700 | [space-mono-latin-700.woff2](./space-mono-latin-700.woff2) | 16,724 bytes |

## Sources and attribution

The WOFF2 subsets were provided by [Google Fonts CSS API](https://fonts.googleapis.com/css2?family=DM+Sans:wght@400..700&family=Manrope:wght@400..800&family=Space+Mono:wght@400;700&display=swap) and downloaded directly from fonts.gstatic.com on 2026-09-15. Exact versioned asset URLs, SHA-256 checksums, Unicode ranges and sizes are recorded in [sources.json](./sources.json).

Official source families and their complete SIL Open Font License 1.1 notices:

- **DM Sans:** [Google Fonts source](https://github.com/google/fonts/tree/main/ofl/dmsans) · [bundled copyright and license](./licenses/DM-Sans-OFL.txt)
- **Manrope:** [Google Fonts source](https://github.com/google/fonts/tree/main/ofl/manrope) · [bundled copyright and license](./licenses/Manrope-OFL.txt)
- **Space Mono:** [Google Fonts source](https://github.com/google/fonts/tree/main/ofl/spacemono) · [bundled copyright and license](./licenses/Space-Mono-OFL.txt)

Keep the bundled copyright and license notices with redistributed fonts. These fonts are provided by their respective authors; the family-specific notices identify the copyright holders and reserved font names.

## Integration and maintenance

Import **src/fonts.css** from the app's styles or entry point and remove the remote Google Fonts import. Every **@font-face** source points to the packaged **/fonts/** directory and uses **font-display: swap**. Normal builds and native packages do not need a network connection to fetch fonts.

To refresh the assets intentionally, run **node scripts/vendor-fonts.mjs** from the project. This maintenance command needs network access to the official Google Fonts hosts and the Google Fonts repository on GitHub. It validates the expected four Latin font faces, WOFF2 headers and license text before replacing the known outputs. Review the new checksums and visual typography after a refresh.
