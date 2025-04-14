# 📦 bundle4llm

A specialized JavaScript bundler that creates single-file bundles optimized for feeding into Large Language Models (LLMs). Inspired by [GitIngest](https://gitingest.com).

## Why bundle4llm?

LLMs like Claude and GPT process code more effectively when it's presented as a cohesive, self-contained unit without imports, exports, or external dependencies. This tool automatically:

- Resolves and includes all module dependencies
- Removes import/export statements
- Preserves logical code organization
- Estimates token consumption for different LLM models
- Creates a single file that's ready for LLM processing

[GitIngest](https://gitingest.com) was my go-to for this, but I wanted something integrated into my workflow that I could run on the command line and integrate with any project I'm working on.

The ideal use case is when you have a self-contained project that you want to feed into an LLM. This bundle is exceptionally useful for running on the Claude REPL to help you find issues in your code. 

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

Will produce a single file `./dist/llm-code.js` with all project files included, imports/exports removed, and token estimation. The bundle should be a valid JavaScript file that can be run directly either on the browser on a JS REPL.

## Project Integration

### Adding to your project

To use bundle4llm as part of your development workflow, install it as a devDependency:

```bash
# Using npm
npm install --save-dev bundle4llm

# Using yarn
yarn add --dev bundle4llm

# Using pnpm
pnpm add -D bundle4llm
```

### Adding to your scripts

Once installed, you can add it to your package.json scripts:

```json
"scripts": {
  "build:llm": "npx bundle4llm --src=./src --out=./llm-docs --file=myproject-llm.js -v"
}
```

Then simply run:

```bash
npm run build:llm
```

This will generate an LLM-optimized bundle of your code that you can then feed to models like Claude or GPT for analysis, documentation, or refactoring assistance.

### CI/CD Integration

You can also integrate bundle4llm into your CI/CD pipelines to automatically generate LLM-ready code snapshots. This is particularly useful when you want to:

- Generate documentation with AI assistance
- Perform automated code reviews with LLMs
- Create code snapshots for debugging sessions with AI

Add the build:llm script to your CI workflow to generate these files during your build process.

## Limitations

- Currently only supports JavaScript (ES2020)
- Does not handle circular dependencies
- Does not include external dependencies so it's best suited for self-contained projects.
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
