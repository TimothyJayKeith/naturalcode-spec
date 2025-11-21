# naturalcode-spec
Defines the `.nc` (Natural Code) file type to be used in semantics based coding.

## Overview
A `.nc` file is a structured text document that contains:
1. **Semantics** — English descriptions of functions, scenes, assets, or behaviors
2. **Generated Code** — machine-generated source code in any supported language
3. **Metadata** — hashes, versions, timestamps, and generation details

## File Structure

A valid `.nc` file contains up to three top-level sections in this order

```
=== Semantics ===
... natural-language function or object definitions ...

=== Code (Python) ===
... executable code matched to semantics ...

=== Metadata ===
... machine-readable sync info ...
```

Each section is plain text and git friendly

## Semantics Section

The semantics block describes what the developer wants, using flexible English-style structure.

Example:

```
=== Semantics ===

define isPalindrome:
    Input - any string
    Output - True if the string reads the same forward and backward
    Special Notes - ignore spaces, punctuation, capitalization

define reverseString:
    Input - any string
    Output - the reversed version of that string
```

**Rules**
* Must start with === Semantics ===.
* Must contain at least one definition.
* A definition starts with define, def, function, object or class.
* Content must be natural-language based, not code-based.
* Comments begin with #.

## Code Section

The code block contains executable source code in the chosen language.

Example:

```
=== Code (Python) ===

def is_palindrome(s: str) -> bool:
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return cleaned == cleaned[::-1]

def reverse_string(s: str) -> str:
    return s[::-1]
```

**Rules**

* Must declare the language in parentheses (e.g., Python, JavaScript, GDScript).
* The code may be user-edited; NaturalCode will detect changes using hashes.
* Missing functions will be automatically generated when needed.

## Metadata Section
Metadata ensures synchronization between the semantic block and code block.

Example:

```
=== Metadata ===
version: 0.1
language: Python
generated_at: 2025-11-21T04:12:22Z
semantic_hash: "2ab3c288fe"
code_hash: "fa339e01ba"
model: "gpt-4o-mini"
```

**Required Keys**
| Key             | Description                        |
| --------------- | ---------------------------------- |
| `version`       | `.nc` format version number        |
| `language`      | Programming language in Code block |
| `semantic_hash` | Hash of the semantics block        |
| `code_hash`     | Hash of the code block             |
| `generated_at`  | Timestamp of last generation       |

**Optional Keys**
* `warnings`
* `require_regeneration`
* `assets`
* `notes`
* `model`
* `user_edits`

## Contributing
Issues, pull requests, and discussions are welcome.
NaturalCode’s .nc format is intended to become an open standard for semantic programming.
