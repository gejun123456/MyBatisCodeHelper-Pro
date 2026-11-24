# Format Mapper XML

As of 3.7.0, use the IDE's **Reformat Code** shortcut in the Mapper XML editor. The default is `Ctrl+Alt+L` on Windows and Linux or `⌥⌘L` on macOS. Check the IDE's Keymap for your configured shortcut.

| Scope | How to format |
| --- | --- |
| Current statement | Place the caret inside a `<select>`, `<insert>`, `<update>`, `<delete>`, or `<sql>` tag. Press the shortcut with no selection. |
| Selection | Select the text and press the shortcut. |
| Entire file | Move the caret outside the SQL statements and fragments, clear the selection, and press the shortcut. |

## Formatter settings

Under **Settings → MyBatisCodeHelperPro → Formatter**, select `Plugin formatter` or `No formatter`. The latter disables formatting for Mapper XML and its injected SQL fragments. Existing `IDEA default formatter` settings migrate to `No formatter` on upgrade. Select `Plugin formatter` to turn formatting back on.

This feature requires the IDE's Database Tools and SQL support. The formatter uses the Mapper file's configured SQL dialect when available, then falls back to the database type in the plugin settings and finally to the generic SQL dialect. [Configure the database and SQL dialect](configure.md)

## What formatting preserves

The plugin adjusts indentation, spacing, and line breaks around tags and SQL. It preserves dynamic tags, parameter expressions, string contents, comments, and existing SQL keyword case. It skips statements that could change meaning, such as those with arbitrary `${...}` substitution or string literals that span dynamic tags.
