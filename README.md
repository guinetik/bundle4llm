# 📦 bundle4llm

A specialized JavaScript bundler that creates comprehensive, single-file bundles optimized for feeding into Large Language Models (LLMs).

## Why bundle4llm?

LLMs like Claude and GPT process code more effectively when it's presented as a cohesive, self-contained unit without imports, exports, or external dependencies. This tool automatically:

- Resolves and includes all module dependencies
- Removes import/export statements
- Preserves logical code organization
- Estimates token consumption for different LLM models
- Creates a single file that's ready for LLM processing

## Features

- 🧩 **Recursive Module Resolution**: Automatically includes all dependencies
- 📋 **Export-Driven Ordering**: Uses index.js files to determine correct module order
- 🔄 **Directory Structure Preservation**: Maintains logical organization with comments
- 🧹 **Code Sanitization**: Removes imports/exports and optionally strips comments
- 📏 **Token Estimation**: Provides accurate token counts for various LLM models
- 🛠️ **Configurable**: Multiple presets and options for customization

## Installation

```bash
# Install globally
npm install -g bundle4llm

# Or use with npx
npx bundle4llm
```

## Usage

```bash
bundle4llm --src ./src --out ./dist --file bundle.js --model claude --preset es2020 --strip-comments -v
```

### Options

| Option | Description | Default |
|--------|-------------|---------|
| `--src` | Source directory | `./src` |
| `--out` | Output directory | `./dist` |
| `--file` | Output filename | `llm-bundle.js` |
| `--preset` | Code sanitization preset (`es2020`, `es2015`, `minimal`) | `es2020` |
| `--strip-comments` | Remove comments from the output | `false` |
| `--model` | LLM model for token estimation (`claude`, `gpt3`, `gpt4`) | `claude` |
| `-v`, `--verbose` | Enable verbose logging | `false` |

## Example

Suppose you have a project with multiple JavaScript files and subdirectories:

```
src/
├── index.js
├── utils/
│   ├── index.js
│   ├── helpers.js
│   └── math.js
└── components/
    ├── index.js
    ├── base.js
    └── advanced.js
```

Running:

```bash
bundle4llm --src ./src --out ./dist --file llm-code.js --model claude -v
```

Will produce a single file `./dist/llm-code.js` with all dependencies included, imports/exports removed, and token estimation for Claude.

## Limitations

- Currently only supports JavaScript (ES2020)
- Does not handle circular dependencies
- Best suited for projects using ES modules

## License

APACHE

## Contributing

Contributions welcome! Open an issue or submit a PR.

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add some amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request
