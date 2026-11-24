# Mapper XML 格式化

从 3.7.0 起，在 Mapper XML 编辑器中使用 IDE 的 **Reformat Code** 快捷键。默认是 Windows / Linux 的 `Ctrl+Alt+L` 和 macOS 的 `⌥⌘L`，实际按键以 IDE 的 Keymap 为准。

| 范围 | 操作 |
| --- | --- |
| 当前语句 | 将光标放在 `<select>`、`<insert>`、`<update>`、`<delete>` 或 `<sql>` 内，无选区时按快捷键。 |
| 选区 | 选中文本后按快捷键。 |
| 整个文件 | 将光标移到 SQL 语句和片段之外，取消选区后按快捷键。 |

## 格式化设置

在 **Settings → MyBatisCodeHelperPro → 格式化器** 中选择 `Plugin formatter` 或 `No formatter`。后者会关闭 Mapper XML 及其注入 SQL 片段的格式化。旧的 `IDEA default formatter` 设置升级时会自动迁移为 `No formatter`。如需恢复格式化，请选择 `Plugin formatter`。

此功能需要 IDE 的 Database Tools and SQL 支持。格式化器优先使用 Mapper 文件配置的 SQL 方言，其次使用插件中的数据库类型，最后使用通用 SQL 方言。[配置数据库与 SQL 方言](configure.md)

## 格式化保留的内容

插件整理 XML 标签和 SQL 的缩进、空格与换行，保留动态标签、参数表达式、字符串内容、注释及 SQL 关键字的原有大小写。遇到可能改变 SQL 含义的语句时会跳过，例如含有任意文本替换的 `${...}` 或跨动态标签拼接字符串的语句。
