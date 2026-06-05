# feishu-editable-diagrams

Version: 0.9

Feishu/Lark editable diagram skill. Use it when an agent needs to create, insert, or update SVG-based diagrams that remain editable inside Feishu documents or whiteboards, instead of being uploaded as static PNG/JPG images.

## What It Does

- Creates Feishu-friendly SVG diagrams using editable primitives such as rectangles, text, lines, groups, and simple paths.
- Converts SVG diagrams into Feishu whiteboard-compatible OpenAPI JSON.
- Inserts new editable whiteboards into Feishu documents through `lark-cli docs +update`.
- Updates existing Feishu whiteboards through `lark-cli whiteboard +update`.
- Validates SVG rendering, text overflow, node overlap, and editability before touching the Feishu document.
- Exports server-rendered previews after insertion or update so the result can be checked against the local preview.

## Install

Clone this repository into your agent skills directory:

```bash
cd ~/.codex/skills
git clone https://github.com/raymonder/feishu-editable-diagrams.git
```

If your agent uses another skills directory, clone the repository there instead. Keep the folder structure as:

```text
skills/
└── feishu-editable-diagrams/
    ├── SKILL.md
    └── README.md
```

Restart the agent or open a new session so the skill metadata is loaded.

## Use

Ask for an editable Feishu/Lark diagram:

```text
帮我在这个飞书文档里插入一个可编辑的流程图。
```

```text
把这张架构图做成飞书里可以编辑的白板，不要只是 PNG。
```

```text
更新这个飞书白板，保持里面的文字、方框和箭头都能继续编辑。
```

## Requirements

- Node.js and npm.
- `lark-cli` installed and authenticated.
- `@larksuite/whiteboard-cli` available through `npx`.
- Access to the target Feishu/Lark document or whiteboard.
- The relevant `lark-doc`, `lark-whiteboard`, and `lark-shared` skills, when available.

## Limits

- This skill is for editable diagrams, not photo editing, screenshot cleanup, or raster image design.
- Complex SVG features such as filters, gradients, masks, clipping paths, patterns, and `foreignObject` may not import cleanly.
- Automatic text wrapping is unreliable; labels should be split into explicit SVG text lines.
- Existing whiteboards should not be overwritten unless the user explicitly confirms replacement.
- A successful CLI command is not enough; the server-rendered Feishu preview still needs to be exported and checked.
- Permission errors, missing scopes, or unauthenticated `lark-cli` sessions must be handled through Feishu/Lark setup skills first.
