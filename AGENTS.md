# AI Agent Documentation

This file (`AGENTS.md`) provides context for AI agents working on this repository.

## Structure & Style

* **Language**: Only **English**.
* **Logs**: Use specific verbs (`[HASHED]`, `[SIGNED]`, `[VERIFIED]`). Do not use `[OK]`.
* **Colors**:
  * Status/Action: Green/Red/Yellow (full line).
  * Paths/Files: Cyan (`\033[0;36m`) embedded.
* **Scripts**:
  * `hash_dictionary_audit.py`: Python 3.
* **Code Comments**: Exclusively in **English**. Concise, helpful, and following language Best Practices (PEP 8 for Python, Google Shell Style Guide).

## Project Context

Document integrity tools. Security and data consistency are critical.

* **Never** introduce unnecessary dependencies.
* **Never** modify cryptographic logic without exhaustive review.
