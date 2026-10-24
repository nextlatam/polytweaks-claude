---
name: setup
description: Connect or troubleshoot the Polytweaks connector in Claude when the user asks to set it up, reconnect an account, or fix missing Polytweaks tools.
---

# Connect Polytweaks

The Polytweaks plugin pairs workflow skills with a remote MCP connector. Installing the instructions does not establish a connection or publish its server. Use the bundled Polytweaks connector in the plugin's Connectors tab after the service has been released. Do not substitute the ChatGPT or Gemini endpoint.

The current release supports the hosted Claude OAuth profile for chat, Desktop, mobile and Cowork, pending live verification. Claude Code's separate native OAuth client is not supported by this release. Do not place a confidential client secret in a Claude Code configuration or invent a workaround to make it connect.

Let the user sign in on Polytweaks and review the requested account permissions. Never ask for passwords, bearer tokens, cookies or developer client secrets in chat. A test administrator may configure a client in Claude's secure connector settings; this is not a credential the end user needs to supply for an approved directory connection. If authentication is not configured, report that the provider must complete setup.

Verify the connection with `list_models` and a small limit. A successful empty list is valid. If there is no pending task, suggest one first GLB upload through the Polytweaks web app; do not create a sample. If the user already supplied files and asked to save them, continue that task using [model-library](../model-library/SKILL.md).

For an unexpected library, explain that the connected Polytweaks account is selected during OAuth and may differ from the Claude account. Have the user reconnect to their intended Polytweaks account rather than trying other credentials or bypassing access controls.

To disconnect, unlink the connector in Claude and revoke its grant from the Polytweaks Claude integration settings. Removing the skill or plugin instructions alone does not establish revocation. Do not claim setup or revocation succeeded without a confirming result.

Use English by default, honor an explicit language preference and preserve user-authored names. Keep setup concise; do not recite all tools or sharing settings. Creation/editing depends on the actual available authoring environment. This plugin installs neither Blender nor a paid cloud worker and requires no user-supplied Anthropic API key.
