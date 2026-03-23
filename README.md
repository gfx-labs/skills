# gfx labs llm repo

## rules for contributing

just please make sure your rules, skills, etc, have frontmatter that includes an author, like

```
---
author: elee
---
```

that's all.

## setup guide

this is a collection of random skills and agent rules that people use.

i personally install agent rules to `~/.agents/rules` using this config as part of my `~/.config/opencode/opencode.json`

```
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": [
    "~/.agents/rules/**/*.md"
  ]
}

```

and i run this command to make the skills from `~/.agents/skills`  available to opencode

```
ln -s ~/.agents/skills ~/.config/opencode/skills
```

## repo layout

skills are in the ./skills folder

agent rules are in the ./rules folder

mcp suggestions and markdown documents that describe what they do and how to set them up are in the ./mcp folder


