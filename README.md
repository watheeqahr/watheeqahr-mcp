# WatheeqaHR Attendance Analyzer — MCP server

A free, hosted [Model Context Protocol](https://modelcontextprotocol.io) server that lets AI assistants (Claude, ChatGPT, Cursor, VS Code and others) **analyze biometric attendance device exports** directly: ZKTeco / BioTime, Hikvision, Dahua, Anviz, Suprema BioStar, FingerTec, Matrix COSEC, eSSL and similar. It reads CSV, Excel or text files with English or Arabic headers.

For each employee it returns days present, estimated absent days, late days and missing punches, plus the column mapping it detected. That way you can check a month of attendance before payroll without building spreadsheet formulas.

- **Endpoint:** `https://www.watheeqahr.com/api/v1/mcp` (remote, Streamable HTTP)
- **Authentication:** none
- **Cost:** free
- **Made by:** [WatheeqaHR](https://www.watheeqahr.com), attendance, leave and payroll preparation for companies in the UAE, Saudi Arabia, Kuwait, Qatar, Bahrain and Oman.

## Tools

| Tool | What it does |
|---|---|
| `analyze_attendance_file` | Analyzes a device export, passed as `csv_text` or as `content_base64` + `filename`. Optional settings: shift start and end, weekend days, holidays, flexible schedule, required hours, Hijri calendar, sheet, country. |
| `list_supported_attendance_formats` | Lists the export header shapes the analyzer is tested against, so you can check a file before uploading it. |
| `get_product_facts` | Returns WatheeqaHR's scope, supported countries and pricing, so an assistant does not have to guess. |

## Connect

**Claude (web or desktop):** go to Settings → Connectors → Add custom connector, then paste `https://www.watheeqahr.com/api/v1/mcp`.

**Claude Desktop / Cursor / any client with a JSON config** (through [`mcp-remote`](https://www.npmjs.com/package/mcp-remote)):

```json
{
  "mcpServers": {
    "watheeqahr": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://www.watheeqahr.com/api/v1/mcp"]
    }
  }
}
```

**VS Code** (`.vscode/mcp.json`):

```json
{ "servers": { "watheeqahr": { "type": "http", "url": "https://www.watheeqahr.com/api/v1/mcp" } } }
```

**HTTP API (no MCP):** the same analyzer is described in OpenAPI 3.1 at `https://www.watheeqahr.com/api/v1/public/openapi.json`.

## Try it

Ask your assistant something like:

> "Here is our ZKTeco export for October. Shift is 08:00–17:00, Friday off. Who was late most often, and who has missing punches?"

Synthetic sample files are in [`examples/`](examples/). Every name and number in them is invented.

## Limits and privacy

- 5 MB per file, and 3 distinct files per 30 days per network address without an account.
- An encrypted copy of each uploaded file is kept for up to 90 days to improve the analyzer, then deleted automatically. A result summary is kept for 7 days behind an unguessable link.
- Only send files you are allowed to share. Full statement: [Privacy policy](https://www.watheeqahr.com/privacy).
- The results are an operational review, not legal or payroll advice. WatheeqaHR is not a WPS provider and does not file anything with any government.

More: [Developers & AI assistants guide](https://www.watheeqahr.com/developers) · [Supported export formats](https://www.watheeqahr.com/biometric-attendance-export-formats) · [Web analyzer](https://www.watheeqahr.com/tools/attendance-analyzer)

---

## بالعربية

**محلل ملفات الحضور من وثيقة — خادم MCP مجاني**

يتيح خادم MCP هذا لمساعدات الذكاء الاصطناعي (Claude وChatGPT وCursor وغيرها) **تحليل ملفات أجهزة البصمة مباشرة**. يدعم ZKTeco وBioTime وHikvision وDahua وAnviz وSuprema وFingerTec وMatrix COSEC وeSSL، بصيغ CSV وExcel والنصوص، وبعناوين أعمدة عربية أو إنجليزية.

لكل موظف يعرض أيام الحضور والغياب المقدّر وأيام التأخير والبصمات الناقصة، وذلك قبل تجهيز الرواتب ودون معادلات Excel.

- **الرابط:** `https://www.watheeqahr.com/api/v1/mcp`، مجاني ولا يحتاج تسجيلًا.
- **في Claude:** الإعدادات ← Connectors ← Add custom connector، ثم الصق الرابط.
- **المحلل على الويب:** [www.watheeqahr.com/ar/tools/attendance-analyzer](https://www.watheeqahr.com/ar/tools/attendance-analyzer)
- **الحدود والخصوصية:**
  - الحجم: حتى 5 MB للملف.
  - العدد: 3 ملفات مختلفة كل 30 يومًا لكل عنوان شبكة.
  - الاحتفاظ: نحتفظ بنسخة مشفّرة من الملف لمدة أقصاها 90 يومًا لتحسين المحلل، ثم تُحذف تلقائيًا.

## License

The documentation and sample files in this repository are released under the MIT License. The hosted service is operated by Fluxnova LLC (Sharjah Media City, UAE) under the [WatheeqaHR terms](https://www.watheeqahr.com/terms).
