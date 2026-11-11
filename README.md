# PHP Regex Symbols and Practical Examples - 746 Examples

**Operations covered:** `preg_match()`, `preg_match_all()`, `preg_replace()`, and `preg_split()`. Dates, email addresses, URLs, identifiers, and similar values are checked for **format**.

Regex combinations are effectively unlimited. These examples cover practical combinations instead of trying to list every theoretical permutation.

For HTML and CSS examples, regex was used only on a few **known and simple fragments**.

# Part I - Individual regex symbols

## A1. Individual symbols: character matching

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 1. Dot . - find the first character in a product reference | `~.~` | `$text = "X9"; preg_match('~.~', $text, $m); echo $m[0] ?? 'Not found';` | `X` |
| 2. Escaped dot \\. - find the literal decimal point in a price | `~\.~` | `$text = "19.95"; preg_match('~\\.~', $text, $m); echo $m[0] ?? 'Not found';` | `.` |
| 3. Digit \\d - read the first digit of a one-line code | `~\d~` | `$text = "Code A7"; preg_match('~\\d~', $text, $m); echo $m[0] ?? 'Not found';` | `7` |
| 4. Non-digit \\D - find the first letter before an ID | `~\D~` | `$text = "A123"; preg_match('~\\D~', $text, $m); echo $m[0] ?? 'Not found';` | `A` |
| 5. Word \\w - identify an underscore in an identifier | `~\w~` | `$text = "_field"; preg_match('~\\w~', $text, $m); echo $m[0] ?? 'Not found';` | `_` |
| 6. Non-word \\W - find punctuation in a short tag | `~\W~` | `$text = "user-name"; preg_match('~\\W~', $text, $m); echo $m[0] ?? 'Not found';` | `-` |
| 7. Whitespace \\s - locate a gap between two words | `~\s~` | `$text = "first last"; preg_match('~\\s~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `" "` |
| 8. Non-whitespace \\S - skip leading spaces to the next character | `~\S~` | `$text = "  Ready"; preg_match('~\\S~', $text, $m); echo $m[0] ?? 'Not found';` | `R` |
| 9. Horizontal space \\h - find a tab or ordinary space | `~\h~` | `$text = "A\tB"; preg_match('~\\h~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\t"` |
| 10. Vertical space \\v - detect a line-feed character | `~\v~` | `$text = "A\nB"; preg_match('~\\v~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\n"` |
| 11. Unicode newline \\R - find a Windows CRLF line break | `~\R~` | `$text = "First\r\nSecond"; preg_match('~\\R~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\r\n"` |
| 12. Unicode letter \\p{L} - find a Greek character | `~\p{L}~u` | `$text = "Ωmega"; preg_match('~\\p{L}~u', $text, $m); echo $m[0] ?? 'Not found';` | `Ω` |
| 13. Not a Unicode letter \\P{L} - find the digit after a name | `~\P{L}~u` | `$text = "Alice7"; preg_match('~\\P{L}~u', $text, $m); echo $m[0] ?? 'Not found';` | `7` |
| 14. Unicode digit \\p{Nd} - find an Arabic-Indic digit | `~\p{Nd}~u` | `$text = "Page ٣"; preg_match('~\\p{Nd}~u', $text, $m); echo $m[0] ?? 'Not found';` | `٣` |
| 15. Currency class \\p{Sc} - find a currency symbol | `~\p{Sc}~u` | `$text = "Price €39"; preg_match('~\\p{Sc}~u', $text, $m); echo $m[0] ?? 'Not found';` | `€` |
| 16. Unicode grapheme \\X - match one full accented character | `~\X~u` | `$text = "é"; preg_match('~\\X~u', $text, $m); echo $m[0] ?? 'Not found';` | `é` |
| 17. Tab escape \\t - detect a tab-delimited column separator | `~\t~` | `$text = "one\ttwo"; preg_match('~\\t~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\t"` |
| 18. Line-feed escape \\n - detect a Unix line break | `~\n~` | `$text = "one\ntwo"; preg_match('~\\n~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\n"` |
| 19. Carriage return \\r - detect a legacy line break | `~\r~` | `$text = "old\rnew"; preg_match('~\\r~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\r"` |
| 20. Hex byte escape \\x2E - match a literal dot | `~\x2E~` | `$text = "notes.txt"; preg_match('~\\x2E~', $text, $m); echo $m[0] ?? 'Not found';` | `.` |
| 21. Unicode hex escape \\x{20AC} - match a euro sign | `~\x{20AC}~u` | `$text = "Total €30"; preg_match('~\\x{20AC}~u', $text, $m); echo $m[0] ?? 'Not found';` | `€` |
| 22. Literal plus \\+ - detect a plus in arithmetic text | `~\+~` | `$text = "5+8"; preg_match('~\\+~', $text, $m); echo $m[0] ?? 'Not found';` | `+` |
| 23. Literal asterisk \\* - find a wildcard a user typed | `~\*~` | `$text = "Search dev*"; preg_match('~\\*~', $text, $m); echo $m[0] ?? 'Not found';` | `*` |
| 24. Literal question mark \\? - find a question in a prompt | `~\?~` | `$text = "Continue?"; preg_match('~\\?~', $text, $m); echo $m[0] ?? 'Not found';` | `?` |
| 25. Literal dollar \\$ - find a dollar price marker | `~\$~` | `$text = "Total \$25"; preg_match('~\\$~', $text, $m); echo $m[0] ?? 'Not found';` | `$` |
| 26. Literal caret \\^ - find a caret in a version constraint | `~\^~` | `$text = "Version ^2.0"; preg_match('~\\^~', $text, $m); echo $m[0] ?? 'Not found';` | `^` |
| 27. Literal parenthesis \\( - detect an opening parenthesis | `~\(~` | `$text = "call(arg)"; preg_match('~\\(~', $text, $m); echo $m[0] ?? 'Not found';` | `(` |
| 28. Literal square bracket \\[ - detect a list marker | `~\[~` | `$text = "[x] Done"; preg_match('~\\[~', $text, $m); echo $m[0] ?? 'Not found';` | `[` |
| 29. Literal curly brace \\{ - detect an opening template brace | `~\{~` | `$text = "{username}"; preg_match('~\\{~', $text, $m); echo $m[0] ?? 'Not found';` | `{` |
| 30. Literal hyphen - - find a dash between words | `~-~` | `$text = "pre-order"; preg_match('~-~', $text, $m); echo $m[0] ?? 'Not found';` | `-` |
| 31. Literal slash / - find a separator in a URL path | `~/~` | `$text = "/products"; preg_match('~/~', $text, $m); echo $m[0] ?? 'Not found';` | `/` |
| 32. Literal colon : - locate the separator in a field | `~:~` | `$text = "status:active"; preg_match('~:~', $text, $m); echo $m[0] ?? 'Not found';` | `:` |
| 33. Literal pipe via [\|] - detect a pipe delimiter | `~[\|]~` | `$text = "a\|b"; preg_match('~[\|]~', $text, $m); echo $m[0] ?? 'Not found';` | `\|` |
| 34. Literal backslash - detect a Windows path separator | `~\\~` | `$text = "C:\\Data\\file.txt"; preg_match('~\\\\~', $text, $m); echo $m[0] ?? 'Not found';` | `\` |
| 35. Literal hash # - detect the start of a hashtag | `~#~` | `$text = "#release"; preg_match('~#~', $text, $m); echo $m[0] ?? 'Not found';` | `#` |
| 36. Literal double quote - find a quoted value marker | `~"~` | `$text = "\"ready\""; preg_match('~"~', $text, $m); echo $m[0] ?? 'Not found';` | `"` |

## A2. Individual symbols: positions and anchors

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 37. Start anchor ^ - require a line to begin with SKU | `~^SKU~` | `$text = "SKU-491"; preg_match('~^SKU~', $text, $m); echo $m[0] ?? 'Not found';` | `SKU` |
| 38. End anchor $ - require the final text to say OK | `~OK$~` | `$text = "Status OK"; preg_match('~OK$~', $text, $m); echo $m[0] ?? 'Not found';` | `OK` |
| 39. Absolute start \\A - require a file header prefix | `~\AREPORT~` | `$text = "REPORT,2026"; preg_match('~\\AREPORT~', $text, $m); echo $m[0] ?? 'Not found';` | `REPORT` |
| 40. Absolute end \\z - require the last character to be ! | `~!\z~` | `$text = "Approved!"; preg_match('~!\\z~', $text, $m); echo $m[0] ?? 'Not found';` | `!` |
| 41. End-before-final-newline \\Z - find END before the final newline | `~END\Z~` | `$text = "Data END\n"; preg_match('~END\\Z~', $text, $m); echo $m[0] ?? 'Not found';` | `END` |
| 42. Word boundary \\b - find the standalone word ID | `~\bID\b~` | `$text = "Read ID: 45"; preg_match('~\\bID\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `ID` |
| 43. Non-boundary \\B - find an internal suffix in shipping | `~\Bing\b~` | `$text = "shipping"; preg_match('~\\Bing\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `ing` |
| 44. Reset-match-start \\K - return only the code after SKU- | `~SKU-\K\d+~` | `$text = "SKU-58412"; preg_match('~SKU-\\K\\d+~', $text, $m); echo $m[0] ?? 'Not found';` | `58412` |
| 45. Line start with m modifier - locate a TODO line | `~^TODO:~m` | `$text = "DONE\nTODO: fix\nNEXT"; preg_match('~^TODO:~m', $text, $m); echo $m[0] ?? 'Not found';` | `TODO:` |
| 46. Exact end with D modifier - reject a trailing newline | `~^ABC$~D` | `$text = "ABC\n"; echo preg_match('~^ABC$~D', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 47. First-match start with \\G - match a prefix at offset zero | `~\G\w+~` | `$text = "alpha beta"; preg_match('~\\G\\w+~', $text, $m); echo $m[0] ?? 'Not found';` | `alpha` |

## A3. Individual symbols: sets and quantifiers

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 48. Positive set [abc] - find the first allowed size letter | `~[SML]~` | `$text = "Size M"; preg_match('~[SML]~', $text, $m); echo $m[0] ?? 'Not found';` | `S` |
| 49. Negated set [^...] - find a forbidden punctuation mark | `~[^a-z0-9 ]~` | `$text = "user@name"; preg_match('~[^a-z0-9 ]~', $text, $m); echo $m[0] ?? 'Not found';` | `@` |
| 50. Set range [A-Z] - find an uppercase ticket prefix | `~[A-Z]~` | `$text = "aB12"; preg_match('~[A-Z]~', $text, $m); echo $m[0] ?? 'Not found';` | `B` |
| 51. Digit set [0-9] - find a digit using explicit ranges | `~[0-9]~` | `$text = "Unit 6"; preg_match('~[0-9]~', $text, $m); echo $m[0] ?? 'Not found';` | `6` |
| 52. Literal hyphen inside a set - find a product-code dash | `~[-]~` | `$text = "AB-42"; preg_match('~[-]~', $text, $m); echo $m[0] ?? 'Not found';` | `-` |
| 53. Literal closing bracket inside a set - find ] | `~[\]]~` | `$text = "[done]"; preg_match('~[\\]]~', $text, $m); echo $m[0] ?? 'Not found';` | `]` |
| 54. Star * - match zero or more A characters | `~A*~` | `$text = "AAAA4"; preg_match('~A*~', $text, $m); echo $m[0] ?? 'Not found';` | `AAAA` |
| 55. Plus + - collect one or more digits in a count | `~\d+~` | `$text = "Visitors 1280"; preg_match('~\\d+~', $text, $m); echo $m[0] ?? 'Not found';` | `1280` |
| 56. Question ? - allow an optional final s in an item name | `~items?~` | `$text = "item"; preg_match('~items?~', $text, $m); echo $m[0] ?? 'Not found';` | `item` |
| 57. Exact repeat {3} - collect a three-digit department code | `~\d{3}~` | `$text = "Dept 407"; preg_match('~\\d{3}~', $text, $m); echo $m[0] ?? 'Not found';` | `407` |
| 58. Repeat {2,} - collect at least two dashes | `~-{2,}~` | `$text = "Wait---"; preg_match('~-{2,}~', $text, $m); echo $m[0] ?? 'Not found';` | `---` |
| 59. Repeat {2,4} - collect two to four consecutive letters | `~[A-Z]{2,4}~` | `$text = "Code ABCR"; preg_match('~[A-Z]{2,4}~', $text, $m); echo $m[0] ?? 'Not found';` | `ABCR` |
| 60. Lazy star *? - stop at the first matching close marker | `~<.*?>~` | `$text = "<a><b>"; preg_match('~<.*?>~', $text, $m); echo htmlspecialchars($m[0] ?? 'Not found', ENT_QUOTES, 'UTF-8');` | `<a>` |
| 61. Lazy plus +? - stop at the first separator | `~\w+?=~` | `$text = "color=blue"; preg_match('~\\w+?=~', $text, $m); echo $m[0] ?? 'Not found';` | `color=` |
| 62. Lazy optional ?? - prefer omitting an optional character | `~ab??~` | `$text = "ab"; preg_match('~ab??~', $text, $m); echo $m[0] ?? 'Not found';` | `a` |
| 63. Lazy range {2,4}? - take the shortest permitted code | `~\d{2,4}?~` | `$text = "12345"; preg_match('~\\d{2,4}?~', $text, $m); echo $m[0] ?? 'Not found';` | `12` |
| 64. Possessive plus ++ - collect digits without backtracking | `~\d++~` | `$text = "12345X"; preg_match('~\\d++~', $text, $m); echo $m[0] ?? 'Not found';` | `12345` |
| 65. Possessive star *+ - consume spaces without backtracking | `~[ ]*+X~` | `$text = "   X"; preg_match('~[ ]*+X~', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"   X"` |
| 66. Possessive optional ?+ - take optional dash without retry | `~A-?+B~` | `$text = "A-B"; preg_match('~A-?+B~', $text, $m); echo $m[0] ?? 'Not found';` | `A-B` |
| 67. Possessive range {2,4}+ - collect bounded digits | `~\d{2,4}+~` | `$text = "87430"; preg_match('~\\d{2,4}+~', $text, $m); echo $m[0] ?? 'Not found';` | `8743` |
| 68. Alternation \| - accept one of two statuses | `~\bstatus:(on\|off)\b~` | `$text = "status:on"; preg_match('~\\bstatus:(on\|off)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `on` |

## A4. Individual symbols: groups and assertions

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 69. Capture (...) - extract a number following item # | `~item #(\d+)~` | `$text = "item #482"; preg_match('~item #(\\d+)~', $text, $m); echo $m[1] ?? 'Not found';` | `482` |
| 70. Noncapturing (?:...) - group units without extra captures | `~(?:cm\|mm)~` | `$text = "15 mm"; preg_match('~(?:cm\|mm)~', $text, $m); echo $m[0] ?? 'Not found';` | `mm` |
| 71. Named capture (?&lt;name&gt;...) - extract a product code | `~(?<sku>[A-Z]{3}\d{2})~` | `$text = "SKU ABC12"; preg_match('~(?<sku>[A-Z]{3}\\d{2})~', $text, $m); echo $m[1] ?? 'Not found';` | `ABC12` |
| 72. Backreference \\1 - find an exactly repeated word | `~\b(\w+)\s+\1\b~i` | `$text = "very very good"; preg_match('~\\b(\\w+)\\s+\\1\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `very very` |
| 73. Named backreference \\k&lt;name&gt; - find a repeated label | `~\b(?<tag>[a-z]+)-\k<tag>\b~` | `$text = "test-test"; preg_match('~\\b(?<tag>[a-z]+)-\\k<tag>\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `test-test` |
| 74. Positive lookahead (?=...) - find digits before kg | `~\d+(?=kg)~` | `$text = "Mass 25kg"; preg_match('~\\d+(?=kg)~', $text, $m); echo $m[0] ?? 'Not found';` | `25` |
| 75. Negative lookahead (?!...) - find cat not followed by s | `~cat(?!s)~` | `$text = "catnap"; preg_match('~cat(?!s)~', $text, $m); echo $m[0] ?? 'Not found';` | `cat` |
| 76. Positive lookbehind (?&lt;=...) - read the ID after # | `~(?<=#)\d+~` | `$text = "Order #471"; preg_match('~(?<=#)\\d+~', $text, $m); echo $m[0] ?? 'Not found';` | `471` |
| 77. Negative lookbehind (?&lt;!...) - find a number without # | `~(?<!#)\b\d+\b~` | `$text = "Order 471"; preg_match('~(?<!#)\\b\\d+\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `471` |
| 78. Atomic group (?&gt;...) - choose a route prefix without retrying | `~(?>/api/)\w+~` | `$text = "/api/users"; preg_match('~(?>/api/)\\w+~', $text, $m); echo $m[0] ?? 'Not found';` | `/api/users` |
| 79. Inline case flag (?i:...) - ignore case in one prefix | `~(?i:warn):\s*\w+~` | `$text = "WARN: Disk"; preg_match('~(?i:warn):\\s*\\w+~', $text, $m); echo $m[0] ?? 'Not found';` | `WARN: Disk` |
| 80. Pattern comment (?#...) - annotate a numeric ID check | `~^(?#digits only)\d{4}$~` | `$text = "5821"; echo preg_match('~^(?#digits only)\\d{4}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 81. Extended mode x - allow whitespace/comments in a pattern | `~ \d{2} \s+ [A-Z]{2} ~x` | `$text = "25 AB"; preg_match('~ \\d{2} \\s+ [A-Z]{2} ~x', $text, $m); echo $m[0] ?? 'Not found';` | `25 AB` |
| 82. Case-insensitive i - find ERROR regardless of case | `~error~i` | `$text = "Error: timeout"; preg_match('~error~i', $text, $m); echo $m[0] ?? 'Not found';` | `Error` |
| 83. Dotall s - let dot cross a line break | `~START.*END~s` | `$text = "START\nmiddle\nEND"; preg_match('~START.*END~s', $text, $m); echo json_encode($m[0] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"START\nmiddle\nEND"` |
| 84. Unicode u - match a Greek literal as UTF-8 | `~Ω~u` | `$text = "Ωmega"; preg_match('~Ω~u', $text, $m); echo $m[0] ?? 'Not found';` | `Ω` |
| 85. Ungreedy U - make normal star consume less | `~<.+>~U` | `$text = "<a><b>"; preg_match('~<.+>~U', $text, $m); echo htmlspecialchars($m[0] ?? 'Not found', ENT_QUOTES, 'UTF-8');` | `<a>` |
| 86. Duplicate-name J - allow named groups in alternatives | `~(?<id>A\d+)\|(?<id>B\d+)~J` | `$text = "A42"; preg_match('~(?<id>A\\d+)\|(?<id>B\\d+)~J', $text, $m); echo $m[1] ?? 'Not found';` | `A42` |

# Part II - Useful symbol combinations

## B1. Combining anchors, boundaries and whole-value checks

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 87. Start + end + ranges - validate an uppercase reference | `~^[A-Z]{3}-\d{4}$~` | `$text = "ORD-4821"; echo preg_match('~^[A-Z]{3}-\\d{4}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 88. Anchors + optional suffix - validate a support-ticket key | `~^TKT-\d{6}(?:-[A-Z])?$~` | `$text = "TKT-108472-A"; echo preg_match('~^TKT-\\d{6}(?:-[A-Z])?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 89. Anchors + alternation - accept known message priorities | `~^(?:low\|normal\|high\|urgent)$~i` | `$text = "URGENT"; echo preg_match('~^(?:low\|normal\|high\|urgent)$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 90. Anchors + lookahead - reject a username reserved for admins | `~^(?!admin$)[a-z][a-z0-9_]{2,15}$~i` | `$text = "admin"; echo preg_match('~^(?!admin$)[a-z][a-z0-9_]{2,15}$~i', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 91. Anchors + quantifier - enforce a 1–80 character title | `~^.{1,80}$~us` | `$text = "Weekly delivery summary"; echo preg_match('~^.{1,80}$~us', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 92. Anchors + negative class - reject newline in one-line input | `~^[^\r\n]{1,100}$~` | `$text = "Two\nlines"; echo preg_match('~^[^\\r\\n]{1,100}$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 93. Absolute start + literal - recognize an export signature | `~\AEXPORT:~` | `$text = "EXPORT: customers"; preg_match('~\\AEXPORT:~', $text, $m); echo $m[0] ?? 'Not found';` | `EXPORT:` |
| 94. Absolute end + literal - require a release name to end in .zip | `~\.zip\z~` | `$text = "release_2026.zip"; preg_match('~\\.zip\\z~', $text, $m); echo $m[0] ?? 'Not found';` | `.zip` |
| 95. Word boundary + alternative - find a full-word alert | `~\b(?:ERROR\|WARN\|FATAL)\b~` | `$text = "Level WARN now"; preg_match('~\\b(?:ERROR\|WARN\|FATAL)\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `WARN` |
| 96. Non-boundary + letters - find an internal plural marker | `~\Bs\b~` | `$text = "folders"; preg_match('~\\Bs\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `s` |
| 97. Multiline anchor + capture - extract a TODO description | `~^TODO:\s*(.+)$~m` | `$text = "DONE: sent\nTODO: call Maria\nNEXT"; preg_match('~^TODO:\\s*(.+)$~m', $text, $m); echo $m[1] ?? 'Not found';` | `call Maria` |
| 98. Multiline end anchor + capture - find a log-line timeout | `~timeout$~m` | `$text = "start\nrequest timeout\nfinish"; preg_match('~timeout$~m', $text, $m); echo $m[0] ?? 'Not found';` | `timeout` |
| 99. Full string + positive class - accept a project tag | `~^[a-z][a-z0-9-]{2,30}$~` | `$text = "summer-campaign"; echo preg_match('~^[a-z][a-z0-9-]{2,30}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 100. Full string + negative lookahead - reject a leading zero | `~^(?!0)[1-9]\d*$~` | `$text = "080"; echo preg_match('~^(?!0)[1-9]\\d*$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 101. Whole string + Unicode letters - validate a short name | `~^[\p{L}][\p{L}\p{M} '-]{1,50}$~u` | `$text = "Zoë Martin"; echo preg_match('~^[\\p{L}][\\p{L}\\p{M} \'-]{1,50}$~u', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 102. Multiline anchors + selection - list second-level headings | `~^##\s+.+$~m` | `$text = "# Index\n## Intro\n## Setup"; preg_match_all('~^##\\s+.+$~m', $text, $m); echo implode(', ', $m[0]);` | `## Intro, ## Setup` |
| 103. Absolute end + trailing whitespace check | `~\A[A-Z]{4}\z~` | `$text = "ABCD\n"; echo preg_match('~\\A[A-Z]{4}\\z~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 104. Anchors + number range - match a 0–59 minute field | `~^(?:[0-5]\d)$~` | `$text = "45"; echo preg_match('~^(?:[0-5]\\d)$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 105. Start + optional prefix - accept a simple invoice label | `~^(?:INV-)?\d{5}$~` | `$text = "INV-41028"; echo preg_match('~^(?:INV-)?\\d{5}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 106. Word boundary + Unicode setting - find a standalone café | `~(*UCP)\bcafé\b~u` | `$text = "A café nearby"; preg_match('~(*UCP)\\bcafé\\b~u', $text, $m); echo $m[0] ?? 'Not found';` | `café` |

## B2. Combining character classes and escaped characters

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 107. Digits + dash + quantities - capture a department code | `~\bDEP-(\d{3})\b~` | `$text = "Department DEP-094"; preg_match('~\\bDEP-(\\d{3})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `094` |
| 108. Non-digits + digit class - locate a reference among text | `~\b[A-Z]{2}\d{5}\b~` | `$text = "Ref AB04719 approved"; preg_match('~\\b[A-Z]{2}\\d{5}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `AB04719` |
| 109. Unicode letters + apostrophe - validate a display surname | `~^[\p{L}]+(?:['’][\p{L}]+)*$~u` | `$text = "O’Neill"; echo preg_match('~^[\\p{L}]+(?:[\'’][\\p{L}]+)*$~u', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 110. Not-space class + bounded repetition - find a short token | `~(?<=Token )[^\s]{4,12}~` | `$text = "Token abc_42"; preg_match('~(?<=Token )[^\\s]{4,12}~', $text, $m); echo $m[0] ?? 'Not found';` | `abc_42` |
| 111. Explicit allowed characters + anchors - validate a URL slug | `~^[a-z0-9]+(?:-[a-z0-9]+)*$~` | `$text = "our-new-store"; echo preg_match('~^[a-z0-9]+(?:-[a-z0-9]+)*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 112. Negated bracket class + capture - read a CSV first field | `~^([^,]+),~` | `$text = "Ada,Manager,London"; preg_match('~^([^,]+),~', $text, $m); echo $m[1] ?? 'Not found';` | `Ada` |
| 113. Negated slash class + capture - extract URL route segment | `~^/news/([^/]+)~` | `$text = "/news/releases/latest"; preg_match('~^/news/([^/]+)~', $text, $m); echo $m[1] ?? 'Not found';` | `releases` |
| 114. Whitespace + number - find numbered chapter headings | `~\bChapter\s+\d+\b~i` | `$text = "Chapter 1 and Chapter 12"; preg_match_all('~\\bChapter\\s+\\d+\\b~i', $text, $m); echo implode(', ', $m[0]);` | `Chapter 1, Chapter 12` |
| 115. Horizontal whitespace + capture - read a tab-aligned value | `~^Price\h+(\d+\.\d{2})$~m` | `$text = "Price\t49.90"; preg_match('~^Price\\h+(\\d+\\.\\d{2})$~m', $text, $m); echo $m[1] ?? 'Not found';` | `49.90` |
| 116. Unicode newline + split - break imported text into lines | `~\R+~` | `$text = "one\r\ntwo\nthree"; echo implode(' \| ', preg_split('~\\R+~', $text));` | `one \| two \| three` |
| 117. Literal quote + captured text - extract a quoted option | `~"([^"\r\n]+)"~` | `$text = "Theme: \"dark\""; preg_match('~"([^"\\r\\n]+)"~', $text, $m); echo $m[1] ?? 'Not found';` | `dark` |
| 118. Literal brackets + captured digits - read a list reference | `~\[(\d+)]~` | `$text = "See item [17]"; preg_match('~\\[(\\d+)]~', $text, $m); echo $m[1] ?? 'Not found';` | `17` |
| 119. Hex escape + capture - extract text after an equals sign | `~\x3D([A-Za-z0-9_-]+)~` | `$text = "mode=dark"; preg_match('~\\x3D([A-Za-z0-9_-]+)~', $text, $m); echo $m[1] ?? 'Not found';` | `dark` |
| 120. Literal dot + end anchor - require a .csv suffix | `~\.csv$~i` | `$text = "daily_report.CSV"; preg_match('~\\.csv$~i', $text, $m); echo $m[0] ?? 'Not found';` | `.CSV` |
| 121. Unicode digits + all matches - extract Eastern and Western numbers | `~\p{Nd}+~u` | `$text = "Scores १२ and 12"; preg_match_all('~\\p{Nd}+~u', $text, $m); echo implode(', ', $m[0]);` | `१२, 12` |
| 122. Unicode space + replacement - normalize nonbreaking spaces | `~[\x{00A0}\x{2007}\x{202F}]+~u` | `$text = "one two"; echo preg_replace('~[\\x{00A0}\\x{2007}\\x{202F}]+~u', ' ', $text);` | `one two` |
| 123. Named character property + quantifier - collect Greek words | `~\p{Greek}+~u` | `$text = "Αθήνα, Κρήτη"; preg_match_all('~\\p{Greek}+~u', $text, $m); echo implode(', ', $m[0]);` | `Αθήνα, Κρήτη` |
| 124. Word characters + trim - remove prefix underscores | `~^_+(?=\w)~` | `$text = "___account_id"; echo preg_replace('~^_+(?=\\w)~', '', $text);` | `account_id` |
| 125. Literal slash class + split - break an internal route | `~/+~` | `$text = "catalog/products/2026"; echo implode(' \| ', preg_split('~/+~', $text));` | `catalog \| products \| 2026` |
| 126. POSIX digit class + quantifier - find a tracking number | `~[[:digit:]]{8}~` | `$text = "Tracking 40918273"; preg_match('~[[:digit:]]{8}~', $text, $m); echo $m[0] ?? 'Not found';` | `40918273` |

## B3. Combining quantifiers, optional parts and greediness

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 127. Optional country prefix + phone digits - validate a compact number | `~^\+?\d{10,15}$~` | `$text = "+447911123456"; echo preg_match('~^\\+?\\d{10,15}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 128. Repeated group + literal hyphen - validate grouped serials | `~^(?:[A-Z0-9]{4}-){2}[A-Z0-9]{4}$~` | `$text = "AB12-CD34-EF56"; echo preg_match('~^(?:[A-Z0-9]{4}-){2}[A-Z0-9]{4}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 129. Lazy repetition + delimiters - extract the first quoted phrase | `~"(.*?)"~` | `$text = "He said \"ready\", then \"go\""; preg_match('~"(.*?)"~', $text, $m); echo $m[1] ?? 'Not found';` | `ready` |
| 130. Greedy repetition + delimiters - capture through the last quote | `~"(.*)"~` | `$text = "A \"one\" and \"two\""; preg_match('~"(.*)"~', $text, $m); echo $m[1] ?? 'Not found';` | `one" and "two` |
| 131. Optional decimal part + quantity - extract a weight | `~\b(\d+(?:\.\d+)?)\s*kg\b~i` | `$text = "Box 2.75 kg"; preg_match('~\\b(\\d+(?:\\.\\d+)?)\\s*kg\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `2.75` |
| 132. At least one delimiter + replacement - normalize repeated commas | `~,{2,}~` | `$text = "a,,,b,,c"; echo preg_replace('~,{2,}~', ',', $text);` | `a,b,c` |
| 133. Bounded digits + anchors - accept a two-decimal amount | `~^\d+(?:\.\d{1,2})?$~` | `$text = "89.9"; echo preg_match('~^\\d+(?:\\.\\d{1,2})?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 134. Lazy star + static tag markers - get first known tag label | `~<label>(.*?)</label>~s` | `$text = "<label>Open</label><label>Done</label>"; preg_match('~<label>(.*?)</label>~s', $text, $m); echo $m[1] ?? 'Not found';` | `Open` |
| 135. Optional dash + case sensitivity - accept reference variants | `~^REF-?\d{6}$~i` | `$text = "ref308271"; echo preg_match('~^REF-?\\d{6}$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 136. Repeated whitespace + replacement - normalize user input | `~[ \t]{2,}~` | `$text = "Good    morning"; echo preg_replace('~[ \\t]{2,}~', ' ', $text);` | `Good morning` |
| 137. Non-greedy bounded run + capture - extract a short preview | `~\bmsg:(.{3,8}?)[\|]~` | `$text = "msg:thanks\|next"; preg_match('~\\bmsg:(.{3,8}?)[\|]~', $text, $m); echo $m[1] ?? 'Not found';` | `thanks` |
| 138. Possessive run + suffix - match a safe digit-only token | `~\b\d++(?=;)~` | `$text = "id=84712;"; preg_match('~\\b\\d++(?=;)~', $text, $m); echo $m[0] ?? 'Not found';` | `84712` |
| 139. Optional suffix + end anchor - accept singular or plural | `~^item(?:s)?$~` | `$text = "items"; echo preg_match('~^item(?:s)?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 140. Zero-or-more grouped keys - validate a dotted setting | `~^[a-z]+(?:\.[a-z]+)*$~` | `$text = "app.cache.enabled"; echo preg_match('~^[a-z]+(?:\\.[a-z]+)*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 141. Repeated group + anchor - validate a colon list of keys | `~^[A-Z]{2}(?::[A-Z]{2}){2,4}$~` | `$text = "AA:BB:CC"; echo preg_match('~^[A-Z]{2}(?::[A-Z]{2}){2,4}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 142. Lazy range + following delimiter - extract a title prefix | `~^(.{1,60}?)\s+[\|]~` | `$text = "Summary of orders \| internal"; preg_match('~^(.{1,60}?)\\s+[\|]~', $text, $m); echo $m[1] ?? 'Not found';` | `Summary of orders` |
| 143. At least three letters + word boundary - find long words | `~\b[A-Za-z]{6,}\b~` | `$text = "Office lamp and keyboard"; preg_match_all('~\\b[A-Za-z]{6,}\\b~', $text, $m); echo implode(', ', $m[0]);` | `Office, keyboard` |
| 144. Optional sign + decimals - extract signed readings | `~(?<!\w)[+-]?\d+(?:\.\d+)?~` | `$text = "Values -4.5, +6, 0.25"; preg_match_all('~(?<!\\w)[+-]?\\d+(?:\\.\\d+)?~', $text, $m); echo implode(', ', $m[0]);` | `-4.5, +6, 0.25` |
| 145. Possessive range + suffix - match version-like digits | `~\d{3,5}+(?=X)~` | `$text = "Code 1234X"; preg_match('~\\d{3,5}+(?=X)~', $text, $m); echo $m[0] ?? 'Not found';` | `1234` |
| 146. Lazy repetition + braces - extract first brace content | `~\{(.*?)\}~` | `$text = "Map {blue} {red}"; preg_match('~\\{(.*?)\\}~', $text, $m); echo $m[1] ?? 'Not found';` | `blue` |

## B4. Combining groups, captures and alternatives

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 147. Alternatives + boundaries - find an urgent severity label | `~\b(?:warn\|error\|fatal)\b~i` | `$text = "Message severity: FATAL"; preg_match('~\\b(?:warn\|error\|fatal)\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `FATAL` |
| 148. Alternatives + capture - extract image type from a filename | `~\.(png\|jpg\|webp)$~i` | `$text = "hero.webp"; preg_match('~\\.(png\|jpg\|webp)$~i', $text, $m); echo $m[1] ?? 'Not found';` | `webp` |
| 149. Nested groups + capture - get a phone country prefix | `~^\+(\d{1,3})[- ]?\d{6,12}$~` | `$text = "+44 7911123456"; preg_match('~^\\+(\\d{1,3})[- ]?\\d{6,12}$~', $text, $m); echo $m[1] ?? 'Not found';` | `44` |
| 150. Noncapturing alternatives + suffix - find a media attachment | `~\b[\w-]+\.(?:pdf\|docx\|xlsx)\b~i` | `$text = "Quote.pdf attached"; preg_match('~\\b[\\w-]+\\.(?:pdf\|docx\|xlsx)\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `Quote.pdf` |
| 151. Named capture + unit - extract a number of megabytes | `~(?<count>\d+(?:\.\d+)?)\s*MB\b~i` | `$text = "File size 11.25 MB"; preg_match('~(?<count>\\d+(?:\\.\\d+)?)\\s*MB\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `11.25` |
| 152. Alternation + line boundaries - extract a build state | `~^BUILD:\s*(PASS\|FAIL\|SKIP)$~m` | `$text = "RUN: done\nBUILD: PASS"; preg_match('~^BUILD:\\s*(PASS\|FAIL\|SKIP)$~m', $text, $m); echo $m[1] ?? 'Not found';` | `PASS` |
| 153. Branch-reset group (?\|...) - capture either prefixed ID | `~(?\|user:(\d+)\|account:(\d+))~` | `$text = "account:208"; preg_match('~(?\|user:(\\d+)\|account:(\\d+))~', $text, $m); echo $m[1] ?? 'Not found';` | `208` |
| 154. Nested alternatives - validate common image dimension units | `~^\d+(?:px\|em\|rem\|%)$~` | `$text = "25rem"; echo preg_match('~^\\d+(?:px\|em\|rem\|%)$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 155. Capture across literal separator - read item code | `~\bitem=([A-Z]{2}-\d{3})\b~` | `$text = "item=AB-209"; preg_match('~\\bitem=([A-Z]{2}-\\d{3})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `AB-209` |
| 156. Optional capture group - read the middle name when present | `~^([A-Z][a-z]+)(?:\s+([A-Z][a-z]+))?\s+[A-Z][a-z]+$~` | `$text = "Sophie Anne Parker"; preg_match('~^([A-Z][a-z]+)(?:\\s+([A-Z][a-z]+))?\\s+[A-Z][a-z]+$~', $text, $m); echo $m[2] ?? 'Not found';` | `Anne` |
| 157. Named groups + alternatives - select either API version | `~/api/(v[12])/(?:users\|orders)\b~` | `$text = "/api/v2/orders"; preg_match('~/api/(v[12])/(?:users\|orders)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `v2` |
| 158. Capture + repeated group - extract a section prefix | `~^([A-Z]{2})(?:-\d{3}){2}$~` | `$text = "AB-101-204"; preg_match('~^([A-Z]{2})(?:-\\d{3}){2}$~', $text, $m); echo $m[1] ?? 'Not found';` | `AB` |
| 159. Capture + word boundary - extract a bug ID | `~\bBUG-(\d{4,7})\b~` | `$text = "See BUG-41023"; preg_match('~\\bBUG-(\\d{4,7})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `41023` |
| 160. Alternatives + case flag - find a CSV status | `~\b(?:active\|inactive\|pending)\b~i` | `$text = "Status Inactive"; preg_match('~\\b(?:active\|inactive\|pending)\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `Inactive` |
| 161. One capture for optional prefix - find a code's category | `~\b([A-Z]{3})(?:-\d{5})?\b~` | `$text = "Product TOY-18920"; preg_match('~\\b([A-Z]{3})(?:-\\d{5})?\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `TOY` |
| 162. Repeated noncapturing group + dot - validate a hostname | `~^(?:[a-z0-9-]+\.)+[a-z]{2,}$~i` | `$text = "docs.example.net"; echo preg_match('~^(?:[a-z0-9-]+\\.)+[a-z]{2,}$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 163. Capture + escaped plus - extract an international dialing prefix | `~\+(\d{1,3})[- ]\d{7,12}\b~` | `$text = "Call +49 17612345678"; preg_match('~\\+(\\d{1,3})[- ]\\d{7,12}\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `49` |
| 164. Backreference + quotes - get a quoted string with matching ends | `~(['\"])(.*?)\1~` | `$text = "Message 'hello'"; preg_match('~([\'\\"])(.*?)\\1~', $text, $m); echo $m[2] ?? 'Not found';` | `hello` |
| 165. Nested capture + simple version - extract minor release | `~\bv(\d+)\.(\d+)\.\d+\b~` | `$text = "Release v2.17.3"; preg_match('~\\bv(\\d+)\\.(\\d+)\\.\\d+\\b~', $text, $m); echo $m[2] ?? 'Not found';` | `17` |
| 166. Capture + punctuation + digits - get a phone area code | `~\((\d{3})\)\s*\d{3}-\d{4}~` | `$text = "(212) 555-0181"; preg_match('~\\((\\d{3})\\)\\s*\\d{3}-\\d{4}~', $text, $m); echo $m[1] ?? 'Not found';` | `212` |

## B5. Combining backreferences, lookarounds and exclusions

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 167. Lookahead + units - extract a number before kg | `~\b\d+(?:\.\d+)?(?=\s*kg\b)~i` | `$text = "Weight 24.5 kg"; preg_match('~\\b\\d+(?:\\.\\d+)?(?=\\s*kg\\b)~i', $text, $m); echo $m[0] ?? 'Not found';` | `24.5` |
| 168. Lookbehind + literal prefix - extract the value after ref= | `~(?<=ref=)[A-Z0-9]{6}~` | `$text = "ref=AB43Q9"; preg_match('~(?<=ref=)[A-Z0-9]{6}~', $text, $m); echo $m[0] ?? 'Not found';` | `AB43Q9` |
| 169. Negative lookahead + anchor - reject temporary file names | `~^(?!temp_)[a-z][a-z0-9_]*\.csv$~` | `$text = "temp_report.csv"; echo preg_match('~^(?!temp_)[a-z][a-z0-9_]*\\.csv$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 170. Negative lookbehind + boundary - ignore #prefixed numbers | `~(?<!#)\b\d{4}\b~` | `$text = "Order 4081 not #1298"; preg_match('~(?<!#)\\b\\d{4}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `4081` |
| 171. Lookahead + boundary - find a word followed by colon | `~\b[A-Za-z_]+(?=:)~` | `$text = "status:approved"; preg_match('~\\b[A-Za-z_]+(?=:)~', $text, $m); echo $m[0] ?? 'Not found';` | `status` |
| 172. Lookbehind + boundary - find a word after a colon | `~(?<=:)[A-Za-z_]+\b~` | `$text = "status:approved"; preg_match('~(?<=:)[A-Za-z_]+\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `approved` |
| 173. Positive and negative lookahead - require ID not followed by .bak | `~\b[A-Z]{3}\d{3}(?!\.bak)\b~` | `$text = "File ABC219.csv"; preg_match('~\\b[A-Z]{3}\\d{3}(?!\\.bak)\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `ABC219` |
| 174. Negative lookahead + word - find a reset that is not expired | `~\breset-(?!expired)\w+\b~` | `$text = "reset-pending"; preg_match('~\\breset-(?!expired)\\w+\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `reset-pending` |
| 175. Lookahead + capture - find the amount before USD | `~\b(\d+\.\d{2})(?=\s+USD\b)~` | `$text = "Total 49.90 USD"; preg_match('~\\b(\\d+\\.\\d{2})(?=\\s+USD\\b)~', $text, $m); echo $m[1] ?? 'Not found';` | `49.90` |
| 176. Lookbehind + 4 digits - read the PIN after pin: | `~(?<=pin:)\d{4}\b~` | `$text = "pin:4712"; preg_match('~(?<=pin:)\\d{4}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `4712` |
| 177. Lookahead + category - find a filename before .pdf | `~\b[\w-]+(?=\.pdf\b)~i` | `$text = "annual-report.pdf"; preg_match('~\\b[\\w-]+(?=\\.pdf\\b)~i', $text, $m); echo $m[0] ?? 'Not found';` | `annual-report` |
| 178. Negative lookahead + grouping - reject reserved slugs | `~^(?!(?:admin\|login\|register)$)[a-z][a-z0-9-]*$~` | `$text = "login"; echo preg_match('~^(?!(?:admin\|login\|register)$)[a-z][a-z0-9-]*$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 179. Lookahead + three conditions - validate token composition | `~^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)[A-Za-z\d]{10,}$~` | `$text = "ReadyToGo27"; echo preg_match('~^(?=.*[A-Z])(?=.*[a-z])(?=.*\\d)[A-Za-z\\d]{10,}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 180. Lookbehind + dollar sign - capture a plain price amount | `~(?<=\$)\d+(?:\.\d{2})?~` | `$text = "Only \$79.00"; preg_match('~(?<=\\$)\\d+(?:\\.\\d{2})?~', $text, $m); echo $m[0] ?? 'Not found';` | `79.00` |
| 181. Negative lookbehind + dot - find standalone extension markers | `~(?<!\.)\bjson\b~` | `$text = "format json"; preg_match('~(?<!\\.)\\bjson\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `json` |
| 182. Negative lookahead + question - find search without ? | `~\bsearch(?!\?)\b~` | `$text = "Quick search results"; preg_match('~\\bsearch(?!\\?)\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `search` |
| 183. Lookahead + comma - get the first field without comma | `~^[^,]+(?=,)~` | `$text = "blue,large,ready"; preg_match('~^[^,]+(?=,)~', $text, $m); echo $m[0] ?? 'Not found';` | `blue` |
| 184. Lookahead + units - recognize digits before ms | `~\d+(?=ms\b)~` | `$text = "Latency 75ms"; preg_match('~\\d+(?=ms\\b)~', $text, $m); echo $m[0] ?? 'Not found';` | `75` |
| 185. Lookbehind + hash - find a hex color value without hash | `~(?<=#)[A-Fa-f0-9]{6}\b~` | `$text = "Theme #3366CC"; preg_match('~(?<=#)[A-Fa-f0-9]{6}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `3366CC` |
| 186. Lookahead + boundary - find a number only before a hyphen | `~\b\d+(?=-[A-Z])~` | `$text = "Order 418-Q"; preg_match('~\\b\\d+(?=-[A-Z])~', $text, $m); echo $m[0] ?? 'Not found';` | `418` |

## B6. Combining modifiers, Unicode and multiline text

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 187. Case-insensitive i + boundary - find TODO anywhere | `~\btodo\b~i` | `$text = "Finish the Todo"; preg_match('~\\btodo\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `Todo` |
| 188. Multiline m + capture - read an environment variable value | `~^APP_ENV=([a-z]+)$~m` | `$text = "APP_ENV=staging\nDEBUG=true"; preg_match('~^APP_ENV=([a-z]+)$~m', $text, $m); echo $m[1] ?? 'Not found';` | `staging` |
| 189. Dotall s + lazy capture - read a simple known block | `~BEGIN(.*?)END~s` | `$text = "BEGIN\nline one\nEND"; preg_match('~BEGIN(.*?)END~s', $text, $m); echo json_encode($m[1] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\nline one\n"` |
| 190. Extended x + named capture - extract an ID with comments | `~ (?<id> [A-Z]{2} - \d{4} ) (?#code) ~x` | `$text = "AB-4927"; preg_match('~ (?<id> [A-Z]{2} - \\d{4} ) (?#code) ~x', $text, $m); echo $m[1] ?? 'Not found';` | `AB-4927` |
| 191. Unicode u + letters - find accented names | `~[\p{L}]{2,}~u` | `$text = "Zoë Jóse"; preg_match_all('~[\\p{L}]{2,}~u', $text, $m); echo implode(', ', $m[0]);` | `Zoë, Jóse` |
| 192. Unicode u + script - extract Cyrillic text | `~\p{Cyrillic}+~u` | `$text = "Hello Мир"; preg_match('~\\p{Cyrillic}+~u', $text, $m); echo $m[0] ?? 'Not found';` | `Мир` |
| 193. Unicode + UCP word boundaries - find standalone résumé | `~(*UCP)\brésumé\b~u` | `$text = "Send a résumé today"; preg_match('~(*UCP)\\brésumé\\b~u', $text, $m); echo $m[0] ?? 'Not found';` | `résumé` |
| 194. Unicode + grapheme repetition - match two combined characters | `~\X{2}~u` | `$text = "éa"; preg_match('~\\X{2}~u', $text, $m); echo $m[0] ?? 'Not found';` | `éa` |
| 195. Ungreedy U + group - capture the first quoted value | `~"(.+)"~U` | `$text = "Fields \"one\" and \"two\""; preg_match('~"(.+)"~U', $text, $m); echo $m[1] ?? 'Not found';` | `one` |
| 196. Multiline m + all matches - gather error labels per line | `~^ERROR:\s*[^\r\n]+$~m` | `$text = "INFO: ok\nERROR: disk\nERROR: network"; preg_match_all('~^ERROR:\\s*[^\\r\\n]+$~m', $text, $m); echo implode(', ', $m[0]);` | `ERROR: disk, ERROR: network` |
| 197. Case-insensitive + alternatives - recognize file types | `~\b(?:PNG\|JPG\|WEBP)\b~i` | `$text = "png, Jpg, webp"; preg_match_all('~\\b(?:PNG\|JPG\|WEBP)\\b~i', $text, $m); echo implode(', ', $m[0]);` | `png, Jpg, webp` |
| 198. Dotall + bounded capture - read a short multiline message | `~\A(.{1,80}?)\n--END--~s` | `$text = "Hello\nagain\n--END--"; preg_match('~\\A(.{1,80}?)\\n--END--~s', $text, $m); echo json_encode($m[1] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"Hello\nagain"` |
| 199. Extended x + whitespace class - match aligned report columns | `~ \d{4} \h+ [A-Z]{2} \h+ \d+ ~x` | `$text = "2026 AB 19"; preg_match('~ \\d{4} \\h+ [A-Z]{2} \\h+ \\d+ ~x', $text, $m); echo $m[0] ?? 'Not found';` | `2026 AB 19` |
| 200. Unicode + script property - read Arabic numbers | `~[\x{0660}-\x{0669}]+~u` | `$text = "Page ١٢ and ٣٤"; preg_match_all('~[\\x{0660}-\\x{0669}]+~u', $text, $m); echo implode(', ', $m[0]);` | `١٢, ٣٤` |
| 201. Multiline start + replace - remove comment lines | `~^#.*(?:\R\|$)~m` | `$text = "# header\nvalue=1"; echo preg_replace('~^#.*(?:\\R\|$)~m', '', $text);` | `value=1` |
| 202. Multiline end + trim - remove trailing spaces on lines | `~[ \t]+$~m` | `$text = "A  \nB "; echo json_encode(preg_replace('~[ \\t]+$~m', '', $text), JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"A\nB"` |
| 203. Unicode + combining marks - normalize a decomposed name | `~\p{M}+~u` | `$text = "Café"; echo preg_replace('~\\p{M}+~u', '', $text);` | `Cafe` |
| 204. Case flag inside group + case-sensitive suffix | `~(?i:error):[A-Z]+~` | `$text = "Error:DB"; preg_match('~(?i:error):[A-Z]+~', $text, $m); echo $m[0] ?? 'Not found';` | `Error:DB` |
| 205. Unicode script + anchors - validate a Greek-only label | `~^\p{Greek}{2,20}$~u` | `$text = "Αθήνα"; echo preg_match('~^\\p{Greek}{2,20}$~u', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 206. Dotall + lookahead - stop before the first END marker | `~BEGIN(.*?)(?=END)~s` | `$text = "BEGIN\nnotes\nEND next"; preg_match('~BEGIN(.*?)(?=END)~s', $text, $m); echo json_encode($m[1] ?? 'Not found', JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"\nnotes\n"` |

## B7. Combining patterns with preg_replace and preg_split

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 207. Whitespace + repetition - collapse spaces in a shipping address | `~ {2,}~` | `$text = "12   Park  Lane"; echo preg_replace('~ {2,}~', ' ', $text);` | `12 Park Lane` |
| 208. Lookbehind + comma - remove separators in amounts | `~(?<=\d),(?=\d{3}(?:\D\|$))~` | `$text = "1,250,000"; echo preg_replace('~(?<=\\d),(?=\\d{3}(?:\\D\|$))~', '', $text);` | `1250000` |
| 209. Capture + replacement backreference - swap date separators | `~^(\d{2})/(\d{2})/(\d{4})$~` | `$text = "25/12/2026"; echo preg_replace('~^(\\d{2})/(\\d{2})/(\\d{4})$~', '$3-$2-$1', $text);` | `2026-12-25` |
| 210. Capture + replacement backreference - remove duplicate words | `~\b([A-Za-z]+)\s+\1\b~i` | `$text = "very very helpful"; echo preg_replace('~\\b([A-Za-z]+)\\s+\\1\\b~i', '$1', $text);` | `very helpful` |
| 211. Prefix + anchor - remove a Markdown list number | `~^\d+\.\s+~` | `$text = "3. Install PHP"; echo preg_replace('~^\\d+\\.\\s+~', '', $text);` | `Install PHP` |
| 212. Group + repeated punctuation - keep one exclamation mark | `~!{2,}~` | `$text = "Great!!!!"; echo preg_replace('~!{2,}~', '!', $text);` | `Great!` |
| 213. Alternation + replace - strip known log-level markers | `~^\[(?:INFO\|WARN\|ERROR)]\s*~` | `$text = "[WARN] Low disk"; echo preg_replace('~^\\[(?:INFO\|WARN\|ERROR)]\\s*~', '', $text);` | `Low disk` |
| 214. Lookahead + replacement - remove trailing revision suffix | `~\s+\(copy\s+\d+\)(?=\.[^.]+$)~i` | `$text = "Plan (copy 3).pdf"; echo preg_replace('~\\s+\\(copy\\s+\\d+\\)(?=\\.[^.]+$)~i', '', $text);` | `Plan.pdf` |
| 215. Character set + replace - remove phone formatting | `~[()\s.-]+~` | `$text = "+1 (212) 555-0100"; echo preg_replace('~[()\\s.-]+~', '', $text);` | `+12125550100` |
| 216. Unicode class + replace - remove zero-width spaces | `~\x{200B}+~u` | `$text = "data​​base"; echo preg_replace('~\\x{200B}+~u', '', $text);` | `database` |
| 217. Anchored group + replace - remove email Re: chains | `~^(?:Re:\s*)+~i` | `$text = "Re: Re: Status"; echo preg_replace('~^(?:Re:\\s*)+~i', '', $text);` | `Status` |
| 218. Repeated dashes + replace - clean a product URL slug | `~-{2,}~` | `$text = "red---running--shoes"; echo preg_replace('~-{2,}~', '-', $text);` | `red-running-shoes` |
| 219. Split + repeated whitespace - break a tag list | `~\s*,\s*~` | `$text = "fast, reliable,compact"; echo implode(' \| ', preg_split('~\\s*,\\s*~', $text));` | `fast \| reliable \| compact` |
| 220. Split + alternatives - accept semicolons or commas | `~\s*[,;]\s*~` | `$text = "red; green, blue"; echo implode(' \| ', preg_split('~\\s*[,;]\\s*~', $text));` | `red \| green \| blue` |
| 221. Split + repeated vertical whitespace - separate paragraphs | `~\R{2,}~` | `$text = "Intro\n\nBody\n\nEnd"; echo implode(' \| ', preg_split('~\\R{2,}~', $text));` | `Intro \| Body \| End` |
| 222. Split + escaped dot - divide a version into components | `~\.~` | `$text = "2.14.6"; echo implode(' \| ', preg_split('~\\.~', $text));` | `2 \| 14 \| 6` |
| 223. Split + pipe character class - extract report columns | `~\s*[\|]\s*~` | `$text = "one \| two \| three"; echo implode(' \| ', preg_split('~\\s*[\|]\\s*~', $text));` | `one \| two \| three` |
| 224. Capture + replacement - normalize name:value fields | `~^([A-Za-z_]+)\s*:\s*(.+)$~` | `$text = "Status : Active"; echo preg_replace('~^([A-Za-z_]+)\\s*:\\s*(.+)$~', '$1: $2', $text);` | `Status: Active` |
| 225. Lookahead + replace - hide digits except last four | `~\d(?=\d{4})~` | `$text = "1234567890"; echo preg_replace('~\\d(?=\\d{4})~', '*', $text);` | `******7890` |
| 226. Word boundary + alternation - replace temporary states | `~\b(?:WAITING\|QUEUED)\b~` | `$text = "Job QUEUED now"; echo preg_replace('~\\b(?:WAITING\|QUEUED)\\b~', 'PENDING', $text);` | `Job PENDING now` |

## B8. Combining advanced PCRE2 constructs

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 227. Recursive group (?R) - match a nested parenthesized note | `~\((?:[^()]++\|(?R))*\)~` | `$text = "Note (a(b(c)d)e)"; preg_match('~\\((?:[^()]++\|(?R))*\\)~', $text, $m); echo $m[0] ?? 'Not found';` | `(a(b(c)d)e)` |
| 228. Recursive group (?R) - match nested curly braces | `~\{(?:[^{}]++\|(?R))*}~` | `$text = "Payload {a{b{c}d}e}"; preg_match('~\\{(?:[^{}]++\|(?R))*}~', $text, $m); echo $m[0] ?? 'Not found';` | `{a{b{c}d}e}` |
| 229. Named recursion (?&par) - match balanced parentheses | `~(?<par>\((?:[^()]++\|(?&par))*\))~` | `$text = "Data ((inner)(more))"; preg_match('~(?<par>\\((?:[^()]++\|(?&par))*\\))~', $text, $m); echo $m[0] ?? 'Not found';` | `((inner)(more))` |
| 230. Branch reset (?\|...) - capture an ID under either key | `~(?\|id=(\d+)\|user=(\d+))~` | `$text = "user=9102"; preg_match('~(?\|id=(\\d+)\|user=(\\d+))~', $text, $m); echo $m[1] ?? 'Not found';` | `9102` |
| 231. Conditional (?(name)yes\|no) - validate prefixed ID lengths | `~^(?<prefix>INV-)?(?(prefix)\d{6}\|\d{4})$~` | `$text = "INV-003819"; echo preg_match('~^(?<prefix>INV-)?(?(prefix)\\d{6}\|\\d{4})$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 232. Atomic group (?&gt;...) - read a nonbacktracking prefix | `~(?>GET\|POST)\s+/[a-z]+~` | `$text = "POST /users"; preg_match('~(?>GET\|POST)\\s+/[a-z]+~', $text, $m); echo $m[0] ?? 'Not found';` | `POST /users` |
| 233. Possessive ++ - read numbers without retrying shorter runs | `~\b\d++(?=\s*ms)~` | `$text = "Wait 150 ms"; preg_match('~\\b\\d++(?=\\s*ms)~', $text, $m); echo $m[0] ?? 'Not found';` | `150` |
| 234. SKIP/FAIL - ignore quoted TODO while scanning comments | `~"[^"]*"(*SKIP)(*F)\|\bTODO\b~` | `$text = "\"TODO\" // TODO fix"; preg_match('~"[^"]*"(*SKIP)(*F)\|\\bTODO\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `TODO` |
| 235. Reset start \\K - report only digits after invoice prefix | `~INV-\K\d{6}~` | `$text = "INV-302918"; preg_match('~INV-\\K\\d{6}~', $text, $m); echo $m[0] ?? 'Not found';` | `302918` |
| 236. Quoted literal \\Q...\\E - search punctuation verbatim | `~\Qfile.name[1]\E~` | `$text = "Found file.name[1]"; preg_match('~\\Qfile.name[1]\\E~', $text, $m); echo $m[0] ?? 'Not found';` | `file.name[1]` |
| 237. DEFINE subpattern + call - match two two-digit fields | `~(?(DEFINE)(?<num>\d{2}))(?&num)-(?&num)~` | `$text = "Code 12-34"; preg_match('~(?(DEFINE)(?<num>\\d{2}))(?&num)-(?&num)~', $text, $m); echo $m[0] ?? 'Not found';` | `12-34` |
| 238. Branch-reset capture - read either old or new config key | `~(?\|old_key:([A-Z]+)\|new_key:([A-Z]+))~` | `$text = "new_key:READY"; preg_match('~(?\|old_key:([A-Z]+)\|new_key:([A-Z]+))~', $text, $m); echo $m[1] ?? 'Not found';` | `READY` |
| 239. Named backreference - find a repeated event name | `~\b(?<name>[a-z]+)\s+\k<name>\b~i` | `$text = "start start finished"; preg_match('~\\b(?<name>[a-z]+)\\s+\\k<name>\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `start start` |
| 240. Recursive brackets - find nested list expressions | `~\[(?:[^\[\]]++\|(?R))*]~` | `$text = "Nested [a[b[c]d]e]"; preg_match('~\\[(?:[^\\[\\]]++\|(?R))*]~', $text, $m); echo $m[0] ?? 'Not found';` | `[a[b[c]d]e]` |
| 241. Unicode grapheme \\X - extract one family emoji cluster | `~\X~u` | `$text = "👨‍👩‍👧‍👦"; preg_match('~\\X~u', $text, $m); echo $m[0] ?? 'Not found';` | `👨‍👩‍👧‍👦` |
| 242. Unicode property + UCP - find a complete Greek word | `~(*UCP)\b\p{Greek}+\b~u` | `$text = "Visit Αθήνα"; preg_match('~(*UCP)\\b\\p{Greek}+\\b~u', $text, $m); echo $m[0] ?? 'Not found';` | `Αθήνα` |
| 243. Conditional quote - allow optional matching double quotes | `~^(?<q>")?value(?(q)")$~` | `$text = "\"value\""; echo preg_match('~^(?<q>")?value(?(q)")$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 244. Possessive range + suffix - identify bounded run before marker | `~\d{3,5}+(?=X)~` | `$text = "Flag 9843X"; preg_match('~\\d{3,5}+(?=X)~', $text, $m); echo $m[0] ?? 'Not found';` | `9843` |
| 245. Repeated alternative with backreference - require same separator | `~^[A-F0-9]{2}([:-])(?:[A-F0-9]{2}\1){4}[A-F0-9]{2}$~i` | `$text = "AA:BB:CC:DD:EE:FF"; echo preg_match('~^[A-F0-9]{2}([:-])(?:[A-F0-9]{2}\\1){4}[A-F0-9]{2}$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 246. Quoted CSV field + doubled-quote syntax - identify a single field | `~"(?:[^"]\|"")*"~` | `$text = "\"He said \"\"hello\"\"\""; preg_match('~"(?:[^"]\|"")*"~', $text, $m); echo $m[0] ?? 'Not found';` | `"He said ""hello"""` |

# Part III - Practical web-development examples

## 1. Account registration and permissions

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 247. Accept a 3–20 character username | `~^[A-Za-z][A-Za-z0-9_]{2,19}$~` | `$text = "sophie_21"; echo preg_match('~^[A-Za-z][A-Za-z0-9_]{2,19}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 248. Reject a username starting with a number | `~^[A-Za-z][A-Za-z0-9_]{2,19}$~` | `$text = "9sophie"; echo preg_match('~^[A-Za-z][A-Za-z0-9_]{2,19}$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 249. Allow usernames with periods between words | `~^[a-z][a-z0-9]*(?:\.[a-z0-9]+)*$~` | `$text = "first.last"; echo preg_match('~^[a-z][a-z0-9]*(?:\\.[a-z0-9]+)*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 250. Disallow repeated underscores in a username | `~^(?!.*__)[a-z][a-z0-9_]{3,15}$~` | `$text = "mary__jane"; echo preg_match('~^(?!.*__)[a-z][a-z0-9_]{3,15}$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 251. Require at least one letter in an account handle | `~^(?=.*[a-z])[a-z0-9_-]{4,20}$~` | `$text = "backup7"; echo preg_match('~^(?=.*[a-z])[a-z0-9_-]{4,20}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 252. Extract the numeric user ID from an account URL | `~/users/([1-9]\d*)(?:/\|$)~` | `$text = "/users/284/profile"; preg_match('~/users/([1-9]\\d*)(?:/\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `284` |
| 253. Extract the account role from a role label | `~\brole:(admin\|editor\|viewer)\b~i` | `$text = "role:editor"; preg_match('~\\brole:(admin\|editor\|viewer)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `editor` |
| 254. Check a password has at least eight characters and a digit | `~^(?=.*\d).{8,}$~s` | `$text = "welcome2026"; echo preg_match('~^(?=.*\\d).{8,}$~s', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 255. Reject a password without an uppercase letter | `~^(?=.*[A-Z])(?=.*[a-z])(?=.*\d).{10,}$~s` | `$text = "alllowercase123"; echo preg_match('~^(?=.*[A-Z])(?=.*[a-z])(?=.*\\d).{10,}$~s', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 256. Require upper/lowercase, digit, and a symbol | `~^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9]).{10,}$~s` | `$text = "StrongPass8!"; echo preg_match('~^(?=.*[A-Z])(?=.*[a-z])(?=.*\\d)(?=.*[^A-Za-z0-9]).{10,}$~s', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 257. Validate a six-digit temporary sign-in code | `~^\d{6}$~D` | `$text = "406912"; echo preg_match('~^\\d{6}$~D', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 258. Reject a sign-in code with spaces | `~^\d{6}$~D` | `$text = "406 912"; echo preg_match('~^\\d{6}$~D', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 259. Find a user tag such as @alice in a comment | `~(?<!\w)@[A-Za-z][A-Za-z0-9_]{1,19}\b~` | `$text = "Please ask @alice_7"; preg_match('~(?<!\\w)@[A-Za-z][A-Za-z0-9_]{1,19}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `@alice_7` |
| 260. List all mentioned users in a comment | `~(?<!\w)@[A-Za-z][A-Za-z0-9_]*\b~` | `$text = "@lena and @mark can review"; preg_match_all('~(?<!\\w)@[A-Za-z][A-Za-z0-9_]*\\b~', $text, $m); echo implode(', ', $m[0]);` | `@lena, @mark` |
| 261. Extract an account number from a support message | `~\baccount\s*#\s*(\d{5,10})\b~i` | `$text = "Account # 908172"; preg_match('~\\baccount\\s*#\\s*(\\d{5,10})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `908172` |
| 262. Validate a UUID-shaped user identifier | `~^[0-9a-f]{8}(?:-[0-9a-f]{4}){3}-[0-9a-f]{12}$~i` | `$text = "550e8400-e29b-41d4-a716-446655440000"; echo preg_match('~^[0-9a-f]{8}(?:-[0-9a-f]{4}){3}-[0-9a-f]{12}$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 263. Find a permission slug in a log entry | `~\bpermission=([a-z]+(?:\.[a-z]+)+)\b~` | `$text = "permission=posts.publish"; preg_match('~\\bpermission=([a-z]+(?:\\.[a-z]+)+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `posts.publish` |
| 264. Extract a tenant ID from a prefixed account key | `~\btenant_([A-Z0-9]{6})\b~` | `$text = "tenant_AB392X"; preg_match('~\\btenant_([A-Z0-9]{6})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `AB392X` |
| 265. Validate a lowercase API client identifier | `~^app_[a-z0-9]{12}$~` | `$text = "app_73c01d290ab5"; echo preg_match('~^app_[a-z0-9]{12}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 266. Extract a prefixed session reference | `~\bsess_[A-F0-9]{16}\b~` | `$text = "session=sess_1A2B3C4D5E6F7890"; preg_match('~\\bsess_[A-F0-9]{16}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `sess_1A2B3C4D5E6F7890` |
| 267. Find an enabled/disabled account state | `~\bstatus=(enabled\|disabled\|locked)\b~` | `$text = "status=locked"; preg_match('~\\bstatus=(enabled\|disabled\|locked)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `locked` |
| 268. Allow only known account locales | `~^(?:en\|fr\|de\|es\|it)(?:-[A-Z]{2})?$~` | `$text = "en-GB"; echo preg_match('~^(?:en\|fr\|de\|es\|it)(?:-[A-Z]{2})?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 269. Extract a team slug from a dashboard path | `~/teams/([a-z0-9]+(?:-[a-z0-9]+)*)/dashboard~` | `$text = "/teams/blue-harbor/dashboard"; preg_match('~/teams/([a-z0-9]+(?:-[a-z0-9]+)*)/dashboard~', $text, $m); echo $m[1] ?? 'Not found';` | `blue-harbor` |
| 270. Check a role hierarchy notation | `~^(?:owner\|manager\|member):[1-9]\d*$~` | `$text = "manager:27"; echo preg_match('~^(?:owner\|manager\|member):[1-9]\\d*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 271. Remove accidental whitespace around a login name | `~^\s+\|\s+$~` | `$text = "   maria_7   "; echo preg_replace('~^\\s+\|\\s+$~', '', $text);` | `maria_7` |

## 2. Contact details and profiles

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 272. Extract an email address from a sentence | `~[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}~` | `$text = "Write to help@example.org today"; preg_match('~[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}~', $text, $m); echo $m[0] ?? 'Not found';` | `help@example.org` |
| 273. Check a basic email address format | `~^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$~D` | `$text = "person@example.net"; echo preg_match('~^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$~D', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 274. Reject an email address containing whitespace | `~^[^\s@]+@[^\s@]+\.[A-Za-z]{2,}$~D` | `$text = "john doe@example.com"; echo preg_match('~^[^\\s@]+@[^\\s@]+\\.[A-Za-z]{2,}$~D', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 275. Extract the domain from an email address | `~@([A-Za-z0-9.-]+\.[A-Za-z]{2,})$~` | `$text = "eva@north.example.com"; preg_match('~@([A-Za-z0-9.-]+\\.[A-Za-z]{2,})$~', $text, $m); echo $m[1] ?? 'Not found';` | `north.example.com` |
| 276. Extract the local part of an email address | `~^([A-Za-z0-9._%+-]+)@~` | `$text = "team.billing@example.com"; preg_match('~^([A-Za-z0-9._%+-]+)@~', $text, $m); echo $m[1] ?? 'Not found';` | `team.billing` |
| 277. Find all email addresses in a support note | `~[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}~` | `$text = "Send to a@example.org and b@example.net"; preg_match_all('~[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}~', $text, $m); echo implode(', ', $m[0]);` | `a@example.org, b@example.net` |
| 278. Validate an international phone number in E.164 shape | `~^\+[1-9]\d{7,14}$~` | `$text = "+447911123456"; echo preg_match('~^\\+[1-9]\\d{7,14}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 279. Strip formatting from a phone number | `~[()\s-]+~` | `$text = "+1 (212) 555-0188"; echo preg_replace('~[()\\s-]+~', '', $text);` | `+12125550188` |
| 280. Find an international phone number in text | `~\+[1-9]\d{7,14}\b~` | `$text = "Call +33612345678 tomorrow"; preg_match('~\\+[1-9]\\d{7,14}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `+33612345678` |
| 281. Extract a phone extension | `~\b(?:ext\.?\|extension)\s*(\d{2,5})\b~i` | `$text = "Office ext. 341"; preg_match('~\\b(?:ext\\.?\|extension)\\s*(\\d{2,5})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `341` |
| 282. Validate a postal code with five digits | `~^\d{5}$~` | `$text = "02139"; echo preg_match('~^\\d{5}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 283. Validate a postal code with optional four-digit suffix | `~^\d{5}(?:-\d{4})?$~` | `$text = "02139-4307"; echo preg_match('~^\\d{5}(?:-\\d{4})?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 284. Extract a country code from a locale string | `~^[a-z]{2}-([A-Z]{2})$~` | `$text = "en-CA"; preg_match('~^[a-z]{2}-([A-Z]{2})$~', $text, $m); echo $m[1] ?? 'Not found';` | `CA` |
| 285. Normalize repeated spaces in a full name | `~[ \t]{2,}~` | `$text = "Anna   Marie  Reed"; echo preg_replace('~[ \\t]{2,}~', ' ', $text);` | `Anna Marie Reed` |
| 286. Reject a profile display name containing HTML brackets | `~^[^<>]{2,60}$~u` | `$text = "Daniel <Grey>"; echo preg_match('~^[^<>]{2,60}$~u', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 287. Find a hashtag in a profile biography | `~(?<!\w)#[\p{L}\p{N}_]+~u` | `$text = "Designer and #photographer"; preg_match('~(?<!\\w)#[\\p{L}\\p{N}_]+~u', $text, $m); echo $m[0] ?? 'Not found';` | `#photographer` |
| 288. List hashtags in a short biography | `~(?<!\w)#[\p{L}\p{N}_]+~u` | `$text = "I love #design, #travel, and #coffee"; preg_match_all('~(?<!\\w)#[\\p{L}\\p{N}_]+~u', $text, $m); echo implode(', ', $m[0]);` | `#design, #travel, #coffee` |
| 289. Extract a social handle from a URL path | `~/@([A-Za-z0-9_.]{2,30})(?:/\|$)~` | `$text = "https://social.example/@alexa.art"; preg_match('~/@([A-Za-z0-9_.]{2,30})(?:/\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `alexa.art` |
| 290. Validate a two-letter country code | `~^[A-Z]{2}$~` | `$text = "SE"; echo preg_match('~^[A-Z]{2}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 291. Find a birthday year in an ISO date | `~\b((?:19\|20)\d{2})-\d{2}-\d{2}\b~` | `$text = "Born: 1994-08-12"; preg_match('~\\b((?:19\|20)\\d{2})-\\d{2}-\\d{2}\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `1994` |
| 292. Extract a website domain from a profile URL | `~^https?://(?:www\.)?([^/:?#]+)~i` | `$text = "https://www.sample.org/people"; preg_match('~^https?://(?:www\\.)?([^/:?#]+)~i', $text, $m); echo $m[1] ?? 'Not found';` | `sample.org` |
| 293. Validate a simple LinkedIn-style profile slug | `~^[a-z0-9]+(?:-[a-z0-9]+)*$~` | `$text = "anna-smith-42"; echo preg_match('~^[a-z0-9]+(?:-[a-z0-9]+)*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 294. Remove a leading @ from a social handle | `~^@+~` | `$text = "@@marissa"; echo preg_replace('~^@+~', '', $text);` | `marissa` |
| 295. Extract preferred pronouns from a profile label | `~\bpronouns:\s*(she/her\|he/him\|they/them)\b~i` | `$text = "Pronouns: they/them"; preg_match('~\\bpronouns:\\s*(she/her\|he/him\|they/them)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `they/them` |
| 296. Find a numbered apartment in an address line | `~\b(?:apt\|unit\|suite)\.?\s*#?\s*(\d+[A-Za-z]?)\b~i` | `$text = "Suite 204B, Main St"; preg_match('~\\b(?:apt\|unit\|suite)\\.?\\s*#?\\s*(\\d+[A-Za-z]?)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `204B` |

## 3. Numbers, units and measurements

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 297. Extract an integer quantity from an order | `~\bqty:\s*(\d+)\b~i` | `$text = "Qty: 48 boxes"; preg_match('~\\bqty:\\s*(\\d+)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `48` |
| 298. Validate a positive whole-number quantity | `~^[1-9]\d*$~` | `$text = "24"; echo preg_match('~^[1-9]\\d*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 299. Reject a quantity with a leading zero | `~^[1-9]\d*$~` | `$text = "024"; echo preg_match('~^[1-9]\\d*$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 300. Extract a signed temperature | `~\btemp:\s*([+-]?\d+(?:\.\d+)?)~i` | `$text = "temp: -7.5 C"; preg_match('~\\btemp:\\s*([+-]?\\d+(?:\\.\\d+)?)~i', $text, $m); echo $m[1] ?? 'Not found';` | `-7.5` |
| 301. Extract a weight expressed in kilograms | `~\b(\d+(?:\.\d+)?)\s*kg\b~i` | `$text = "Package 12.75 kg"; preg_match('~\\b(\\d+(?:\\.\\d+)?)\\s*kg\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `12.75` |
| 302. Extract a length expressed in centimeters | `~\b(\d+(?:\.\d+)?)\s*cm\b~i` | `$text = "Width: 42 cm"; preg_match('~\\b(\\d+(?:\\.\\d+)?)\\s*cm\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `42` |
| 303. Find all values expressed in meters | `~\b\d+(?:\.\d+)?\s*m\b~` | `$text = "Walls: 3.5 m, 4 m and 2.2 m"; preg_match_all('~\\b\\d+(?:\\.\\d+)?\\s*m\\b~', $text, $m); echo implode(', ', $m[0]);` | `3.5 m, 4 m, 2.2 m` |
| 304. Validate a two-decimal price value | `~^\d+\.\d{2}$~` | `$text = "19.95"; echo preg_match('~^\\d+\\.\\d{2}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 305. Extract a percentage from a report | `~\b(\d+(?:\.\d+)?)%~` | `$text = "Progress 87.5%"; preg_match('~\\b(\\d+(?:\\.\\d+)?)%~', $text, $m); echo $m[1] ?? 'Not found';` | `87.5` |
| 306. Validate a percentage between 0 and 100 | `~^(?:100(?:\.0+)?\|(?:\d\|[1-9]\d)(?:\.\d+)?)$~` | `$text = "99.25"; echo preg_match('~^(?:100(?:\\.0+)?\|(?:\\d\|[1-9]\\d)(?:\\.\\d+)?)$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 307. Extract a numeric range written as 10-20 | `~\b\d+\s*-\s*\d+\b~` | `$text = "Allowed: 10-20 users"; preg_match('~\\b\\d+\\s*-\\s*\\d+\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `10-20` |
| 308. Find all signed numbers in a measurement note | `~(?<!\w)[+-]?\d+(?:\.\d+)?~` | `$text = "Offsets -2.5, +3.0, 0"; preg_match_all('~(?<!\\w)[+-]?\\d+(?:\\.\\d+)?~', $text, $m); echo implode(', ', $m[0]);` | `-2.5, +3.0, 0` |
| 309. Normalize decimal commas to decimal points | `~(?<=\d),(?=\d)~` | `$text = "Length 12,5 meters"; echo preg_replace('~(?<=\\d),(?=\\d)~', '.', $text);` | `Length 12.5 meters` |
| 310. Extract a scientific-notation value | `~[+-]?(?:\d+(?:\.\d*)?\|\.\d+)[eE][+-]?\d+~` | `$text = "Reading 1.25e-4"; preg_match('~[+-]?(?:\\d+(?:\\.\\d*)?\|\\.\\d+)[eE][+-]?\\d+~', $text, $m); echo $m[0] ?? 'Not found';` | `1.25e-4` |
| 311. Validate a signed integer input | `~^[+-]?(?:0\|[1-9]\d*)$~` | `$text = "-48"; echo preg_match('~^[+-]?(?:0\|[1-9]\\d*)$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 312. Extract a speed in km/h | `~\b(\d+(?:\.\d+)?)\s*km/h\b~i` | `$text = "Speed: 65 km/h"; preg_match('~\\b(\\d+(?:\\.\\d+)?)\\s*km/h\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `65` |
| 313. Extract a file size in megabytes | `~\b(\d+(?:\.\d+)?)\s*MB\b~i` | `$text = "Uploaded 24.6 MB"; preg_match('~\\b(\\d+(?:\\.\\d+)?)\\s*MB\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `24.6` |
| 314. Find all millisecond timings in a log line | `~\b\d+(?:\.\d+)?ms\b~` | `$text = "db 12ms, cache 4.2ms, api 103ms"; preg_match_all('~\\b\\d+(?:\\.\\d+)?ms\\b~', $text, $m); echo implode(', ', $m[0]);` | `12ms, 4.2ms, 103ms` |
| 315. Extract a 0-5 star rating | `~\brating:\s*([0-5](?:\.\d)?)\b~i` | `$text = "rating: 4.7"; preg_match('~\\brating:\\s*([0-5](?:\\.\\d)?)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `4.7` |
| 316. Validate a 1-10 numeric score | `~^(?:10\|[1-9])$~` | `$text = "8"; echo preg_match('~^(?:10\|[1-9])$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 317. Extract width and height from an image dimension | `~\b\d{2,5}\s*[x×]\s*\d{2,5}\b~i` | `$text = "Canvas: 1920x1080"; preg_match('~\\b\\d{2,5}\\s*[x×]\\s*\\d{2,5}\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `1920x1080` |
| 318. Find the first negative balance amount | `~(?<!\d)-\d+(?:\.\d{2})?\b~` | `$text = "Balance: -125.40"; preg_match('~(?<!\\d)-\\d+(?:\\.\\d{2})?\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `-125.40` |
| 319. Validate exactly four fractional decimal digits | `~^\d+\.\d{4}$~` | `$text = "0.0125"; echo preg_match('~^\\d+\\.\\d{4}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 320. Remove grouping commas from a number | `~(?<=\d),(?=\d{3}(?:\D\|$))~` | `$text = "Visitors: 12,345"; echo preg_replace('~(?<=\\d),(?=\\d{3}(?:\\D\|$))~', '', $text);` | `Visitors: 12345` |
| 321. Extract the numerator and denominator in a fraction | `~\b\d+/\d+\b~` | `$text = "Share: 3/8"; preg_match('~\\b\\d+/\\d+\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `3/8` |

## 4. Dates, times and scheduling

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 322. Validate an ISO-shaped calendar date | `~^\d{4}-(?:0[1-9]\|1[0-2])-(?:0[1-9]\|[12]\d\|3[01])$~` | `$text = "2026-11-19"; echo preg_match('~^\\d{4}-(?:0[1-9]\|1[0-2])-(?:0[1-9]\|[12]\\d\|3[01])$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 323. Extract the year from an ISO date | `~\b((?:19\|20)\d{2})-\d{2}-\d{2}\b~` | `$text = "Invoice date 2026-04-19"; preg_match('~\\b((?:19\|20)\\d{2})-\\d{2}-\\d{2}\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2026` |
| 324. Find all ISO dates in a project note | `~\b\d{4}-\d{2}-\d{2}\b~` | `$text = "Start 2026-03-01; end 2026-04-12"; preg_match_all('~\\b\\d{4}-\\d{2}-\\d{2}\\b~', $text, $m); echo implode(', ', $m[0]);` | `2026-03-01, 2026-04-12` |
| 325. Validate a 24-hour time with minutes | `~^(?:[01]\d\|2[0-3]):[0-5]\d$~` | `$text = "23:45"; echo preg_match('~^(?:[01]\\d\|2[0-3]):[0-5]\\d$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 326. Reject an invalid 24-hour clock hour | `~^(?:[01]\d\|2[0-3]):[0-5]\d$~` | `$text = "25:10"; echo preg_match('~^(?:[01]\\d\|2[0-3]):[0-5]\\d$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 327. Extract a clock time from an appointment message | `~\b(?:[01]\d\|2[0-3]):[0-5]\d\b~` | `$text = "Appointment at 14:30"; preg_match('~\\b(?:[01]\\d\|2[0-3]):[0-5]\\d\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `14:30` |
| 328. Validate a clock time including seconds | `~^(?:[01]\d\|2[0-3]):[0-5]\d:[0-5]\d$~` | `$text = "08:15:59"; echo preg_match('~^(?:[01]\\d\|2[0-3]):[0-5]\\d:[0-5]\\d$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 329. Extract a date in DD/MM/YYYY notation | `~\b(?:0[1-9]\|[12]\d\|3[01])/(?:0[1-9]\|1[0-2])/\d{4}\b~` | `$text = "Due by 05/12/2026"; preg_match('~\\b(?:0[1-9]\|[12]\\d\|3[01])/(?:0[1-9]\|1[0-2])/\\d{4}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `05/12/2026` |
| 330. Extract a YYYY/MM/DD date from a filename | `~\b\d{4}/\d{2}/\d{2}\b~` | `$text = "Report path 2026/11/10/daily"; preg_match('~\\b\\d{4}/\\d{2}/\\d{2}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `2026/11/10` |
| 331. Find a 12-hour appointment time with AM/PM | `~\b(?:1[0-2]\|0?[1-9]):[0-5]\d\s*[AP]M\b~i` | `$text = "Reminder: 9:15 AM"; preg_match('~\\b(?:1[0-2]\|0?[1-9]):[0-5]\\d\\s*[AP]M\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `9:15 AM` |
| 332. Validate a YYYY-MM calendar month | `~^\d{4}-(?:0[1-9]\|1[0-2])$~` | `$text = "2027-01"; echo preg_match('~^\\d{4}-(?:0[1-9]\|1[0-2])$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 333. Extract the quarter from a financial report | `~\b(?:FY\d{4}\s+)?(Q[1-4])\b~` | `$text = "FY2026 Q3"; preg_match('~\\b(?:FY\\d{4}\\s+)?(Q[1-4])\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `Q3` |
| 334. Find a weekday at the start of a schedule | `~^(?:Mon\|Tue\|Wed\|Thu\|Fri\|Sat\|Sun)\b~` | `$text = "Thu 10:30-12:00"; preg_match('~^(?:Mon\|Tue\|Wed\|Thu\|Fri\|Sat\|Sun)\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `Thu` |
| 335. Extract the start time of a time range | `~\b([0-2]\d:[0-5]\d)\s*[-–]\s*[0-2]\d:[0-5]\d\b~u` | `$text = "Office 09:00–17:30"; preg_match('~\\b([0-2]\\d:[0-5]\\d)\\s*[-–]\\s*[0-2]\\d:[0-5]\\d\\b~u', $text, $m); echo $m[1] ?? 'Not found';` | `09:00` |
| 336. Extract the end time of a time range | `~\b([0-2]\d:[0-5]\d)\s*[-–]\s*([0-2]\d:[0-5]\d)\b~u` | `$text = "Office 09:00–17:30"; preg_match('~\\b([0-2]\\d:[0-5]\\d)\\s*[-–]\\s*([0-2]\\d:[0-5]\\d)\\b~u', $text, $m); echo $m[2] ?? 'Not found';` | `17:30` |
| 337. Find an ISO UTC timestamp in an audit line | `~\b\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}Z\b~` | `$text = "at 2026-11-11T14:20:00Z"; preg_match('~\\b\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}Z\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `2026-11-11T14:20:00Z` |
| 338. Validate an ISO timestamp with a numeric offset | `~^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}[+-]\d{2}:\d{2}$~` | `$text = "2026-11-11T16:20:00+02:00"; echo preg_match('~^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}[+-]\\d{2}:\\d{2}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 339. Extract the number of days in a reminder | `~\bremind\s+in\s+(\d+)\s+days?\b~i` | `$text = "Remind in 3 days"; preg_match('~\\bremind\\s+in\\s+(\\d+)\\s+days?\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `3` |
| 340. Find a time-zone name in a meeting note | `~\b(?:UTC\|GMT\|CET\|EST\|PST)\b~` | `$text = "Meeting 10:00 CET"; preg_match('~\\b(?:UTC\|GMT\|CET\|EST\|PST)\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `CET` |
| 341. Extract a week number from an ISO-week label | `~\b\d{4}-W(0[1-9]\|[1-4]\d\|5[0-3])\b~` | `$text = "Schedule 2026-W47"; preg_match('~\\b\\d{4}-W(0[1-9]\|[1-4]\\d\|5[0-3])\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `47` |
| 342. Validate a compact YYYYMMDD date token | `~^\d{4}(?:0[1-9]\|1[0-2])(?:0[1-9]\|[12]\d\|3[01])$~` | `$text = "20261125"; echo preg_match('~^\\d{4}(?:0[1-9]\|1[0-2])(?:0[1-9]\|[12]\\d\|3[01])$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 343. Extract a timestamp from a timestamped image name | `~photo_(\d{8}_\d{6})\.(?:jpg\|png)$~i` | `$text = "photo_20261111_083045.jpg"; preg_match('~photo_(\\d{8}_\\d{6})\\.(?:jpg\|png)$~i', $text, $m); echo $m[1] ?? 'Not found';` | `20261111_083045` |
| 344. Find a relative duration expressed in hours | `~\b\d+(?:\.\d+)?\s+hours?\b~i` | `$text = "Job runs for 2.5 hours"; preg_match('~\\b\\d+(?:\\.\\d+)?\\s+hours?\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `2.5 hours` |
| 345. Validate a clock offset like +05:30 | `~^[+-](?:0\d\|1[0-4]):[0-5]\d$~` | `$text = "+05:30"; echo preg_match('~^[+-](?:0\\d\|1[0-4]):[0-5]\\d$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 346. Extract an event ID from a calendar link | `~[?&]event_id=(\d+)(?:&\|$)~` | `$text = "/calendar?event_id=309&view=week"; preg_match('~[?&]event_id=(\\d+)(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `309` |

## 5. Money, receipts and invoices

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 347. Extract a dollar amount from an order confirmation | `~\$(\d+(?:\.\d{2})?)\b~` | `$text = "Total: \$184.95"; preg_match('~\\$(\\d+(?:\\.\\d{2})?)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `184.95` |
| 348. Extract a euro amount from a price label | `~€\s*(\d+(?:[.,]\d{2})?)\b~` | `$text = "Price € 39,90"; preg_match('~€\\s*(\\d+(?:[.,]\\d{2})?)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `39,90` |
| 349. Validate a currency plus amount field | `~^(?:USD\|EUR\|GBP)\s+\d+(?:\.\d{2})?$~` | `$text = "USD 125.00"; echo preg_match('~^(?:USD\|EUR\|GBP)\\s+\\d+(?:\\.\\d{2})?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 350. Find invoice numbers in an email body | `~\bINV-\d{4,8}\b~` | `$text = "Please pay INV-202602 and INV-202603"; preg_match_all('~\\bINV-\\d{4,8}\\b~', $text, $m); echo implode(', ', $m[0]);` | `INV-202602, INV-202603` |
| 351. Extract the invoice year and number as one reference | `~\bINV-\d{4}-\d{5}\b~` | `$text = "Reference INV-2026-00418"; preg_match('~\\bINV-\\d{4}-\\d{5}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `INV-2026-00418` |
| 352. Extract the numeric receipt ID | `~\breceipt\s*#\s*(\d{5,12})\b~i` | `$text = "Receipt # 880135"; preg_match('~\\breceipt\\s*#\\s*(\\d{5,12})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `880135` |
| 353. Validate a tax-rate percentage | `~^(?:100\|[1-9]?\d)(?:\.\d{1,2})?%$~` | `$text = "19.50%"; echo preg_match('~^(?:100\|[1-9]?\\d)(?:\\.\\d{1,2})?%$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 354. Find a discount percentage in an offer | `~\b(\d{1,2})%\s+off\b~i` | `$text = "Get 25% off"; preg_match('~\\b(\\d{1,2})%\\s+off\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `25` |
| 355. Extract an order total from a plain-text receipt | `~\bTOTAL:\s*(\d+\.\d{2})\b~` | `$text = "TOTAL: 249.90"; preg_match('~\\bTOTAL:\\s*(\\d+\\.\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `249.90` |
| 356. Remove currency symbols before decimal conversion | `~[$€£]~u` | `$text = "\$249.90"; echo preg_replace('~[$€£]~u', '', $text);` | `249.90` |
| 357. Remove thin group separators from a copied amount | `~(?<=\d)[ ,](?=\d{3}(?:\D\|$))~` | `$text = "1,234,567.89"; echo preg_replace('~(?<=\\d)[ ,](?=\\d{3}(?:\\D\|$))~', '', $text);` | `1234567.89` |
| 358. Extract a transaction reference from a bank notice | `~\bTXN-([A-Z0-9]{10})\b~` | `$text = "Transaction TXN-A90F71C2D4"; preg_match('~\\bTXN-([A-Z0-9]{10})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `A90F71C2D4` |
| 359. Validate a four-digit merchant category code | `~^\d{4}$~` | `$text = "5411"; echo preg_match('~^\\d{4}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 360. Find an IBAN-shaped account reference (format only) | `~\b[A-Z]{2}\d{2}[A-Z0-9]{11,30}\b~` | `$text = "IBAN GB82WEST12345698765432"; preg_match('~\\b[A-Z]{2}\\d{2}[A-Z0-9]{11,30}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `GB82WEST12345698765432` |
| 361. Mask all but the last four digits of a 16-digit test number | `~\b\d{12}(?=\d{4}\b)~` | `$text = "4111111111111111"; echo preg_replace('~\\b\\d{12}(?=\\d{4}\\b)~', '************', $text);` | `************1111` |
| 362. Extract a PO number from a supplier email | `~\bPO[- #:]*(\d{5,9})\b~i` | `$text = "Purchase order PO-408711"; preg_match('~\\bPO[- #:]*(\\d{5,9})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `408711` |
| 363. Validate a cost center with three letters and four digits | `~^[A-Z]{3}-\d{4}$~` | `$text = "OPS-3102"; echo preg_match('~^[A-Z]{3}-\\d{4}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 364. Extract an amount following VAT: | `~\bVAT:\s*(\d+(?:\.\d{2})?)\b~` | `$text = "Subtotal 100.00 VAT: 20.00"; preg_match('~\\bVAT:\\s*(\\d+(?:\\.\\d{2})?)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `20.00` |
| 365. Find money amounts in a ledger note | `~\b\d+\.\d{2}\s*(?:USD\|EUR\|GBP)\b~` | `$text = "125.00 USD, 90.50 EUR, 8.00 GBP"; preg_match_all('~\\b\\d+\\.\\d{2}\\s*(?:USD\|EUR\|GBP)\\b~', $text, $m); echo implode(', ', $m[0]);` | `125.00 USD, 90.50 EUR, 8.00 GBP` |
| 366. Reject an invoice total with three decimal places | `~^\d+\.\d{2}$~` | `$text = "12.345"; echo preg_match('~^\\d+\\.\\d{2}$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 367. Extract a discount code from a receipt | `~\bcoupon:\s*([A-Z0-9_-]{4,16})\b~i` | `$text = "coupon: SAVE20"; preg_match('~\\bcoupon:\\s*([A-Z0-9_-]{4,16})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `SAVE20` |
| 368. Identify a refund reference | `~\bRFND-\d{7}\b~` | `$text = "Refund RFND-0048201 issued"; preg_match('~\\bRFND-\\d{7}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `RFND-0048201` |
| 369. Extract a five-digit payment batch number | `~\bbatch=(\d{5})\b~` | `$text = "batch=10294"; preg_match('~\\bbatch=(\\d{5})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `10294` |
| 370. Validate a three-letter ISO-like currency label | `~^(?:USD\|EUR\|GBP\|JPY\|CAD\|AUD)$~` | `$text = "CAD"; echo preg_match('~^(?:USD\|EUR\|GBP\|JPY\|CAD\|AUD)$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 371. Extract a payment due date from a reminder | `~\bdue:\s*(\d{4}-\d{2}-\d{2})\b~i` | `$text = "Amount \$55 due: 2026-12-01"; preg_match('~\\bdue:\\s*(\\d{4}-\\d{2}-\\d{2})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `2026-12-01` |

## 6. Products, SKUs and inventory

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 372. Validate an uppercase SKU with a numeric suffix | `~^[A-Z]{3}-\d{5}$~` | `$text = "CAM-01348"; echo preg_match('~^[A-Z]{3}-\\d{5}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 373. Extract a SKU from a product description | `~\bSKU:[A-Z0-9-]{5,20}\b~` | `$text = "Camera SKU:CAM-01348"; preg_match('~\\bSKU:[A-Z0-9-]{5,20}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `SKU:CAM-01348` |
| 374. Extract a product ID from a catalog URL | `~/products/(\d+)(?:/\|$)~` | `$text = "/products/48152/details"; preg_match('~/products/(\\d+)(?:/\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `48152` |
| 375. Find all product codes in an order note | `~\b[A-Z]{2}-\d{4}\b~` | `$text = "Add AB-1320 and CD-8831"; preg_match_all('~\\b[A-Z]{2}-\\d{4}\\b~', $text, $m); echo implode(', ', $m[0]);` | `AB-1320, CD-8831` |
| 376. Validate an EAN-13 barcode shape | `~^\d{13}$~` | `$text = "5901234123457"; echo preg_match('~^\\d{13}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 377. Reject a barcode containing letters | `~^\d{8}(?:\d{5})?$~` | `$text = "590ABC4123457"; echo preg_match('~^\\d{8}(?:\\d{5})?$~', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 378. Extract a product model after Model: | `~\bModel:\s*([A-Z0-9-]+)\b~` | `$text = "Model: XPS-9400"; preg_match('~\\bModel:\\s*([A-Z0-9-]+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `XPS-9400` |
| 379. Find a storage capacity on a phone listing | `~\b(?:64\|128\|256\|512)\s*GB\b~i` | `$text = "Phone, 256 GB"; preg_match('~\\b(?:64\|128\|256\|512)\\s*GB\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `256 GB` |
| 380. Find a screen size written in inches | `~\b\d{1,2}(?:\.\d)?\s*(?:inches\|inch\|in)\b~i` | `$text = "Monitor 27 inches"; preg_match('~\\b\\d{1,2}(?:\\.\\d)?\\s*(?:inches\|inch\|in)\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `27 inches` |
| 381. Extract a garment size from a stock line | `~\bsize:\s*(XS\|S\|M\|L\|XL\|XXL)\b~i` | `$text = "Shirt size: XL"; preg_match('~\\bsize:\\s*(XS\|S\|M\|L\|XL\|XXL)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `XL` |
| 382. Validate a stock location code | `~^[A-Z]\d{2}-[A-Z]\d{2}$~` | `$text = "B12-C04"; echo preg_match('~^[A-Z]\\d{2}-[A-Z]\\d{2}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 383. Extract a warehouse bin location | `~\bbin:\s*([A-Z]\d{2}-[A-Z]\d{2})\b~` | `$text = "bin: D04-A19"; preg_match('~\\bbin:\\s*([A-Z]\\d{2}-[A-Z]\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `D04-A19` |
| 384. Find a manufacturing batch number | `~\bLOT-[A-Z0-9]{8}\b~` | `$text = "Box LOT-A92K10B8"; preg_match('~\\bLOT-[A-Z0-9]{8}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `LOT-A92K10B8` |
| 385. Extract product color from a key-value label | `~\bcolor=(red\|blue\|green\|black\|white)\b~i` | `$text = "color=black"; preg_match('~\\bcolor=(red\|blue\|green\|black\|white)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `black` |
| 386. Find product dimensions written LxWxH | `~\b\d+(?:\.\d+)?x\d+(?:\.\d+)?x\d+(?:\.\d+)?\b~` | `$text = "Box 40x30x20 cm"; preg_match('~\\b\\d+(?:\\.\\d+)?x\\d+(?:\\.\\d+)?x\\d+(?:\\.\\d+)?\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `40x30x20` |
| 387. Extract inventory level from a status label | `~\bstock:\s*(\d+)\b~i` | `$text = "Stock: 128 units"; preg_match('~\\bstock:\\s*(\\d+)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `128` |
| 388. Validate a URL-friendly product slug | `~^[a-z0-9]+(?:-[a-z0-9]+)*$~` | `$text = "wireless-noise-cancelling-headphones"; echo preg_match('~^[a-z0-9]+(?:-[a-z0-9]+)*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 389. Replace spaces with hyphens in a product title | `~\s+~` | `$text = "Desk Lamp Pro"; echo preg_replace('~\\s+~', '-', $text);` | `Desk-Lamp-Pro` |
| 390. Extract a year from a product model | `~\bmodel-(20\d{2})-[a-z0-9]+\b~i` | `$text = "model-2026-a1"; preg_match('~\\bmodel-(20\\d{2})-[a-z0-9]+\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `2026` |
| 391. Find a warranty duration in months | `~\bwarranty:\s*(\d+)\s+months?\b~i` | `$text = "Warranty: 24 months"; preg_match('~\\bwarranty:\\s*(\\d+)\\s+months?\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `24` |
| 392. Extract a paint color hex code from a listing | `~#[0-9a-fA-F]{6}\b~` | `$text = "Color #2F80ED"; preg_match('~#[0-9a-fA-F]{6}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `#2F80ED` |
| 393. Find a product variant ID in a URL | `~[?&]variant=(\d+)(?:&\|$)~` | `$text = "/item?variant=44098&source=search"; preg_match('~[?&]variant=(\\d+)(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `44098` |
| 394. Extract a serial number from a delivery note | `~\bS/N:\s*([A-Z0-9]{12})\b~` | `$text = "S/N: 7XA0928F21Q6"; preg_match('~\\bS/N:\\s*([A-Z0-9]{12})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `7XA0928F21Q6` |
| 395. Validate a product label with language suffix | `~^[A-Z]{2,5}-\d{4}-(?:EN\|FR\|DE)$~` | `$text = "BOOK-0149-EN"; echo preg_match('~^[A-Z]{2,5}-\\d{4}-(?:EN\|FR\|DE)$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 396. Find low-stock flags in an inventory export | `~\bLOW:[A-Z]{2,4}-\d{3,6}\b~` | `$text = "LOW:CAM-0015 LOW:SSD-992"; preg_match_all('~\\bLOW:[A-Z]{2,4}-\\d{3,6}\\b~', $text, $m); echo implode(', ', $m[0]);` | `LOW:CAM-0015, LOW:SSD-992` |

## 7. Search queries and filtering

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 397. Extract all words from a simple site-search query | `~[\p{L}\p{N}]+~u` | `$text = "red shoes size 42"; preg_match_all('~[\\p{L}\\p{N}]+~u', $text, $m); echo implode(', ', $m[0]);` | `red, shoes, size, 42` |
| 398. Remove punctuation from a search phrase | `~[^\p{L}\p{N}\s]+~u` | `$text = "Best shoes, ever!"; echo preg_replace('~[^\\p{L}\\p{N}\\s]+~u', '', $text);` | `Best shoes ever` |
| 399. Collapse repeated spaces in search input | `~\s{2,}~` | `$text = "wireless   gaming  mouse"; echo preg_replace('~\\s{2,}~', ' ', $text);` | `wireless gaming mouse` |
| 400. Extract a quoted phrase from a search query | `~\"([^\"]+)\"~` | `$text = "Find \"blue office chair\" now"; preg_match('~\\"([^\\"]+)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `blue office chair` |
| 401. Find tags of the form tag:word | `~\btag:[a-z0-9_-]+\b~i` | `$text = "tag:sale tag:summer"; preg_match_all('~\\btag:[a-z0-9_-]+\\b~i', $text, $m); echo implode(', ', $m[0]);` | `tag:sale, tag:summer` |
| 402. Extract a numeric minimum price filter | `~\bmin_price:(\d+)\b~` | `$text = "shoes min_price:50"; preg_match('~\\bmin_price:(\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `50` |
| 403. Extract a maximum rating filter | `~\brating:(\d(?:\.\d)?)\b~` | `$text = "coffee rating:4.5"; preg_match('~\\brating:(\\d(?:\\.\\d)?)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `4.5` |
| 404. Find a sort key from a query string | `~[?&]sort=(price\|name\|date)(?:&\|$)~` | `$text = "/items?sort=price"; preg_match('~[?&]sort=(price\|name\|date)(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `price` |
| 405. Find a sort direction from a URL | `~[?&]order=(asc\|desc)(?:&\|$)~` | `$text = "/items?order=desc"; preg_match('~[?&]order=(asc\|desc)(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `desc` |
| 406. Extract a page number from pagination | `~[?&]page=([1-9]\d*)(?:&\|$)~` | `$text = "?q=laptop&page=7"; preg_match('~[?&]page=([1-9]\\d*)(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `7` |
| 407. Validate a comma-separated list of numeric IDs | `~^\d+(?:,\d+)*$~` | `$text = "10,20,35"; echo preg_match('~^\\d+(?:,\\d+)*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 408. Extract all IDs from a comma-separated filter | `~\d+~` | `$text = "12, 48, 91"; preg_match_all('~\\d+~', $text, $m); echo implode(', ', $m[0]);` | `12, 48, 91` |
| 409. Validate a filter field such as status:open | `~^(?:status\|type\|owner):[a-z0-9_-]+$~` | `$text = "status:open"; echo preg_match('~^(?:status\|type\|owner):[a-z0-9_-]+$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 410. Extract the value from a key:value search token | `~\bstatus:([a-z]+)\b~` | `$text = "tickets status:pending"; preg_match('~\\bstatus:([a-z]+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `pending` |
| 411. Find excluded words prefixed by minus | `~(?<!\S)-[a-z][a-z0-9-]*\b~i` | `$text = "phones -used -refurbished"; preg_match_all('~(?<!\\S)-[a-z][a-z0-9-]*\\b~i', $text, $m); echo implode(', ', $m[0]);` | `-used, -refurbished` |
| 412. Find an exact numeric product code in a search phrase | `~\b\d{8}\b~` | `$text = "Search 10020546 charger"; preg_match('~\\b\\d{8}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `10020546` |
| 413. Extract a search term from a simple q= parameter | `~[?&]q=([A-Za-z0-9+_-]+)(?:&\|$)~` | `$text = "/search?q=desk+lamp&page=2"; preg_match('~[?&]q=([A-Za-z0-9+_-]+)(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `desk+lamp` |
| 414. Find a minimum year filter | `~\byear>=(20\d{2})\b~` | `$text = "cars year>=2020"; preg_match('~\\byear>=(20\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2020` |
| 415. Find a maximum year filter | `~\byear<=(20\d{2})\b~` | `$text = "cars year<=2026"; preg_match('~\\byear<=(20\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2026` |
| 416. Validate a safe single-word category filter | `~^[a-z][a-z_-]{1,30}$~` | `$text = "home-office"; echo preg_match('~^[a-z][a-z_-]{1,30}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 417. Find Boolean search operators as whole words | `~\b(?:AND\|OR\|NOT)\b~` | `$text = "camera AND lens NOT used"; preg_match_all('~\\b(?:AND\|OR\|NOT)\\b~', $text, $m); echo implode(', ', $m[0]);` | `AND, NOT` |
| 418. Remove repeated commas from a filter list | `~,{2,}~` | `$text = "red,,,blue,,green"; echo preg_replace('~,{2,}~', ',', $text);` | `red,blue,green` |
| 419. Extract a date-from filter | `~\bfrom:(\d{4}-\d{2}-\d{2})\b~` | `$text = "orders from:2026-01-01"; preg_match('~\\bfrom:(\\d{4}-\\d{2}-\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2026-01-01` |
| 420. Extract a date-to filter | `~\bto:(\d{4}-\d{2}-\d{2})\b~` | `$text = "orders to:2026-02-01"; preg_match('~\\bto:(\\d{4}-\\d{2}-\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2026-02-01` |
| 421. Find wildcard tags ending in an asterisk | `~\b[a-z][a-z0-9_-]*\*~i` | `$text = "Try dev* or design*"; preg_match_all('~\\b[a-z][a-z0-9_-]*\\*~i', $text, $m); echo implode(', ', $m[0]);` | `dev*, design*` |

## 8. URLs, domains and routing

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 422. Extract the hostname from an HTTPS URL | `~^https://([^/:?#]+)~i` | `$text = "https://docs.example.org/setup"; preg_match('~^https://([^/:?#]+)~i', $text, $m); echo $m[1] ?? 'Not found';` | `docs.example.org` |
| 423. Find all HTTPS links in a sentence | `~https://[^\s<>\"']+~i` | `$text = "Visit https://a.example.org and https://b.example.net"; preg_match_all('~https://[^\\s<>\\"\']+~i', $text, $m); echo implode(', ', $m[0]);` | `https://a.example.org, https://b.example.net` |
| 424. Validate an absolute HTTP or HTTPS URL shape | `~^https?://[A-Za-z0-9.-]+(?::\d{2,5})?(?:/[^\s]*)?$~i` | `$text = "https://example.com/articles/42"; echo preg_match('~^https?://[A-Za-z0-9.-]+(?::\\d{2,5})?(?:/[^\\s]*)?$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 425. Extract the path from a full URL | `~^https?://[^/]+(/[^?#]*)~i` | `$text = "https://example.com/blog/latest?ref=1"; preg_match('~^https?://[^/]+(/[^?#]*)~i', $text, $m); echo $m[1] ?? 'Not found';` | `/blog/latest` |
| 426. Extract the fragment identifier from a link | `~#([A-Za-z][A-Za-z0-9_-]*)$~` | `$text = "/guide#installation"; preg_match('~#([A-Za-z][A-Za-z0-9_-]*)$~', $text, $m); echo $m[1] ?? 'Not found';` | `installation` |
| 427. Extract the value of a simple tracking parameter | `~[?&]utm_source=([a-z0-9_-]+)(?:&\|$)~i` | `$text = "/offer?utm_source=newsletter&x=1"; preg_match('~[?&]utm_source=([a-z0-9_-]+)(?:&\|$)~i', $text, $m); echo $m[1] ?? 'Not found';` | `newsletter` |
| 428. Remove tracking parameters from a simple URL tail | `~[?&]utm_[a-z_]+=[^&#]*~` | `$text = "/shop?utm_source=email"; echo preg_replace('~[?&]utm_[a-z_]+=[^&#]*~', '', $text);` | `/shop` |
| 429. Find the protocol of a URL | `~^(https?)://~i` | `$text = "https://example.net"; preg_match('~^(https?)://~i', $text, $m); echo $m[1] ?? 'Not found';` | `https` |
| 430. Extract a port number from a development URL | `~^https?://[^/:]+:(\d{2,5})\b~` | `$text = "http://localhost:8080/app"; preg_match('~^https?://[^/:]+:(\\d{2,5})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `8080` |
| 431. Validate a route with a numeric item ID | `~^/items/[1-9]\d*$~` | `$text = "/items/205"; echo preg_match('~^/items/[1-9]\\d*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 432. Extract the language prefix from a route | `~^/(en\|de\|fr\|es)/~` | `$text = "/fr/products"; preg_match('~^/(en\|de\|fr\|es)/~', $text, $m); echo $m[1] ?? 'Not found';` | `fr` |
| 433. Extract an article slug from a blog URL | `~^/blog/([a-z0-9]+(?:-[a-z0-9]+)*)$~` | `$text = "/blog/learn-php-regex"; preg_match('~^/blog/([a-z0-9]+(?:-[a-z0-9]+)*)$~', $text, $m); echo $m[1] ?? 'Not found';` | `learn-php-regex` |
| 434. Find domain names in server output | `~\b(?:[a-z0-9-]+\.)+[a-z]{2,}\b~i` | `$text = "Sites a.example.com and b.example.net"; preg_match_all('~\\b(?:[a-z0-9-]+\\.)+[a-z]{2,}\\b~i', $text, $m); echo implode(', ', $m[0]);` | `a.example.com, b.example.net` |
| 435. Validate a local anchor link | `~^#[A-Za-z][A-Za-z0-9_-]*$~` | `$text = "#contact-form"; echo preg_match('~^#[A-Za-z][A-Za-z0-9_-]*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 436. Remove a trailing slash from a non-root path | `~(?<!^)/+$~` | `$text = "/users/active///"; echo preg_replace('~(?<!^)/+$~', '', $text);` | `/users/active` |
| 437. Replace repeated slashes in a URL path | `~/{2,}~` | `$text = "/shop//products///recent"; echo preg_replace('~/{2,}~', '/', $text);` | `/shop/products/recent` |
| 438. Extract an image filename from a URL | `~/([^/?#]+\.(?:jpg\|jpeg\|png\|webp))(?:[?#]\|$)~i` | `$text = "https://cdn.example.org/img/photo.webp?w=600"; preg_match('~/([^/?#]+\\.(?:jpg\|jpeg\|png\|webp))(?:[?#]\|$)~i', $text, $m); echo $m[1] ?? 'Not found';` | `photo.webp` |
| 439. Extract a category segment from an item URL | `~^/catalog/([^/]+)/[^/]+$~` | `$text = "/catalog/shoes/blue-runner"; preg_match('~^/catalog/([^/]+)/[^/]+$~', $text, $m); echo $m[1] ?? 'Not found';` | `shoes` |
| 440. Check that a page path contains no whitespace | `~^/[A-Za-z0-9/_-]*$~` | `$text = "/help/contact-us"; echo preg_match('~^/[A-Za-z0-9/_-]*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 441. Extract a query-string key name | `~[?&]([a-z_][a-z0-9_]*)=~i` | `$text = "/search?category=books&page=2"; preg_match('~[?&]([a-z_][a-z0-9_]*)=~i', $text, $m); echo $m[1] ?? 'Not found';` | `category` |
| 442. Find a URL-encoded space in a query | `~%20~i` | `$text = "name=Blue%20Lamp"; preg_match('~%20~i', $text, $m); echo $m[0] ?? 'Not found';` | `%20` |
| 443. Validate a lowercase subdomain label | `~^[a-z0-9](?:[a-z0-9-]{0,61}[a-z0-9])?$~` | `$text = "support"; echo preg_match('~^[a-z0-9](?:[a-z0-9-]{0,61}[a-z0-9])?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 444. Extract a file extension from a download link | `~\.([a-z0-9]{2,5})(?:[?#]\|$)~i` | `$text = "/downloads/report.pdf?x=1"; preg_match('~\\.([a-z0-9]{2,5})(?:[?#]\|$)~i', $text, $m); echo $m[1] ?? 'Not found';` | `pdf` |
| 445. Find a version segment inside a REST route | `~^/api/(v[1-9]\d*)/~` | `$text = "/api/v2/users"; preg_match('~^/api/(v[1-9]\\d*)/~', $text, $m); echo $m[1] ?? 'Not found';` | `v2` |
| 446. Validate an article URL path with a numeric year | `~^/news/20\d{2}/[a-z0-9-]+$~` | `$text = "/news/2026/new-office"; echo preg_match('~^/news/20\\d{2}/[a-z0-9-]+$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |

## 9. Files, paths and uploads

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 447. Validate a PDF filename for a download form | `~^[A-Za-z0-9_-]+\.pdf$~i` | `$text = "annual_report.pdf"; echo preg_match('~^[A-Za-z0-9_-]+\\.pdf$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 448. Extract a file extension | `~\.([A-Za-z0-9]+)$~` | `$text = "invoice.xlsx"; preg_match('~\\.([A-Za-z0-9]+)$~', $text, $m); echo $m[1] ?? 'Not found';` | `xlsx` |
| 449. Allow only common uploaded image extensions | `~^[^/\\]+\.(?:jpg\|jpeg\|png\|webp\|gif)$~i` | `$text = "summer_photo.JPG"; echo preg_match('~^[^/\\\\]+\\.(?:jpg\|jpeg\|png\|webp\|gif)$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 450. Reject an uploaded script extension | `~^[^/\\]+\.(?:jpg\|jpeg\|png\|webp)$~i` | `$text = "photo.php"; echo preg_match('~^[^/\\\\]+\\.(?:jpg\|jpeg\|png\|webp)$~i', $text) ? 'Valid' : 'Invalid';` | `Invalid` |
| 451. Extract the basename from a Unix-style path | `~/([^/]+)$~` | `$text = "/var/backups/site.sql"; preg_match('~/([^/]+)$~', $text, $m); echo $m[1] ?? 'Not found';` | `site.sql` |
| 452. Extract the directory of a Unix-style path | `~^(.+)/[^/]+$~` | `$text = "/srv/app/config.ini"; preg_match('~^(.+)/[^/]+$~', $text, $m); echo $m[1] ?? 'Not found';` | `/srv/app` |
| 453. Find a Windows drive letter | `~^([A-Za-z]):\\~` | `$text = "C:\\Projects\\app\\readme.md"; preg_match('~^([A-Za-z]):\\\\~', $text, $m); echo $m[1] ?? 'Not found';` | `C` |
| 454. Extract a filename from a Windows path | `~\\([^\\]+)$~` | `$text = "D:\\Work\\notes.txt"; preg_match('~\\\\([^\\\\]+)$~', $text, $m); echo $m[1] ?? 'Not found';` | `notes.txt` |
| 455. Find dated backup archives | `~\bbackup_\d{8}\.zip\b~i` | `$text = "backup_20261110.zip backup_20261111.zip"; preg_match_all('~\\bbackup_\\d{8}\\.zip\\b~i', $text, $m); echo implode(', ', $m[0]);` | `backup_20261110.zip, backup_20261111.zip` |
| 456. Extract a timestamp from a server backup name | `~\bdb_(\d{8}_\d{6})\.sql\b~` | `$text = "db_20261111_021500.sql"; preg_match('~\\bdb_(\\d{8}_\\d{6})\\.sql\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `20261111_021500` |
| 457. Validate a log rotation filename | `~^[a-z][a-z0-9_-]*\.log\.\d+$~` | `$text = "access.log.3"; echo preg_match('~^[a-z][a-z0-9_-]*\\.log\\.\\d+$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 458. Extract an image resolution from a filename | `~_(\d{3,4}x\d{3,4})\.(?:jpg\|png\|webp)$~i` | `$text = "banner_1200x628.png"; preg_match('~_(\\d{3,4}x\\d{3,4})\\.(?:jpg\|png\|webp)$~i', $text, $m); echo $m[1] ?? 'Not found';` | `1200x628` |
| 459. Remove a numeric copy suffix from a filename | `~\s*\(\d+\)(?=\.[^.]+$)~` | `$text = "Report (3).pdf"; echo preg_replace('~\\s*\\(\\d+\\)(?=\\.[^.]+$)~', '', $text);` | `Report.pdf` |
| 460. Replace spaces in a download filename | `~\s+~` | `$text = "Q4 Sales Summary.pdf"; echo preg_replace('~\\s+~', '_', $text);` | `Q4_Sales_Summary.pdf` |
| 461. Extract a two-letter locale from a file name | `~_([a-z]{2})\.(?:json\|po)$~` | `$text = "messages_fr.json"; preg_match('~_([a-z]{2})\\.(?:json\|po)$~', $text, $m); echo $m[1] ?? 'Not found';` | `fr` |
| 462. Validate a versioned asset filename | `~^[a-z0-9_-]+\.[a-f0-9]{8}\.(?:css\|js)$~i` | `$text = "app.9a41e0bc.js"; echo preg_match('~^[a-z0-9_-]+\\.[a-f0-9]{8}\\.(?:css\|js)$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 463. Find files ending in .bak in a directory listing | `~\b[A-Za-z0-9_.-]+\.bak\b~` | `$text = "config.bak index.php config.ini.bak"; preg_match_all('~\\b[A-Za-z0-9_.-]+\\.bak\\b~', $text, $m); echo implode(', ', $m[0]);` | `config.bak, config.ini.bak` |
| 464. Extract a checksum from a filename | `~_sha256_([a-f0-9]{12})\.tar\.gz$~` | `$text = "archive_sha256_9a1b2c3d4e5f.tar.gz"; preg_match('~_sha256_([a-f0-9]{12})\\.tar\\.gz$~', $text, $m); echo $m[1] ?? 'Not found';` | `9a1b2c3d4e5f` |
| 465. Validate a simple Linux config filename | `~^[a-z][a-z0-9_.-]*\.conf$~` | `$text = "web-server.conf"; echo preg_match('~^[a-z][a-z0-9_.-]*\\.conf$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 466. Find document attachments in a mail summary | `~\b[\w.-]+\.(?:pdf\|docx\|xlsx)\b~i` | `$text = "Attached quote.pdf and costs.xlsx"; preg_match_all('~\\b[\\w.-]+\\.(?:pdf\|docx\|xlsx)\\b~i', $text, $m); echo implode(', ', $m[0]);` | `quote.pdf, costs.xlsx` |
| 467. Extract an upload ID from a temporary path | `~/uploads/([a-f0-9]{16})/~` | `$text = "/uploads/a1b2c3d4e5f60718/photo.png"; preg_match('~/uploads/([a-f0-9]{16})/~', $text, $m); echo $m[1] ?? 'Not found';` | `a1b2c3d4e5f60718` |
| 468. Validate a year/month upload folder | `~^/uploads/20\d{2}/(?:0[1-9]\|1[0-2])/$~` | `$text = "/uploads/2026/11/"; echo preg_match('~^/uploads/20\\d{2}/(?:0[1-9]\|1[0-2])/$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 469. Remove redundant ./ from a local relative path | `~^(?:\./)+~` | `$text = "././images/icon.png"; echo preg_replace('~^(?:\\./)+~', '', $text);` | `images/icon.png` |
| 470. Extract a compression format from an archive | `~\.(zip\|7z\|rar\|tar\.gz)$~i` | `$text = "release.tar.gz"; preg_match('~\\.(zip\|7z\|rar\|tar\\.gz)$~i', $text, $m); echo $m[1] ?? 'Not found';` | `tar.gz` |
| 471. Find all numbered report files | `~\breport-\d{3}\.csv\b~` | `$text = "report-001.csv report-002.csv"; preg_match_all('~\\breport-\\d{3}\\.csv\\b~', $text, $m); echo implode(', ', $m[0]);` | `report-001.csv, report-002.csv` |

## 10. Cleaning and normalizing text

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 472. Collapse several spaces into one | `~ {2,}~` | `$text = "Hello     world"; echo preg_replace('~ {2,}~', ' ', $text);` | `Hello world` |
| 473. Remove leading spaces from copied text | `~^ +~` | `$text = "    Welcome!"; echo preg_replace('~^ +~', '', $text);` | `Welcome!` |
| 474. Remove trailing whitespace from a form entry | `~\s+$~` | `$text = "Submitted   "; echo preg_replace('~\\s+$~', '', $text);` | `Submitted` |
| 475. Replace tabs with ordinary spaces | `~\t+~` | `$text = "Name\tAge\tCity"; echo preg_replace('~\\t+~', ' ', $text);` | `Name Age City` |
| 476. Remove repeated punctuation in a message | `~([!?])\1+~` | `$text = "Really??? Wow!!!"; echo preg_replace('~([!?])\\1+~', '$1', $text);` | `Really? Wow!` |
| 477. Collapse multiple hyphens in a slug | `~-{2,}~` | `$text = "new---summer--sale"; echo preg_replace('~-{2,}~', '-', $text);` | `new-summer-sale` |
| 478. Remove HTML-like tags from a known plain-text snippet | `~<[^>]*>~` | `$text = "Hello <b>friend</b>"; echo preg_replace('~<[^>]*>~', '', $text);` | `Hello friend` |
| 479. Remove square-bracketed editor notes | `~\[[^\]]*]\s*~` | `$text = "Ready [draft] for release"; echo preg_replace('~\\[[^\\]]*]\\s*~', '', $text);` | `Ready for release` |
| 480. Remove a leading list number from a heading | `~^\s*\d+[.)]\s*~` | `$text = "12. Getting Started"; echo preg_replace('~^\\s*\\d+[.)]\\s*~', '', $text);` | `Getting Started` |
| 481. Replace underscores with spaces for a label | `~_+~` | `$text = "first_name_field"; echo preg_replace('~_+~', ' ', $text);` | `first name field` |
| 482. Remove a UTF-8 BOM at the start of imported text | `~^\x{FEFF}~u` | `$text = "﻿Header"; echo preg_replace('~^\\x{FEFF}~u', '', $text);` | `Header` |
| 483. Collapse several blank lines into one separator | `~(?:\r?\n){3,}~` | `$text = "A\n\n\n\nB"; echo json_encode(preg_replace('~(?:\\r?\\n){3,}~', "\n\n", $text), JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"A\n\nB"` |
| 484. Remove spaces directly before punctuation | `~\s+([,.;!?])~` | `$text = "Hello , friend !"; echo preg_replace('~\\s+([,.;!?])~', '$1', $text);` | `Hello, friend!` |
| 485. Add a space after commas when missing | `~,(?=\S)~` | `$text = "Red,Green,Blue"; echo preg_replace('~,(?=\\S)~', ', ', $text);` | `Red, Green, Blue` |
| 486. Remove all non-digit characters from a phone value | `~\D+~` | `$text = "(212) 555-0198"; echo preg_replace('~\\D+~', '', $text);` | `2125550198` |
| 487. Turn runs of dots into a single dot | `~\.{2,}~` | `$text = "Wait.... please..."; echo preg_replace('~\\.{2,}~', '.', $text);` | `Wait. please.` |
| 488. Strip a trailing file extension from a display name | `~\.[^.]+$~` | `$text = "final-report.docx"; echo preg_replace('~\\.[^.]+$~', '', $text);` | `final-report` |
| 489. Remove spaces on both sides of equals signs | `~\s*=\s*~` | `$text = "color = blue"; echo preg_replace('~\\s*=\\s*~', '=', $text);` | `color=blue` |
| 490. Normalize whitespace around a colon in a label | `~\s*:\s*~` | `$text = "Status :   Active"; echo preg_replace('~\\s*:\\s*~', ': ', $text);` | `Status: Active` |
| 491. Remove blank parentheses left by an editor | `~\s*\(\s*\)~` | `$text = "Notes () today"; echo preg_replace('~\\s*\\(\\s*\\)~', '', $text);` | `Notes today` |
| 492. Remove duplicate consecutive commas | `~(?:,\s*){2,}~` | `$text = "one,, two,,, three"; echo preg_replace('~(?:,\\s*){2,}~', ', ', $text);` | `one, two, three` |
| 493. Replace repeated forward slashes in a relative path | `~/{2,}~` | `$text = "docs///manual//intro"; echo preg_replace('~/{2,}~', '/', $text);` | `docs/manual/intro` |
| 494. Normalize mixed line endings to LF | `~\r\n?~` | `$text = "First\r\nSecond\rThird"; echo json_encode(preg_replace('~\\r\\n?~', "\n", $text), JSON_UNESCAPED_UNICODE \| JSON_UNESCAPED_SLASHES);` | `"First\nSecond\nThird"` |
| 495. Remove ASCII control characters except tabs and line feeds | `~[\x00-\x08\x0B\x0C\x0E-\x1F\x7F]~` | `$text = "Good morning"; echo preg_replace('~[\\x00-\\x08\\x0B\\x0C\\x0E-\\x1F\\x7F]~', '', $text);` | `Good morning` |
| 496. Trim extra spaces after opening parentheses | `~\(\s+~` | `$text = "Call (   tomorrow)"; echo preg_replace('~\\(\\s+~', '(', $text);` | `Call (tomorrow)` |

## 11. Notifications and chat messages

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 497. Extract a ticket reference from a notification | `~\bTKT-\d{6}\b~` | `$text = "Ticket TKT-004812 updated"; preg_match('~\\bTKT-\\d{6}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `TKT-004812` |
| 498. Find the first @mention in a chat message | `~(?<!\w)@[A-Za-z]\w{1,20}\b~` | `$text = "Thanks @becca for the fix"; preg_match('~(?<!\\w)@[A-Za-z]\\w{1,20}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `@becca` |
| 499. List all @mentions from a comment | `~(?<!\w)@[A-Za-z]\w*\b~` | `$text = "@ana @leo Please review"; preg_match_all('~(?<!\\w)@[A-Za-z]\\w*\\b~', $text, $m); echo implode(', ', $m[0]);` | `@ana, @leo` |
| 500. Find hashtags in a status update | `~(?<!\w)#[A-Za-z][A-Za-z0-9_]*\b~` | `$text = "Release #beta #mobile"; preg_match_all('~(?<!\\w)#[A-Za-z][A-Za-z0-9_]*\\b~', $text, $m); echo implode(', ', $m[0]);` | `#beta, #mobile` |
| 501. Extract a one-time code mentioned in an SMS | `~\bcode:\s*(\d{6})\b~i` | `$text = "Your code: 118204"; preg_match('~\\bcode:\\s*(\\d{6})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `118204` |
| 502. Extract a delivery tracking code from a message | `~\btracking:\s*([A-Z0-9]{12,20})\b~i` | `$text = "Tracking: 1Z999AA10123456784"; preg_match('~\\btracking:\\s*([A-Z0-9]{12,20})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `1Z999AA10123456784` |
| 503. Find a quoted text reply segment | `~\"([^\"]{1,120})\"~` | `$text = "He replied \"I will join\""; preg_match('~\\"([^\\"]{1,120})\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `I will join` |
| 504. Detect a message beginning with /help | `~^/help(?:\s+\S+)?$~` | `$text = "/help commands"; echo preg_match('~^/help(?:\\s+\\S+)?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 505. Extract the command from a slash-command message | `~^/([a-z][a-z0-9_-]*)\b~` | `$text = "/remind tomorrow"; preg_match('~^/([a-z][a-z0-9_-]*)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `remind` |
| 506. Detect a chat message prefixed by [URGENT] | `~^\[URGENT\]~` | `$text = "[URGENT] Server offline"; preg_match('~^\\[URGENT\\]~', $text, $m); echo $m[0] ?? 'Not found';` | `[URGENT]` |
| 507. Extract a room number from a meeting reminder | `~\broom\s+([A-Z]\d{2,4})\b~i` | `$text = "Meet in room B204"; preg_match('~\\broom\\s+([A-Z]\\d{2,4})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `B204` |
| 508. Find a clickable-looking invite code in a message | `~\bINVITE-[A-Z2-9]{8}\b~` | `$text = "Use INVITE-PK3Q5R7T"; preg_match('~\\bINVITE-[A-Z2-9]{8}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `INVITE-PK3Q5R7T` |
| 509. Extract an RSVP status from a reply | `~\bRSVP:\s*(yes\|no\|maybe)\b~i` | `$text = "RSVP: maybe"; preg_match('~\\bRSVP:\\s*(yes\|no\|maybe)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `maybe` |
| 510. Find a due time in a push notification | `~\b(?:[01]\d\|2[0-3]):[0-5]\d\b~` | `$text = "Reminder due at 17:45"; preg_match('~\\b(?:[01]\\d\|2[0-3]):[0-5]\\d\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `17:45` |
| 511. Extract an unread-count badge value | `~\bunread:\s*(\d+)\b~` | `$text = "unread: 12"; preg_match('~\\bunread:\\s*(\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `12` |
| 512. Find a task ID in a status message | `~\bTASK-(\d{4,8})\b~` | `$text = "Completed TASK-90125"; preg_match('~\\bTASK-(\\d{4,8})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `90125` |
| 513. Extract a numeric poll choice | `~\bvote:\s*([1-9]\d*)\b~i` | `$text = "Vote: 3"; preg_match('~\\bvote:\\s*([1-9]\\d*)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `3` |
| 514. Find an inline emoji short code | `~:[a-z_]{2,24}:~` | `$text = "Great :thumbs_up: :sparkles:"; preg_match_all('~:[a-z_]{2,24}:~', $text, $m); echo implode(', ', $m[0]);` | `:thumbs_up:, :sparkles:` |
| 515. Extract a time span from a chat booking | `~\b\d{1,2}:\d{2}\s*-\s*\d{1,2}:\d{2}\b~` | `$text = "Book 9:00 - 10:30"; preg_match('~\\b\\d{1,2}:\\d{2}\\s*-\\s*\\d{1,2}:\\d{2}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `9:00 - 10:30` |
| 516. Remove repetitive exclamation marks in a notice | `~!{2,}~` | `$text = "Alert!!! Please read!!"; echo preg_replace('~!{2,}~', '!', $text);` | `Alert! Please read!` |
| 517. Find a feedback rating from a comment | `~\brating\s*(\d)/5\b~i` | `$text = "Rating 4/5"; preg_match('~\\brating\\s*(\\d)/5\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `4` |
| 518. Extract a delivery window date from a message | `~\bdeliver\s+on\s+(\d{4}-\d{2}-\d{2})\b~i` | `$text = "Deliver on 2026-12-02"; preg_match('~\\bdeliver\\s+on\\s+(\\d{4}-\\d{2}-\\d{2})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `2026-12-02` |
| 519. Find a support reference number in chat | `~\bCASE-\d{5}\b~` | `$text = "Case CASE-55109 reopened"; preg_match('~\\bCASE-\\d{5}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `CASE-55109` |
| 520. Extract a channel name after #channel: | `~#channel:([a-z0-9_-]+)\b~` | `$text = "#channel:announcements"; preg_match('~#channel:([a-z0-9_-]+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `announcements` |
| 521. Detect an automatic reply disclaimer | `~\bautomated (?:reply\|message)\b~i` | `$text = "This is an automated message."; preg_match('~\\bautomated (?:reply\|message)\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `automated message` |

## 12. Logs, errors and monitoring

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 522. Extract a log level from a bracketed log line | `~^\[(DEBUG\|INFO\|WARN\|ERROR)\]~` | `$text = "[ERROR] Database unavailable"; preg_match('~^\\[(DEBUG\|INFO\|WARN\|ERROR)\\]~', $text, $m); echo $m[1] ?? 'Not found';` | `ERROR` |
| 523. Find ISO timestamps in an application log | `~\b\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}Z\b~` | `$text = "2026-11-11T09:00:00Z 2026-11-11T10:00:00Z"; preg_match_all('~\\b\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}Z\\b~', $text, $m); echo implode(', ', $m[0]);` | `2026-11-11T09:00:00Z, 2026-11-11T10:00:00Z` |
| 524. Extract a process ID from a service message | `~\bpid[=:]\s*(\d+)\b~i` | `$text = "worker pid=3817 started"; preg_match('~\\bpid[=:]\\s*(\\d+)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `3817` |
| 525. Find an HTTP status code in a log | `~\bstatus[=:]\s*([1-5]\d{2})\b~i` | `$text = "GET /status status=503"; preg_match('~\\bstatus[=:]\\s*([1-5]\\d{2})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `503` |
| 526. Find all response times in a performance log | `~\b\d+(?:\.\d+)?ms\b~` | `$text = "db=7ms api=49ms total=57ms"; preg_match_all('~\\b\\d+(?:\\.\\d+)?ms\\b~', $text, $m); echo implode(', ', $m[0]);` | `7ms, 49ms, 57ms` |
| 527. Extract a request ID from an audit message | `~\brequest_id=([a-f0-9]{16})\b~` | `$text = "request_id=a98c771d2290ef11"; preg_match('~\\brequest_id=([a-f0-9]{16})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `a98c771d2290ef11` |
| 528. Extract a database query duration | `~\bquery_time=(\d+(?:\.\d+)?)ms\b~` | `$text = "query_time=23.7ms"; preg_match('~\\bquery_time=(\\d+(?:\\.\\d+)?)ms\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `23.7` |
| 529. Extract a log source module | `~\bmodule=([a-z][a-z0-9_.-]+)\b~` | `$text = "module=payment.worker"; preg_match('~\\bmodule=([a-z][a-z0-9_.-]+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `payment.worker` |
| 530. Detect a PHP fatal error prefix | `~\bPHP Fatal error:~` | `$text = "PHP Fatal error: Uncaught Error"; preg_match('~\\bPHP Fatal error:~', $text, $m); echo $m[0] ?? 'Not found';` | `PHP Fatal error:` |
| 531. Find PHP warning entries | `~\bPHP Warning:\s*[^;]+~` | `$text = "PHP Warning: file missing; PHP Warning: bad header"; preg_match_all('~\\bPHP Warning:\\s*[^;]+~', $text, $m); echo implode(', ', $m[0]);` | `PHP Warning: file missing, PHP Warning: bad header` |
| 532. Extract a failing filename and line number | `~\bin\s+[\w./-]+\.php\s+on\s+line\s+(\d+)\b~` | `$text = "in src/router.php on line 81"; preg_match('~\\bin\\s+[\\w./-]+\\.php\\s+on\\s+line\\s+(\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `81` |
| 533. Find SQLSTATE error codes | `~\bSQLSTATE\[[A-Z0-9]{5}\]~` | `$text = "SQLSTATE[23000] then SQLSTATE[42000]"; preg_match_all('~\\bSQLSTATE\\[[A-Z0-9]{5}\\]~', $text, $m); echo implode(', ', $m[0]);` | `SQLSTATE[23000], SQLSTATE[42000]` |
| 534. Extract a memory usage value from a log | `~\bmemory=(\d+(?:\.\d+)?)MB\b~` | `$text = "memory=128.4MB"; preg_match('~\\bmemory=(\\d+(?:\\.\\d+)?)MB\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `128.4` |
| 535. Find connection refused messages | `~\bconnection refused\b~i` | `$text = "ERROR Connection refused by peer"; preg_match('~\\bconnection refused\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `Connection refused` |
| 536. Extract a client IPv4 address from an access log | `~\b(?:\d{1,3}\.){3}\d{1,3}\b~` | `$text = "203.0.113.7 GET /"; preg_match('~\\b(?:\\d{1,3}\\.){3}\\d{1,3}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `203.0.113.7` |
| 537. Extract a URL path from a quoted GET request | `~\"GET\s+(/[^\s]*)\s+HTTP/\d\.\d\"~` | `$text = "\"GET /api/users HTTP/1.1\" 200"; preg_match('~\\"GET\\s+(/[^\\s]*)\\s+HTTP/\\d\\.\\d\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `/api/users` |
| 538. Find HTTP 5xx errors in an access-log excerpt | `~\b5\d{2}\b~` | `$text = "GET / 200; GET /cart 502; GET /api 503"; preg_match_all('~\\b5\\d{2}\\b~', $text, $m); echo implode(', ', $m[0]);` | `502, 503` |
| 539. Extract a port number from a listening message | `~\blistening\s+on\s+port\s+(\d{2,5})\b~i` | `$text = "Listening on port 8081"; preg_match('~\\blistening\\s+on\\s+port\\s+(\\d{2,5})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `8081` |
| 540. Find a restarted-service notice | `~\bservice\s+\w+\s+restarted\b~i` | `$text = "Service nginx restarted"; preg_match('~\\bservice\\s+\\w+\\s+restarted\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `Service nginx restarted` |
| 541. Extract CPU utilization from a metric line | `~\bcpu_usage=(\d+(?:\.\d+)?)%~` | `$text = "cpu_usage=78.5%"; preg_match('~\\bcpu_usage=(\\d+(?:\\.\\d+)?)%~', $text, $m); echo $m[1] ?? 'Not found';` | `78.5` |
| 542. Extract a failed login username from an audit log | `~\bfailed login for ([a-z0-9_.-]+)\b~i` | `$text = "Failed login for guest_4"; preg_match('~\\bfailed login for ([a-z0-9_.-]+)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `guest_4` |
| 543. Extract an error code from a server response | `~\berror_code=([A-Z][A-Z0-9_]+)\b~` | `$text = "error_code=AUTH_EXPIRED"; preg_match('~\\berror_code=([A-Z][A-Z0-9_]+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `AUTH_EXPIRED` |
| 544. Find a retry attempt number | `~\bretry\s+(\d+)\s+of\s+\d+\b~i` | `$text = "Retry 2 of 5"; preg_match('~\\bretry\\s+(\\d+)\\s+of\\s+\\d+\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `2` |
| 545. Find a run of at least three hash markers | `~#{3,}~` | `$text = "Progress ######## done"; preg_match('~#{3,}~', $text, $m); echo $m[0] ?? 'Not found';` | `########` |
| 546. Extract a Docker-like short container ID | `~\bcontainer=([a-f0-9]{12})\b~` | `$text = "container=8c6f0a1b2c3d"; preg_match('~\\bcontainer=([a-f0-9]{12})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `8c6f0a1b2c3d` |

## 13. HTTP headers, requests and APIs

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 547. Extract a bearer token from an Authorization header | `~^Authorization:\s+Bearer\s+([A-Za-z0-9._-]+)$~im` | `$text = "Authorization: Bearer aBc.012-xyz"; preg_match('~^Authorization:\\s+Bearer\\s+([A-Za-z0-9._-]+)$~im', $text, $m); echo $m[1] ?? 'Not found';` | `aBc.012-xyz` |
| 548. Find the Content-Type of a response header | `~^Content-Type:\s*([^\r\n;]+)~im` | `$text = "Content-Type: application/json"; preg_match('~^Content-Type:\\s*([^\\r\\n;]+)~im', $text, $m); echo $m[1] ?? 'Not found';` | `application/json` |
| 549. Extract an HTTP status line code | `~^HTTP/\d(?:\.\d)?\s+([1-5]\d{2})\b~` | `$text = "HTTP/1.1 404 Not Found"; preg_match('~^HTTP/\\d(?:\\.\\d)?\\s+([1-5]\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `404` |
| 550. Find JSON Content-Type headers in a response | `~^Content-Type:\s*application/json\b~im` | `$text = "Content-Type: application/json"; preg_match('~^Content-Type:\\s*application/json\\b~im', $text, $m); echo $m[0] ?? 'Not found';` | `Content-Type: application/json` |
| 551. Extract an HTTP method from a request line | `~^(GET\|POST\|PUT\|PATCH\|DELETE)\s+/~` | `$text = "PATCH /users/7 HTTP/1.1"; preg_match('~^(GET\|POST\|PUT\|PATCH\|DELETE)\\s+/~', $text, $m); echo $m[1] ?? 'Not found';` | `PATCH` |
| 552. Extract a route from an HTTP request line | `~^(?:GET\|POST\|PUT\|DELETE)\s+(/[^\s]*)\s+HTTP/~` | `$text = "GET /api/v2/users HTTP/1.1"; preg_match('~^(?:GET\|POST\|PUT\|DELETE)\\s+(/[^\\s]*)\\s+HTTP/~', $text, $m); echo $m[1] ?? 'Not found';` | `/api/v2/users` |
| 553. Extract a numeric status from a JSON-shaped response | `~\"status\"\s*:\s*(\d{3})~` | `$text = "{\"status\":201}"; preg_match('~\\"status\\"\\s*:\\s*(\\d{3})~', $text, $m); echo $m[1] ?? 'Not found';` | `201` |
| 554. Extract a request timeout in milliseconds | `~\btimeout_ms=(\d+)\b~` | `$text = "timeout_ms=2500"; preg_match('~\\btimeout_ms=(\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2500` |
| 555. Validate a small CORS allow-origin hostname | `~^https://(?:[a-z0-9-]+\.)+[a-z]{2,}$~i` | `$text = "https://app.example.org"; echo preg_match('~^https://(?:[a-z0-9-]+\\.)+[a-z]{2,}$~i', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 556. Extract a MIME type from a header | `~\b([a-z]+/[a-z0-9.+-]+)\b~i` | `$text = "Content-Type: image/webp"; preg_match('~\\b([a-z]+/[a-z0-9.+-]+)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `image/webp` |
| 557. Find an Accept-Language primary tag | `~\bAccept-Language:\s*([a-z]{2})\b~i` | `$text = "Accept-Language: en-US,en;q=0.9"; preg_match('~\\bAccept-Language:\\s*([a-z]{2})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `en` |
| 558. Extract the value of X-Request-ID | `~^X-Request-ID:\s*([A-Za-z0-9-]+)$~im` | `$text = "X-Request-ID: req-18b9"; preg_match('~^X-Request-ID:\\s*([A-Za-z0-9-]+)$~im', $text, $m); echo $m[1] ?? 'Not found';` | `req-18b9` |
| 559. Find a Set-Cookie name | `~^Set-Cookie:\s*([A-Za-z_][A-Za-z0-9_-]*)=~im` | `$text = "Set-Cookie: session_id=abc123; Secure"; preg_match('~^Set-Cookie:\\s*([A-Za-z_][A-Za-z0-9_-]*)=~im', $text, $m); echo $m[1] ?? 'Not found';` | `session_id` |
| 560. Extract a max-age cache value | `~\bmax-age=(\d+)\b~` | `$text = "Cache-Control: public, max-age=3600"; preg_match('~\\bmax-age=(\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `3600` |
| 561. Find a retry-after duration | `~^Retry-After:\s*(\d+)\s*$~im` | `$text = "Retry-After: 120"; preg_match('~^Retry-After:\\s*(\\d+)\\s*$~im', $text, $m); echo $m[1] ?? 'Not found';` | `120` |
| 562. Extract a request body length | `~^Content-Length:\s*(\d+)\s*$~im` | `$text = "Content-Length: 1024"; preg_match('~^Content-Length:\\s*(\\d+)\\s*$~im', $text, $m); echo $m[1] ?? 'Not found';` | `1024` |
| 563. Validate a simple API version string | `~^v[1-9]\d*(?:\.\d+)?$~` | `$text = "v2.1"; echo preg_match('~^v[1-9]\\d*(?:\\.\\d+)?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 564. Extract a cursor from a paginated API link | `~[?&]cursor=([A-Za-z0-9_-]+)(?:&\|$)~` | `$text = "?limit=20&cursor=abcDEF_49"; preg_match('~[?&]cursor=([A-Za-z0-9_-]+)(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `abcDEF_49` |
| 565. Find an ETag header value | `~^ETag:\s*\"([A-Fa-f0-9]{8,64})\"~im` | `$text = "ETag: \"e9e0ad44\""; preg_match('~^ETag:\\s*\\"([A-Fa-f0-9]{8,64})\\"~im', $text, $m); echo $m[1] ?? 'Not found';` | `e9e0ad44` |
| 566. Detect gzip content encoding | `~^Content-Encoding:\s*gzip\b~im` | `$text = "Content-Encoding: gzip"; preg_match('~^Content-Encoding:\\s*gzip\\b~im', $text, $m); echo $m[0] ?? 'Not found';` | `Content-Encoding: gzip` |
| 567. Extract a localhost development port | `~\blocalhost:(\d{2,5})\b~` | `$text = "http://localhost:3000/api"; preg_match('~\\blocalhost:(\\d{2,5})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `3000` |
| 568. Find a JWT-shaped access token (shape only) | `~\b[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+\b~` | `$text = "token eyJhbGci.eyJzdWI.signature"; preg_match('~\\b[A-Za-z0-9_-]+\\.[A-Za-z0-9_-]+\\.[A-Za-z0-9_-]+\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `eyJhbGci.eyJzdWI.signature` |
| 569. Extract an API error identifier | `~\"error\"\s*:\s*\"([A-Z_]+)\"~` | `$text = "{\"error\":\"RATE_LIMITED\"}"; preg_match('~\\"error\\"\\s*:\\s*\\"([A-Z_]+)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `RATE_LIMITED` |
| 570. Extract a pagination limit parameter | `~[?&]limit=(\d{1,3})(?:&\|$)~` | `$text = "?limit=50&page=1"; preg_match('~[?&]limit=(\\d{1,3})(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `50` |
| 571. Find response headers beginning with X- | `~\bX-[A-Za-z-]+(?=:)~` | `$text = "X-Cache: HIT; X-Frame-Options: DENY"; preg_match_all('~\\bX-[A-Za-z-]+(?=:)~', $text, $m); echo implode(', ', $m[0]);` | `X-Cache, X-Frame-Options` |

## 14. Imports, CSV and delimited data

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 572. Split a simple comma-separated list (not quoted CSV) | `~\s*,\s*~` | `$text = "red, green,blue"; echo implode(' \| ', preg_split('~\\s*,\\s*~', $text));` | `red \| green \| blue` |
| 573. Split a simple semicolon-delimited row | `~\s*;\s*~` | `$text = "name; age ; city"; echo implode(' \| ', preg_split('~\\s*;\\s*~', $text));` | `name \| age \| city` |
| 574. Split a tab-separated record | `~\t+~` | `$text = "A\tB\tC"; echo implode(' \| ', preg_split('~\\t+~', $text));` | `A \| B \| C` |
| 575. Extract a date from a simple CSV row | `~\b20\d{2}-\d{2}-\d{2}\b~` | `$text = "104,2026-11-11,approved"; preg_match('~\\b20\\d{2}-\\d{2}-\\d{2}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `2026-11-11` |
| 576. Extract all numeric cells from a simple data row | `~(?<!\w)\d+(?:\.\d+)?(?!\w)~` | `$text = "3,12.50,0,98"; preg_match_all('~(?<!\\w)\\d+(?:\\.\\d+)?(?!\\w)~', $text, $m); echo implode(', ', $m[0]);` | `3, 12.50, 0, 98` |
| 577. Find a row's leading numeric ID | `~^(\d+)[,;]~` | `$text = "2941,Jane,active"; preg_match('~^(\\d+)[,;]~', $text, $m); echo $m[1] ?? 'Not found';` | `2941` |
| 578. Extract a trailing status field from a CSV-style row | `~,(active\|pending\|disabled)$~` | `$text = "52,Henry,pending"; preg_match('~,(active\|pending\|disabled)$~', $text, $m); echo $m[1] ?? 'Not found';` | `pending` |
| 579. Find duplicate commas indicating empty cells | `~,,~` | `$text = "Alice,,Active"; preg_match('~,,~', $text, $m); echo $m[0] ?? 'Not found';` | `,,` |
| 580. Replace semicolons with commas in a simple export | `~;~` | `$text = "one;two;three"; echo preg_replace('~;~', ',', $text);` | `one,two,three` |
| 581. Remove thousands separators from a copied numeric field | `~(?<=\d),(?=\d{3}(?:\D\|$))~` | `$text = "1,250,000"; echo preg_replace('~(?<=\\d),(?=\\d{3}(?:\\D\|$))~', '', $text);` | `1250000` |
| 582. Validate a three-column numeric row | `~^\d+,\d+,\d+$~` | `$text = "12,25,37"; echo preg_match('~^\\d+,\\d+,\\d+$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 583. Find all quoted cells in a simple CSV excerpt | `~\"(?:[^\"]\|\"\")*\"~` | `$text = "\"Alice\",\"New York\",\"Hi\""; preg_match_all('~\\"(?:[^\\"]\|\\"\\")*\\"~', $text, $m); echo implode(', ', $m[0]);` | `"Alice", "New York", "Hi"` |
| 584. Extract a value wrapped in double quotes | `~^\"([^\"]+)\"$~` | `$text = "\"Sample Item\""; preg_match('~^\\"([^\\"]+)\\"$~', $text, $m); echo $m[1] ?? 'Not found';` | `Sample Item` |
| 585. Find the first nonempty line's ID | `~(?m)^([1-9]\d*),[^\r\n]+~` | `$text = "24,Alice,active\n25,Bob,active"; preg_match('~(?m)^([1-9]\\d*),[^\\r\\n]+~', $text, $m); echo $m[1] ?? 'Not found';` | `24` |
| 586. Extract a key from a key=value export | `~^([A-Z_][A-Z0-9_]*)=~` | `$text = "MAX_RETRIES=5"; preg_match('~^([A-Z_][A-Z0-9_]*)=~', $text, $m); echo $m[1] ?? 'Not found';` | `MAX_RETRIES` |
| 587. Extract a value from a key=value export | `~^[A-Z_][A-Z0-9_]*=(.+)$~` | `$text = "MAX_RETRIES=5"; preg_match('~^[A-Z_][A-Z0-9_]*=(.+)$~', $text, $m); echo $m[1] ?? 'Not found';` | `5` |
| 588. Find integers within a pipe-delimited line | `~(?<!\w)\d+(?!\w)~` | `$text = "12\|42\|64"; preg_match_all('~(?<!\\w)\\d+(?!\\w)~', $text, $m); echo implode(', ', $m[0]);` | `12, 42, 64` |
| 589. Split simple pipe-delimited records | `~[\|]~` | `$text = "alpha\|beta\|gamma"; echo implode(' \| ', preg_split('~[\|]~', $text));` | `alpha \| beta \| gamma` |
| 590. Find a valid ISO-like header name | `~\b[A-Za-z][A-Za-z_]*(?=,)~` | `$text = "customer_id,amount,status"; preg_match('~\\b[A-Za-z][A-Za-z_]*(?=,)~', $text, $m); echo $m[0] ?? 'Not found';` | `customer_id` |
| 591. Validate a four-digit import year column | `~^(?:19\|20)\d{2}$~` | `$text = "2026"; echo preg_match('~^(?:19\|20)\\d{2}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 592. Find database-style NULL placeholders | `~\b(?:NULL\|N/A\|NA)\b~` | `$text = "NULL,51,N/A"; preg_match_all('~\\b(?:NULL\|N/A\|NA)\\b~', $text, $m); echo implode(', ', $m[0]);` | `NULL, N/A` |
| 593. Replace textual NULL values with an empty field | `~\bNULL\b~` | `$text = "Alice,NULL,active"; echo preg_replace('~\\bNULL\\b~', '', $text);` | `Alice,,active` |
| 594. Extract the extension from an import filename | `~\.([a-z]{2,5})$~i` | `$text = "customer-list.csv"; preg_match('~\\.([a-z]{2,5})$~i', $text, $m); echo $m[1] ?? 'Not found';` | `csv` |
| 595. Detect a UTF-8 BOM before CSV headers | `~^\x{FEFF}~u` | `$text = "﻿id,name,email"; preg_match('~^\\x{FEFF}~u', $text, $m); echo $m[0] ?? 'Not found';` | `﻿` |
| 596. Split a numeric range written as 10..20 | `~\.\.~` | `$text = "10..20"; echo implode(' \| ', preg_split('~\\.\\.~', $text));` | `10 \| 20` |

## 15. Markdown and publishing content

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 597. Extract headings from a Markdown article | `~^#{1,6}\s+.+$~m` | `$text = "# Start\nText\n## Details"; preg_match_all('~^#{1,6}\\s+.+$~m', $text, $m); echo implode(', ', $m[0]);` | `# Start, ## Details` |
| 598. Extract the title from the first Markdown H1 | `~^#\s+(.+)$~m` | `$text = "# Getting Started"; preg_match('~^#\\s+(.+)$~m', $text, $m); echo $m[1] ?? 'Not found';` | `Getting Started` |
| 599. Find Markdown task-list items | `~^\s*-\s+\[[ xX]\]\s+.+$~m` | `$text = "- [x] Done\n- [ ] Todo"; preg_match_all('~^\\s*-\\s+\\[[ xX]\\]\\s+.+$~m', $text, $m); echo implode(', ', $m[0]);` | `- [x] Done, - [ ] Todo` |
| 600. Find unchecked tasks in a Markdown note | `~^-\s+\[ \]\s+.+$~m` | `$text = "- [ ] Call client\n- [x] Sent mail"; preg_match_all('~^-\\s+\\[ \\]\\s+.+$~m', $text, $m); echo implode(', ', $m[0]);` | `- [ ] Call client` |
| 601. Extract a simple Markdown link label | `~\[([^\]]+)\]\(https?://[^)\s]+\)~` | `$text = "Read [Documentation](https://docs.example.org)"; preg_match('~\\[([^\\]]+)\\]\\(https?://[^)\\s]+\\)~', $text, $m); echo $m[1] ?? 'Not found';` | `Documentation` |
| 602. Extract a URL from a simple Markdown link | `~\[([^\]]+)\]\((https?://[^)\s]+)\)~` | `$text = "[Home](https://example.com)"; preg_match('~\\[([^\\]]+)\\]\\((https?://[^)\\s]+)\\)~', $text, $m); echo $m[2] ?? 'Not found';` | `https://example.com` |
| 603. Find inline code surrounded by single backticks | `~(?<!\x60)\x60[^\x60\r\n]+\x60(?!\x60)~` | ``$text = "Use `echo` and `preg_match`"; preg_match_all('~(?<!\\x60)\\x60[^\\x60\\r\\n]+\\x60(?!\\x60)~', $text, $m); echo implode(', ', $m[0]);`` | `` `echo`, `preg_match` `` |
| 604. Find bold Markdown phrases using double asterisks | `~\*\*[^*\r\n]+\*\*~` | `$text = "A **quick** and **clean** fix"; preg_match_all('~\\*\\*[^*\\r\\n]+\\*\\*~', $text, $m); echo implode(', ', $m[0]);` | `**quick**, **clean**` |
| 605. Extract a fenced code block language | `~^\x60{3}([A-Za-z0-9_-]+)\s*$~m` | ````$text = "```php\n<?php echo 1;\n```"; preg_match('~^\\x60{3}([A-Za-z0-9_-]+)\\s*$~m', $text, $m); echo $m[1] ?? 'Not found';```` | `php` |
| 606. Find images referenced in Markdown | `~!\[[^\]]*]\([^)]+\)~` | `$text = "![Logo](logo.png) ![Icon](icon.svg)"; preg_match_all('~!\\[[^\\]]*]\\([^)]+\\)~', $text, $m); echo implode(', ', $m[0]);` | `![Logo](logo.png), ![Icon](icon.svg)` |
| 607. Extract image alt text from Markdown | `~!\[([^\]]+)]\([^)]+\)~` | `$text = "![Sunset over lake](lake.jpg)"; preg_match('~!\\[([^\\]]+)]\\([^)]+\\)~', $text, $m); echo $m[1] ?? 'Not found';` | `Sunset over lake` |
| 608. Remove an empty Markdown link placeholder | `~\[\]\(\)\s*~` | `$text = "Visit []() later"; echo preg_replace('~\\[\\]\\(\\)\\s*~', '', $text);` | `Visit later` |
| 609. Find horizontal rules made of three or more hyphens | `~^-{3,}\s*$~m` | `$text = "Intro\n---\nMore"; preg_match('~^-{3,}\\s*$~m', $text, $m); echo $m[0] ?? 'Not found';` | `---` |
| 610. Extract a footnote reference identifier | `~\[\^([A-Za-z0-9_-]+)]~` | `$text = "More details[^sources]"; preg_match('~\\[\\^([A-Za-z0-9_-]+)]~', $text, $m); echo $m[1] ?? 'Not found';` | `sources` |
| 611. Find Markdown table alignment markers | `~:?-{3,}:?~` | `$text = "\|:---\|---:\|:---:\|"; preg_match_all('~:?-{3,}:?~', $text, $m); echo implode(', ', $m[0]);` | `:---, ---:, :---:` |
| 612. Extract a numbered list item body | `~^\d+\.\s+(.+)$~m` | `$text = "1. Install dependencies"; preg_match('~^\\d+\\.\\s+(.+)$~m', $text, $m); echo $m[1] ?? 'Not found';` | `Install dependencies` |
| 613. Remove a leading blockquote marker | `~^>\s?~m` | `$text = "> Important notice"; echo preg_replace('~^>\\s?~m', '', $text);` | `Important notice` |
| 614. Find wiki-style internal links | `~\[\[[^\]\r\n]+]]~` | `$text = "See [[Project Plan]] and [[Roadmap]]"; preg_match_all('~\\[\\[[^\\]\\r\\n]+]]~', $text, $m); echo implode(', ', $m[0]);` | `[[Project Plan]], [[Roadmap]]` |
| 615. Extract a simple URL inside angle brackets | `~<(https?://[^>\s]+)>~` | `$text = "Read <https://example.org/help>"; preg_match('~<(https?://[^>\\s]+)>~', $text, $m); echo $m[1] ?? 'Not found';` | `https://example.org/help` |
| 616. Find link-reference definitions | `~^\[[a-z0-9_-]+]:\s+https?://\S+$~im` | `$text = "[docs]: https://docs.example.org"; preg_match_all('~^\\[[a-z0-9_-]+]:\\s+https?://\\S+$~im', $text, $m); echo implode(', ', $m[0]);` | `[docs]: https://docs.example.org` |
| 617. Remove trailing spaces from Markdown lines | `~[ \t]+$~m` | `$text = "Line with spaces   "; echo preg_replace('~[ \\t]+$~m', '', $text);` | `Line with spaces` |
| 618. Extract a Markdown heading's hash level | `~^(#{1,6})\s+.+$~m` | `$text = "### Installation"; preg_match('~^(#{1,6})\\s+.+$~m', $text, $m); echo $m[1] ?? 'Not found';` | `###` |
| 619. Find strikethrough text written with tildes | `~\x7E\x7E[^\x7E\r\n]+\x7E\x7E~` | `$text = "We ~~cancelled~~ postponed"; preg_match('~\\x7E\\x7E[^\\x7E\\r\\n]+\\x7E\\x7E~', $text, $m); echo $m[0] ?? 'Not found';` | `~~cancelled~~` |
| 620. Find inline arithmetic surrounded by dollar signs | `~\$(?!\s)[^$\r\n]+\$~` | `$text = "Formula: \$a+b\$ here"; preg_match('~\\$(?!\\s)[^$\\r\\n]+\\$~', $text, $m); echo $m[0] ?? 'Not found';` | `$a+b$` |
| 621. Validate a simple Markdown document anchor | `~^[a-z0-9]+(?:-[a-z0-9]+)*$~` | `$text = "installation-guide"; echo preg_match('~^[a-z0-9]+(?:-[a-z0-9]+)*$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |

## 16. Email messages and support workflows

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 622. Extract an email subject from a header block | `~^Subject:\s*([^\r\n]+)$~im` | `$text = "Subject: Your order shipped"; preg_match('~^Subject:\\s*([^\\r\\n]+)$~im', $text, $m); echo $m[1] ?? 'Not found';` | `Your order shipped` |
| 623. Extract a From email from a mail header | `~^From:\s*([A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,})~im` | `$text = "From: support@example.com"; preg_match('~^From:\\s*([A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,})~im', $text, $m); echo $m[1] ?? 'Not found';` | `support@example.com` |
| 624. Extract a ticket number from an email subject | `~\[#(\d{4,8})\]~` | `$text = "[#10482] Password reset"; preg_match('~\\[#(\\d{4,8})\\]~', $text, $m); echo $m[1] ?? 'Not found';` | `10482` |
| 625. Find all email addresses in a support thread | `~[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}~` | `$text = "Reply to a@example.net and b@example.org"; preg_match_all('~[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}~', $text, $m); echo implode(', ', $m[0]);` | `a@example.net, b@example.org` |
| 626. Remove a Reply: subject prefix | `~^(?:Re:\s*)+~i` | `$text = "Re: Re: Meeting agenda"; echo preg_replace('~^(?:Re:\\s*)+~i', '', $text);` | `Meeting agenda` |
| 627. Remove a Forward: subject prefix | `~^(?:Fwd?:\s*)+~i` | `$text = "Fwd: Fwd: Contract"; echo preg_replace('~^(?:Fwd?:\\s*)+~i', '', $text);` | `Contract` |
| 628. Detect a no-reply address in a sender field | `~\bno-?reply@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b~i` | `$text = "Sender: noreply@example.com"; preg_match('~\\bno-?reply@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `noreply@example.com` |
| 629. Extract a shipment number from an order email | `~\bshipment\s*#\s*(\d{5,10})\b~i` | `$text = "Shipment # 204891"; preg_match('~\\bshipment\\s*#\\s*(\\d{5,10})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `204891` |
| 630. Find a customer-support case ID | `~\bSUP-\d{7}\b~` | `$text = "SUP-0042015 is pending"; preg_match('~\\bSUP-\\d{7}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `SUP-0042015` |
| 631. Extract a quoted reply after On ... wrote: | `~^On\s+(.+?)\s+wrote:$~m` | `$text = "On Tue at 10:00 wrote:"; preg_match('~^On\\s+(.+?)\\s+wrote:$~m', $text, $m); echo $m[1] ?? 'Not found';` | `Tue at 10:00` |
| 632. Find a message signature delimiter | `~^--\s*$~m` | `$text = "Thanks\n--\nSupport Team"; preg_match('~^--\\s*$~m', $text, $m); echo $m[0] ?? 'Not found';` | `--` |
| 633. Extract a message priority header | `~^X-Priority:\s*([1-5])\b~im` | `$text = "X-Priority: 1"; preg_match('~^X-Priority:\\s*([1-5])\\b~im', $text, $m); echo $m[1] ?? 'Not found';` | `1` |
| 634. Find an unsubscribe URL | `~https://[^\s<>]+/unsubscribe(?:\?[^\s<>]+)?~i` | `$text = "https://mail.example.org/unsubscribe?token=abc"; preg_match('~https://[^\\s<>]+/unsubscribe(?:\\?[^\\s<>]+)?~i', $text, $m); echo $m[0] ?? 'Not found';` | `https://mail.example.org/unsubscribe?token=abc` |
| 635. Find a case-insensitive spam phrase in a subject | `~\bfree\s+gift\b~i` | `$text = "A FREE GIFT for you"; preg_match('~\\bfree\\s+gift\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `FREE GIFT` |
| 636. Extract a verification link token (simple shape) | `~[?&]token=([A-Za-z0-9_-]{8,64})(?:&\|$)~` | `$text = "/verify?token=cE90zKqR5D1"; preg_match('~[?&]token=([A-Za-z0-9_-]{8,64})(?:&\|$)~', $text, $m); echo $m[1] ?? 'Not found';` | `cE90zKqR5D1` |
| 637. Find all reference numbers in a mail message | `~\bREF-[A-Z0-9]{6,10}\b~` | `$text = "REF-A013N9 REF-C31V82"; preg_match_all('~\\bREF-[A-Z0-9]{6,10}\\b~', $text, $m); echo implode(', ', $m[0]);` | `REF-A013N9, REF-C31V82` |
| 638. Extract a confirmation number from an email | `~\bconfirmation:\s*([A-Z0-9]{8})\b~i` | `$text = "Confirmation: A8273XZ9"; preg_match('~\\bconfirmation:\\s*([A-Z0-9]{8})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `A8273XZ9` |
| 639. Extract a complaint category from a subject | `~^\[(Billing\|Technical\|Shipping)\]~i` | `$text = "[Billing] Refund request"; preg_match('~^\\[(Billing\|Technical\|Shipping)\\]~i', $text, $m); echo $m[1] ?? 'Not found';` | `Billing` |
| 640. Detect a mailing-list footer line | `~\bunsubscribe\s+from\s+this\s+list\b~i` | `$text = "Unsubscribe from this list"; preg_match('~\\bunsubscribe\\s+from\\s+this\\s+list\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `Unsubscribe from this list` |
| 641. Extract an order number from an email subject | `~\bOrder\s*#\s*(\d{5,9})\b~i` | `$text = "Order # 209813 received"; preg_match('~\\bOrder\\s*#\\s*(\\d{5,9})\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `209813` |
| 642. Find a forwarded-message divider | `~^-{3,}\s*Forwarded message\s*-{3,}$~im` | `$text = "---- Forwarded message ----"; preg_match('~^-{3,}\\s*Forwarded message\\s*-{3,}$~im', $text, $m); echo $m[0] ?? 'Not found';` | `---- Forwarded message ----` |
| 643. Extract the top-level suffix from a sender address | `~@[A-Za-z0-9.-]+\.([A-Za-z]{2,})$~` | `$text = "agent@example.org"; preg_match('~@[A-Za-z0-9.-]+\\.([A-Za-z]{2,})$~', $text, $m); echo $m[1] ?? 'Not found';` | `org` |
| 644. Find a support SLA value in hours | `~\bSLA:\s*(\d+)\s*hours?\b~i` | `$text = "SLA: 24 hours"; preg_match('~\\bSLA:\\s*(\\d+)\\s*hours?\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `24` |
| 645. Extract an email message ID from a header | `~^Message-ID:\s*<([^<>\r\n]+)>~im` | `$text = "Message-ID: <m_294@example.org>"; preg_match('~^Message-ID:\\s*<([^<>\\r\\n]+)>~im', $text, $m); echo $m[1] ?? 'Not found';` | `m_294@example.org` |
| 646. Remove an [EXTERNAL] label from a mail subject | `~^\[EXTERNAL\]\s*~i` | `$text = "[EXTERNAL] Project update"; echo preg_replace('~^\\[EXTERNAL\\]\\s*~i', '', $text);` | `Project update` |

## 17. Known HTML and CSS fragments

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 647. Extract a title from a simple generated title tag | `~<title>([^<]*)</title>~i` | `$text = "<title>Contact us</title>"; preg_match('~<title>([^<]*)</title>~i', $text, $m); echo $m[1] ?? 'Not found';` | `Contact us` |
| 648. Find a class name in a controlled HTML fragment | `~\bclass=\"([A-Za-z0-9 _-]+)\"~` | `$text = "class=\"card active\""; preg_match('~\\bclass=\\"([A-Za-z0-9 _-]+)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `card active` |
| 649. Extract a static alt attribute value | `~\balt=\"([^\"]*)\"~i` | `$text = "alt=\"Sunny day\""; preg_match('~\\balt=\\"([^\\"]*)\\"~i', $text, $m); echo $m[1] ?? 'Not found';` | `Sunny day` |
| 650. Extract a basic button label in a fixed template | `~<button\b[^>]*>([^<]+)</button>~i` | `$text = "<button>Save changes</button>"; preg_match('~<button\\b[^>]*>([^<]+)</button>~i', $text, $m); echo $m[1] ?? 'Not found';` | `Save changes` |
| 651. Find an ID attribute in generated markup | `~\bid=\"([A-Za-z][A-Za-z0-9_-]*)\"~` | `$text = "id=\"submit-order\""; preg_match('~\\bid=\\"([A-Za-z][A-Za-z0-9_-]*)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `submit-order` |
| 652. Extract the input name from a known form tag | `~<input\b[^>]*\bname=\"([A-Za-z_][A-Za-z0-9_]*)\"~i` | `$text = "<input name=\"email\" type=\"text\">"; preg_match('~<input\\b[^>]*\\bname=\\"([A-Za-z_][A-Za-z0-9_]*)\\"~i', $text, $m); echo $m[1] ?? 'Not found';` | `email` |
| 653. Find a CSS custom property name | `~--[a-z][a-z0-9-]*\b~` | `$text = "--card-background: #fff;"; preg_match('~--[a-z][a-z0-9-]*\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `--card-background` |
| 654. Extract a CSS hex color value | `~#[0-9a-fA-F]{6}\b~` | `$text = "background: #2D7AC8;"; preg_match('~#[0-9a-fA-F]{6}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `#2D7AC8` |
| 655. Extract a CSS pixel size | `~\b\d+(?:\.\d+)?px\b~` | `$text = "padding: 16px;"; preg_match('~\\b\\d+(?:\\.\\d+)?px\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `16px` |
| 656. Extract a CSS rem value | `~\b\d+(?:\.\d+)?rem\b~` | `$text = "font-size: 1.25rem;"; preg_match('~\\b\\d+(?:\\.\\d+)?rem\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `1.25rem` |
| 657. Find a CSS selector's class name | `~\.([a-z][a-z0-9_-]*)\s*\{~` | `$text = ".primary-button { color: red; }"; preg_match('~\\.([a-z][a-z0-9_-]*)\\s*\\{~', $text, $m); echo $m[1] ?? 'Not found';` | `primary-button` |
| 658. Extract an RGB color value | `~rgb\(\s*\d{1,3}\s*,\s*\d{1,3}\s*,\s*\d{1,3}\s*\)~i` | `$text = "color: rgb(20, 40, 60)"; preg_match('~rgb\\(\\s*\\d{1,3}\\s*,\\s*\\d{1,3}\\s*,\\s*\\d{1,3}\\s*\\)~i', $text, $m); echo $m[0] ?? 'Not found';` | `rgb(20, 40, 60)` |
| 659. Find a media-query breakpoint | `~min-width:\s*(\d+)px~i` | `$text = "@media (min-width: 768px)"; preg_match('~min-width:\\s*(\\d+)px~i', $text, $m); echo $m[1] ?? 'Not found';` | `768` |
| 660. Extract a transition duration in milliseconds | `~transition:\s*[^;]*?\b(\d+)ms\b~` | `$text = "transition: color 250ms ease"; preg_match('~transition:\\s*[^;]*?\\b(\\d+)ms\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `250` |
| 661. Find a data-attribute key on a known element | `~\bdata-([a-z][a-z0-9-]*)=\"~` | `$text = "data-product-id=\"501\""; preg_match('~\\bdata-([a-z][a-z0-9-]*)=\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `product-id` |
| 662. Extract a static href attribute | `~\bhref=\"([^\"]+)\"~` | `$text = "href=\"/about\""; preg_match('~\\bhref=\\"([^\\"]+)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `/about` |
| 663. Extract a static image source attribute | `~\bsrc=\"([^\"]+\.(?:png\|jpg\|webp))\"~i` | `$text = "src=\"/img/banner.webp\""; preg_match('~\\bsrc=\\"([^\\"]+\\.(?:png\|jpg\|webp))\\"~i', $text, $m); echo $m[1] ?? 'Not found';` | `/img/banner.webp` |
| 664. Find a CSS z-index declaration | `~\bz-index:\s*(\d+)\b~` | `$text = "z-index: 1000;"; preg_match('~\\bz-index:\\s*(\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `1000` |
| 665. Extract a simple font-weight number | `~font-weight:\s*([1-9]00)\b~` | `$text = "font-weight: 600"; preg_match('~font-weight:\\s*([1-9]00)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `600` |
| 666. Find a viewport width from a simple meta value | `~width=device-width~` | `$text = "content=\"width=device-width,initial-scale=1\""; preg_match('~width=device-width~', $text, $m); echo $m[0] ?? 'Not found';` | `width=device-width` |
| 667. Extract a controlled HTML lang attribute | `~\blang=\"([a-z]{2}(?:-[A-Z]{2})?)\"~` | `$text = "lang=\"en-GB\""; preg_match('~\\blang=\\"([a-z]{2}(?:-[A-Z]{2})?)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `en-GB` |
| 668. Find a CSS percentage width | `~width:\s*\d+(?:\.\d+)?%~` | `$text = "width: 75%"; preg_match('~width:\\s*\\d+(?:\\.\\d+)?%~', $text, $m); echo $m[0] ?? 'Not found';` | `width: 75%` |
| 669. Extract a simple ARIA label | `~\baria-label=\"([^\"]+)\"~` | `$text = "aria-label=\"Close dialog\""; preg_match('~\\baria-label=\\"([^\\"]+)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `Close dialog` |
| 670. Find a CSS grid gap in pixels | `~\bgap:\s*(\d+)px\b~` | `$text = "gap: 12px"; preg_match('~\\bgap:\\s*(\\d+)px\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `12` |
| 671. Extract an HTML data-count value from a controlled component | `~\bdata-count=\"(\d+)\"~` | `$text = "data-count=\"37\""; preg_match('~\\bdata-count=\\"(\\d+)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `37` |

## 18. Unicode, languages and international text

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 672. Find Latin-alphabet words, including accented words | `~\b[\p{Latin}]+\b~u` | `$text = "Crème brûlée is tasty"; preg_match_all('~\\b[\\p{Latin}]+\\b~u', $text, $m); echo implode(', ', $m[0]);` | `Crème, brûlée, is, tasty` |
| 673. Extract a Greek word from a document | `~\p{Greek}+~u` | `$text = "Section Αθήνα"; preg_match('~\\p{Greek}+~u', $text, $m); echo $m[0] ?? 'Not found';` | `Αθήνα` |
| 674. Find a Cyrillic word in a sentence | `~\p{Cyrillic}+~u` | `$text = "Hello Привет world"; preg_match('~\\p{Cyrillic}+~u', $text, $m); echo $m[0] ?? 'Not found';` | `Привет` |
| 675. Find a sequence of Arabic letters | `~\p{Arabic}+~u` | `$text = "Welcome مرحبا"; preg_match('~\\p{Arabic}+~u', $text, $m); echo $m[0] ?? 'Not found';` | `مرحبا` |
| 676. Extract Japanese Hiragana from text | `~\p{Hiragana}+~u` | `$text = "Greeting こんにちは!"; preg_match('~\\p{Hiragana}+~u', $text, $m); echo $m[0] ?? 'Not found';` | `こんにちは` |
| 677. Extract Japanese Katakana from a label | `~\p{Katakana}+~u` | `$text = "Brand カメラ"; preg_match('~\\p{Katakana}+~u', $text, $m); echo $m[0] ?? 'Not found';` | `カメラ` |
| 678. Find Korean Hangul in a product name | `~\p{Hangul}+~u` | `$text = "Product 한글"; preg_match('~\\p{Hangul}+~u', $text, $m); echo $m[0] ?? 'Not found';` | `한글` |
| 679. Find a word containing Unicode letters | `~[\p{L}]{3,}~u` | `$text = "café"; preg_match('~[\\p{L}]{3,}~u', $text, $m); echo $m[0] ?? 'Not found';` | `café` |
| 680. Find all Unicode decimal digits in an input | `~\p{Nd}+~u` | `$text = "Count १२ and 42"; preg_match_all('~\\p{Nd}+~u', $text, $m); echo implode(', ', $m[0]);` | `१२, 42` |
| 681. Remove combining marks from an already-decomposed word | `~\p{M}+~u` | `$text = "Café"; echo preg_replace('~\\p{M}+~u', '', $text);` | `Cafe` |
| 682. Collapse Unicode whitespace in copied content | `~\p{Zs}+~u` | `$text = "a  b"; echo preg_replace('~\\p{Zs}+~u', ' ', $text);` | `a b` |
| 683. Find emoji faces in a notification | `~[\x{1F600}-\x{1F64F}]~u` | `$text = "Happy 😀 😎"; preg_match_all('~[\\x{1F600}-\\x{1F64F}]~u', $text, $m); echo implode(', ', $m[0]);` | `😀, 😎` |
| 684. Find arrows used as navigation markers | `~[\x{2190}-\x{21FF}]~u` | `$text = "← Back → Forward"; preg_match_all('~[\\x{2190}-\\x{21FF}]~u', $text, $m); echo implode(', ', $m[0]);` | `←, →` |
| 685. Remove zero-width spaces from pasted text | `~\x{200B}~u` | `$text = "co​operate"; echo preg_replace('~\\x{200B}~u', '', $text);` | `cooperate` |
| 686. Find a nonbreaking space in imported content | `~\x{00A0}~u` | `$text = "Hello world"; preg_match('~\\x{00A0}~u', $text, $m); echo bin2hex($m[0] ?? 'Not found');` | `c2a0` |
| 687. Extract a language tag from a translation key | `~\b([a-z]{2}-[A-Z]{2})\b~` | `$text = "Language en-GB"; preg_match('~\\b([a-z]{2}-[A-Z]{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `en-GB` |
| 688. Validate a BCP47-like language prefix | `~^[a-z]{2}(?:-[A-Z]{2})?$~` | `$text = "de-DE"; echo preg_match('~^[a-z]{2}(?:-[A-Z]{2})?$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 689. Find Arabic-Indic digits in a form field | `~[\x{0660}-\x{0669}]+~u` | `$text = "Page ١٢٣"; preg_match_all('~[\\x{0660}-\\x{0669}]+~u', $text, $m); echo implode(', ', $m[0]);` | `١٢٣` |
| 690. Find typographic curly apostrophes in copied text | `~[\x{2018}\x{2019}]~u` | `$text = "Don’t forget"; preg_match('~[\\x{2018}\\x{2019}]~u', $text, $m); echo $m[0] ?? 'Not found';` | `’` |
| 691. Replace curly double quotes with ordinary quotes | `~[\x{201C}\x{201D}]~u` | `$text = "“Hello”"; echo preg_replace('~[\\x{201C}\\x{201D}]~u', '"', $text);` | `"Hello"` |
| 692. Find em or en dashes in a sentence | `~[\x{2013}\x{2014}]~u` | `$text = "A–B - done"; preg_match_all('~[\\x{2013}\\x{2014}]~u', $text, $m); echo implode(', ', $m[0]);` | `–, -` |
| 693. Remove the Unicode replacement character | `~\x{FFFD}~u` | `$text = "Bad�text"; echo preg_replace('~\\x{FFFD}~u', '', $text);` | `Badtext` |
| 694. Find fullwidth Latin letters from imported text | `~[\x{FF21}-\x{FF3A}]+~u` | `$text = "Code ＡＢＣ"; preg_match('~[\\x{FF21}-\\x{FF3A}]+~u', $text, $m); echo $m[0] ?? 'Not found';` | `ＡＢＣ` |
| 695. Extract currency symbols from a document | `~\p{Sc}~u` | `$text = "Prices \$20 €15 £9"; preg_match_all('~\\p{Sc}~u', $text, $m); echo implode(', ', $m[0]);` | `$, €, £` |
| 696. Find superscript numerals in scientific content | `~[\x{00B2}\x{00B3}\x{2070}-\x{2079}]+~u` | `$text = "Area m²"; preg_match('~[\\x{00B2}\\x{00B3}\\x{2070}-\\x{2079}]+~u', $text, $m); echo $m[0] ?? 'Not found';` | `²` |

## 19. Servers, addresses and network configuration

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 697. Extract an IPv4 address from a server message (shape only) | `~\b(?:\d{1,3}\.){3}\d{1,3}\b~` | `$text = "Connected to 192.0.2.10"; preg_match('~\\b(?:\\d{1,3}\\.){3}\\d{1,3}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `192.0.2.10` |
| 698. Validate an IPv4 address with each octet 0–255 | `~^(?:(?:25[0-5]\|2[0-4]\d\|1\d{2}\|[1-9]?\d)\.){3}(?:25[0-5]\|2[0-4]\d\|1\d{2}\|[1-9]?\d)$~` | `$text = "198.51.100.42"; echo preg_match('~^(?:(?:25[0-5]\|2[0-4]\\d\|1\\d{2}\|[1-9]?\\d)\\.){3}(?:25[0-5]\|2[0-4]\\d\|1\\d{2}\|[1-9]?\\d)$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 699. Extract a URL port from a host:port pair | `~^[A-Za-z0-9.-]+:(\d{2,5})$~` | `$text = "api.example.net:8443"; preg_match('~^[A-Za-z0-9.-]+:(\\d{2,5})$~', $text, $m); echo $m[1] ?? 'Not found';` | `8443` |
| 700. Extract a hostname from a reverse-proxy setting | `~\bserver_name\s+([A-Za-z0-9.-]+);~` | `$text = "server_name docs.example.org;"; preg_match('~\\bserver_name\\s+([A-Za-z0-9.-]+);~', $text, $m); echo $m[1] ?? 'Not found';` | `docs.example.org` |
| 701. Find an Nginx listen port | `~\blisten\s+(\d{2,5})\s*;~` | `$text = "listen 443;"; preg_match('~\\blisten\\s+(\\d{2,5})\\s*;~', $text, $m); echo $m[1] ?? 'Not found';` | `443` |
| 702. Extract a PHP-FPM pool name from a section heading | `~^\[([a-z][a-z0-9_-]+)]$~m` | `$text = "[www]"; preg_match('~^\\[([a-z][a-z0-9_-]+)]$~m', $text, $m); echo $m[1] ?? 'Not found';` | `www` |
| 703. Extract a MariaDB port from a config assignment | `~\bport\s*=\s*(\d{2,5})\b~` | `$text = "port = 3306"; preg_match('~\\bport\\s*=\\s*(\\d{2,5})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `3306` |
| 704. Find an environment-style database name | `~\bDB_NAME=([a-z][a-z0-9_]*)\b~` | `$text = "DB_NAME=shop_main"; preg_match('~\\bDB_NAME=([a-z][a-z0-9_]*)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `shop_main` |
| 705. Find a version in a server banner | `~\bnginx/(\d+(?:\.\d+){1,3})\b~` | `$text = "Server: nginx/1.28.0"; preg_match('~\\bnginx/(\\d+(?:\\.\\d+){1,3})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `1.28.0` |
| 706. Extract a PHP version from a startup line | `~\bPHP\s+(\d+\.\d+\.\d+)\b~` | `$text = "PHP 8.5.12 started"; preg_match('~\\bPHP\\s+(\\d+\\.\\d+\\.\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `8.5.12` |
| 707. Find a CIDR prefix length in an address | `~\b(?:\d{1,3}\.){3}\d{1,3}/(\d{1,2})\b~` | `$text = "10.0.0.0/24"; preg_match('~\\b(?:\\d{1,3}\\.){3}\\d{1,3}/(\\d{1,2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `24` |
| 708. Extract a common service protocol from a URL | `~^(https?\|ftp\|ssh)://~i` | `$text = "ssh://server.example.net"; preg_match('~^(https?\|ftp\|ssh)://~i', $text, $m); echo $m[1] ?? 'Not found';` | `ssh` |
| 709. Find a MAC address in a device inventory | `~\b(?:[A-F0-9]{2}:){5}[A-F0-9]{2}\b~i` | `$text = "Device AA:BB:CC:DD:EE:FF"; preg_match('~\\b(?:[A-F0-9]{2}:){5}[A-F0-9]{2}\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `AA:BB:CC:DD:EE:FF` |
| 710. Validate a lowercase DNS hostname shape | `~^(?:[a-z0-9-]+\.)+[a-z]{2,}$~` | `$text = "api.example.org"; echo preg_match('~^(?:[a-z0-9-]+\\.)+[a-z]{2,}$~', $text) ? 'Valid' : 'Invalid';` | `Valid` |
| 711. Extract a database table name from a SQL log phrase | `~\btable=([a-z][a-z0-9_]*)\b~` | `$text = "table=customer_orders"; preg_match('~\\btable=([a-z][a-z0-9_]*)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `customer_orders` |
| 712. Find a TCP connection count in a metric line | `~\btcp_connections=(\d+)\b~` | `$text = "tcp_connections=89"; preg_match('~\\btcp_connections=(\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `89` |
| 713. Extract a disk usage percentage from status output | `~\bdisk:\s*(\d+(?:\.\d+)?)%~` | `$text = "disk: 73.2%"; preg_match('~\\bdisk:\\s*(\\d+(?:\\.\\d+)?)%~', $text, $m); echo $m[1] ?? 'Not found';` | `73.2` |
| 714. Find a process uptime expressed in days | `~\buptime:\s*(\d+)\s+days?\b~i` | `$text = "Uptime: 18 days"; preg_match('~\\buptime:\\s*(\\d+)\\s+days?\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `18` |
| 715. Extract a service name from systemctl output | `~\b([a-z0-9_.@-]+\.service)\b~` | `$text = "nginx.service loaded active"; preg_match('~\\b([a-z0-9_.@-]+\\.service)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `nginx.service` |
| 716. Find IPv6 loopback notation | `~(?<!:)(?<!\w)::1(?!\w)~` | `$text = "Listening on ::1"; preg_match('~(?<!:)(?<!\\w)::1(?!\\w)~', $text, $m); echo $m[0] ?? 'Not found';` | `::1` |
| 717. Extract a container image tag from a version label | `~\bimage:[a-z0-9_.-]+:([a-z0-9_.-]+)\b~` | `$text = "image:app-server:2.4.1"; preg_match('~\\bimage:[a-z0-9_.-]+:([a-z0-9_.-]+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2.4.1` |
| 718. Find a Redis endpoint in configuration | `~\bredis://[a-z0-9.-]+:\d+\b~i` | `$text = "redis://cache.example.net:6379"; preg_match('~\\bredis://[a-z0-9.-]+:\\d+\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `redis://cache.example.net:6379` |
| 719. Extract a retry interval from server configuration | `~\bretry_interval=(\d+)s\b~` | `$text = "retry_interval=30s"; preg_match('~\\bretry_interval=(\\d+)s\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `30` |
| 720. Find a certificate expiration date label | `~\bexpires=(\d{4}-\d{2}-\d{2})\b~` | `$text = "expires=2027-05-01"; preg_match('~\\bexpires=(\\d{4}-\\d{2}-\\d{2})\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `2027-05-01` |
| 721. Extract a command exit code from monitoring | `~\bexit_code=(-?\d+)\b~` | `$text = "exit_code=127"; preg_match('~\\bexit_code=(-?\\d+)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `127` |

## 20. Developer tools, code and configuration

| Objective | PHP regex | PHP example (input + usage) | Web output |
|---|---|---|---|
| 722. Extract a PHP function name from a declaration | `~\bfunction\s+([A-Za-z_][A-Za-z0-9_]*)\s*\(~` | `$text = "function buildReport(\$id) {"; preg_match('~\\bfunction\\s+([A-Za-z_][A-Za-z0-9_]*)\\s*\\(~', $text, $m); echo $m[1] ?? 'Not found';` | `buildReport` |
| 723. Find a PHP variable name in a snippet | `~\$[A-Za-z_][A-Za-z0-9_]*~` | `$text = "\$userName = 'Alice';"; preg_match('~\\$[A-Za-z_][A-Za-z0-9_]*~', $text, $m); echo $m[0] ?? 'Not found';` | `$userName` |
| 724. Extract a class name from a PHP declaration | `~\bclass\s+([A-Z][A-Za-z0-9_]*)\b~` | `$text = "final class UserService"; preg_match('~\\bclass\\s+([A-Z][A-Za-z0-9_]*)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `UserService` |
| 725. Find a PHP namespace declaration | `~\bnamespace\s+([A-Za-z_][A-Za-z0-9_\\]*);~` | `$text = "namespace App\\Services;"; preg_match('~\\bnamespace\\s+([A-Za-z_][A-Za-z0-9_\\\\]*);~', $text, $m); echo $m[1] ?? 'Not found';` | `App\Services` |
| 726. Find TODO annotations in comments | `~\bTODO:\s*[^;\r\n]+~i` | `$text = "// TODO: add tests"; preg_match_all('~\\bTODO:\\s*[^;\\r\\n]+~i', $text, $m); echo implode(', ', $m[0]);` | `TODO: add tests` |
| 727. Extract a Git commit short hash | `~\b[0-9a-f]{7,12}\b~` | `$text = "commit 8a4b2c1"; preg_match('~\\b[0-9a-f]{7,12}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `8a4b2c1` |
| 728. Find issue references in commit subjects | `~#[1-9]\d{0,6}\b~` | `$text = "Fix #240 and #241"; preg_match_all('~#[1-9]\\d{0,6}\\b~', $text, $m); echo implode(', ', $m[0]);` | `#240, #241` |
| 729. Extract a semantic version number | `~\b\d+\.\d+\.\d+(?:-(?:alpha\|beta\|rc)\.\d+)?\b~` | `$text = "Release 2.6.0-rc.1"; preg_match('~\\b\\d+\\.\\d+\\.\\d+(?:-(?:alpha\|beta\|rc)\\.\\d+)?\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `2.6.0-rc.1` |
| 730. Extract the branch name from a Git status message | `~\bOn branch ([a-z0-9/_-]+)\b~i` | `$text = "On branch feature/checkout"; preg_match('~\\bOn branch ([a-z0-9/_-]+)\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `feature/checkout` |
| 731. Find dependency version constraints | `~\^\d+\.\d+(?:\.\d+)?~` | `$text = "versions ^1.5.0 and ^2.4"; preg_match_all('~\\^\\d+\\.\\d+(?:\\.\\d+)?~', $text, $m); echo implode(', ', $m[0]);` | `^1.5.0, ^2.4` |
| 732. Extract an npm-style package name with a scope | `~@[a-z0-9_-]+/[a-z0-9_.-]+~` | `$text = "@acme/ui-components"; preg_match('~@[a-z0-9_-]+/[a-z0-9_.-]+~', $text, $m); echo $m[0] ?? 'Not found';` | `@acme/ui-components` |
| 733. Find an ENV constant in application source | `~\b[A-Z][A-Z0-9]*(?:_[A-Z0-9]+)+\b~` | `$text = "Use API_TIMEOUT_MS for requests"; preg_match('~\\b[A-Z][A-Z0-9]*(?:_[A-Z0-9]+)+\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `API_TIMEOUT_MS` |
| 734. Extract the value from a .env setting | `~^APP_ENV=(dev\|staging\|production)$~m` | `$text = "APP_ENV=staging"; preg_match('~^APP_ENV=(dev\|staging\|production)$~m', $text, $m); echo $m[1] ?? 'Not found';` | `staging` |
| 735. Find a Boolean configuration setting | `~\b(?:true\|false)\b~i` | `$text = "debug_mode = false"; preg_match('~\\b(?:true\|false)\\b~i', $text, $m); echo $m[0] ?? 'Not found';` | `false` |
| 736. Extract a configured maximum upload size | `~\bupload_max_filesize\s*=\s*(\d+[KMG])\b~i` | `$text = "upload_max_filesize = 16M"; preg_match('~\\bupload_max_filesize\\s*=\\s*(\\d+[KMG])\\b~i', $text, $m); echo $m[1] ?? 'Not found';` | `16M` |
| 737. Find a port mapping from a Docker Compose snippet | `~\b\d{2,5}:\d{2,5}\b~` | `$text = "\"8080:80\""; preg_match('~\\b\\d{2,5}:\\d{2,5}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `8080:80` |
| 738. Extract the version field from a package manifest fragment | `~\"version\"\s*:\s*\"(\d+\.\d+\.\d+)\"~` | `$text = "{\"version\":\"3.1.2\"}"; preg_match('~\\"version\\"\\s*:\\s*\\"(\\d+\\.\\d+\\.\\d+)\\"~', $text, $m); echo $m[1] ?? 'Not found';` | `3.1.2` |
| 739. Find hexadecimal color literals in source code | `~#[0-9a-fA-F]{6}\b~` | `$text = "const colors = ['#112233','#AABBCC']"; preg_match_all('~#[0-9a-fA-F]{6}\\b~', $text, $m); echo implode(', ', $m[0]);` | `#112233, #AABBCC` |
| 740. Extract a PHP require path from a simple call | `~\brequire_once\s+['\"]([^'\"]+)['\"]~` | `$text = "require_once 'config/init.php';"; preg_match('~\\brequire_once\\s+[\'\\"]([^\'\\"]+)[\'\\"]~', $text, $m); echo $m[1] ?? 'Not found';` | `config/init.php` |
| 741. Find a CSS selector ID in a stylesheet | `~#([a-z][a-z0-9_-]*)\s*\{~` | `$text = "#login-form { display: flex; }"; preg_match('~#([a-z][a-z0-9_-]*)\\s*\\{~', $text, $m); echo $m[1] ?? 'Not found';` | `login-form` |
| 742. Extract a CLI option name | `~--([a-z][a-z0-9-]*)\b~` | `$text = "Run with --dry-run"; preg_match('~--([a-z][a-z0-9-]*)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `dry-run` |
| 743. Find an IPv4 address in a sample dotenv value | `~\b(?:\d{1,3}\.){3}\d{1,3}\b~` | `$text = "BACKEND_HOST=127.0.0.1"; preg_match('~\\b(?:\\d{1,3}\\.){3}\\d{1,3}\\b~', $text, $m); echo $m[0] ?? 'Not found';` | `127.0.0.1` |
| 744. Extract a simple SQL parameter name | `~:([a-z][a-z0-9_]*)\b~` | `$text = "WHERE user_id = :user_id"; preg_match('~:([a-z][a-z0-9_]*)\\b~', $text, $m); echo $m[1] ?? 'Not found';` | `user_id` |
| 745. Find a shell-style variable placeholder | `~\$\{[A-Z_][A-Z0-9_]*}~` | `$text = "PATH=\${APP_ROOT}/bin"; preg_match('~\\$\\{[A-Z_][A-Z0-9_]*}~', $text, $m); echo $m[0] ?? 'Not found';` | `${APP_ROOT}` |
| 746. Extract a numeric migration version from filename | `~^(\d{14})_[a-z0-9_]+\.php$~` | `$text = "20261111084530_create_users.php"; preg_match('~^(\\d{14})_[a-z0-9_]+\\.php$~', $text, $m); echo $m[1] ?? 'Not found';` | `20261111084530` |
