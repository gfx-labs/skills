# gfx labs llm repo

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
