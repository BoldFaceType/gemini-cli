# Gemini CLI

Gemini CLI is a command-line interface designed to provide a seamless experience for users interacting with the Gemini project. This README outlines the setup instructions, usage, and other relevant information to help you get started.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Installation

To install the necessary dependencies, ensure you have Python 3.12 or higher installed, then run:

```bash
pip install -r requirements.txt
```

## Usage

To run the Gemini CLI, execute the following command in your terminal:

```bash
python -m src.main
```

You can also use various command-line arguments to customize the behavior of the CLI. For a full list of options, run:

```bash
python -m src.main --help
```

## Configuration

The Gemini CLI can be configured using the `gemini.toml` file located in the `configs` directory. Refer to the [configuration documentation](docs/configuration.md) for detailed instructions on how to set up your configuration.

## Testing

To run the unit tests for the Gemini CLI, use the following command:

```bash
pytest tests/
```

This will execute all tests defined in the `tests` directory.

## Contributing

Contributions are welcome! Please follow the guidelines outlined in the `CONTRIBUTING.md` file (if available) and ensure that your code adheres to the project's coding standards.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.