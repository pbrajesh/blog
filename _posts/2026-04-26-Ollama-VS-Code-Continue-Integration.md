---
layout: post
title: "Ollama VS Code Continue Integration"
date:   2026-04-26 14:38:13 +0530
categories: welcome
tags: [ollama, vscode, llms, deeplearning, coding]
---

This post will guide you through integrating VS Code IDE Continue Plugin with Ollama, covering both local and remote setups.

## Integrating VS Code Continue Plugin with Ollama

**1. Setting Up Ollama Locally**

[Ollama](https://ollama.com/) a fantastic, lightweight, and easy-to-use tool for running LLMs locally. 

**2. Setting up VS Code Continue Plugin**

[Continue](https://www.continue.dev/) is an open-source AI coding assistant designed to integrate directly into popular development environments

*   **Install the Continue Extension:** In VS Code, go to the Extensions view (Ctrl+Shift+X or Cmd+Shift+X) and search for "Continue". 

**3. Setting up a Local Ollama Connection:**

The continue extension should automatically detect your Ollama instance. 

The continue ~/.continue/config.yaml

```
name: Local Config
version: 1.0.0
schema: v1
models:
  - name: Autodetect
    provider: ollama
    model: AUTODETECT
```

**4. Setting Up a Remote Ollama Connection (Cloud Instance):** 

The ~/.continue/config.yaml configurtion for Remote Ollama Connection is below.

```
name: Remote Config
version: 1.0.0
schema: v1
models:
  - name: Autodetect
    provider: ollama
    model: AUTODETECT
    apiBase: http://192.168.1.237:11434
```    

**Resources:**

*   Ollama: [https://ollama.com/](https://ollama.com/)
*   VS Code Marketplace: [https://marketplace.visualstudio.com/](https://marketplace.visualstudio.com/)

---
