# VoltScript Testing Framework

VoltScript Testing Framework is a framework for testing code written using VoltScript, the evolution of LotusScript delivered as part of HCL Volt MX Go. The framework can also be used for LotusScript, with modifications (see below on new language functions used). There are deliberately no dependencies on any LSXs (e.g nlsxbe.dll). None should be added, it will make it dependent on a particular implementation. Create separate classes derived from CustomTester to test individual LSXs or custom classes.

## Using dependency management

Dependency management is available in the documentation for each project, but also aggregated here:

### Authentication

You'll need a [Personal Access Token](../howto/writing/archipelago.md#github-personal-access-token) to use GitHub REST APIs. You'll then need to add this to the JSON object in your [atlas-settings.json](../howto/writing/archipelago.md#atlas-settingsjson), in the .vss directory of your user home directory:

```json
    "hcl-github": {
        "type": "github",
        "token": "${env.TOKEN}"
    }
```

### Repository

You'll need to add to your **repositories** object in the atlas.json of your project:

```json
        {
            "id": "hcl-github",
            "type": "github",
            "url": "https://api.github.com/HCL-TECH-SOFTWARE"
        }
```

### Dependency

You'll need the relevant dependency to add to your **dependencies** or **testDependencies** object in the atlas.json of your project:

```json
        {
            "library": "voltscript-testing",
            "version": "1.0.0",
            "module": "VoltScriptTesting.vss",
            "repository": "hcl-github"
        }
```

## Writing VoltScript Tests

See [Writing Units Tests](/docs/howto/writingtests.md).

## Core Functions Used

Obviously the code runs certain core language functions. These are documented in [Core Functions](/docs/references/CoreFunctions.md).

There are three new VoltScript language functions used - Try/Catch/Finally and GetThreadInfo(12) in TestRunner.vss and ++/-- in SampleBeforeAfterTester.vss.

## Contributing

See [CONTRIBUTING.md](contributing.md).

## Code of Conduct

See [CODE_OF_CONDUCT.md](code_of_conduct.md).

## Issues and discussions

Let's chat on [OpenNTF Discord](https://openntf.org/discord).

For long-running discussions, use Discussions area in GitHub. For bugs and feature requests **specific to VoltScript Testing Framework** use, Issues area.