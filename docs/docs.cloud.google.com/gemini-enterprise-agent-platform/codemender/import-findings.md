---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/import-findings
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/import-findings
title: Import third-party security findings
description: Learn how to import vulnerability findings from other static analysis tools directly into CodeMender.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

If you already use third-party static analysis or vulnerability scanning tools, you can import findings directly into CodeMender to proceed immediately to verification and patching.

## Import security reports

CodeMender parses external security reports and registers findings in its local database.

### Import a JSON findings file

To import findings from a JSON file, use the `--file` (or `-f` ) flag. The JSON file must conform to the following schema:

    [
      {
        "file_path": "src/auth/session_manager.py",
        "line": 42,
        "title": "SQL Injection",
        "message": "Raw user input concatenated in SQL query",
        "severity": "HIGH",
        "vuln_type": "CWE-89"
      }
    ]

Run the import command:

    cm report import --file ./findings.json

### Interactive import mode

If you don't have a JSON file, you can run the import command without the `--file` flag to enter an interactive wizard in your terminal:

    cm report import

Follow the prompts to enter the path, line number, severity, and description for each finding. Enter `q` at any prompt to finish and save.

## Process imported findings

After importing external findings:

1.  Run `cm report` to view the list of registered findings and obtain their generated `<finding-id>` values.

2.  Execute verification on an imported finding to generate a proof-of-concept exploit:
    
        cm verify FINDING_ID

3.  Generate and validate a security patch for the finding:
    
        cm fix FINDING_ID
