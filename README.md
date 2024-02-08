# Serialize Config for Booster Framework Nexus

Welcome to the **Serialize Config** component for Booster Framework's Nexus! This indispensable tool streamlines your infrastructure automation by serializing the Booster Config object into a JSON file. It allows for easy extraction of names and type information for your project's commands, events, entities, read models, and more. Serialize Config is perfect for use with automation tools like Terraform, enhancing your development workflow.

## Features

- **Automation Friendly**: Facilitates infrastructure as code (IaC) practices by making your Booster project's configuration accessible in JSON format.
- **Comprehensive Project Insights**: Gain detailed insights into your project's commands, events, entities, read models, and more.
- **Seamless Integration**: Integrate Serialize Config into your Booster project effortlessly to enhance your infrastructure automation.

## Quick Start

Follow these steps to integrate Serialize Config into your Booster project:

### Installation

First, install Serialize Config via npm by running the following command in your project directory:

```bash
npm install @boostercloud/serialize-config
```

### Configure Nexus

If you don't already have a Nexus configuration file (`nexus.ts`) in your project, you'll need to create one. Here's how to configure Nexus to use Serialize Config:

```typescript
// your-app/src/config/nexus.ts
import * as Serialize Config from '@boostercloud/serialize-config'
import { Nexus } from '@boostercloud/framework-core'
import { NodeContext, Runtime } from '@effect/platform-node'

export default {
  commands: [SerializeConfig.command],
  runMain: Runtime.runMain,
  contextProvider: NodeContext.layer,
} as Nexus.Nexus
```

### Modify Your Entry File

To ensure Serialize Config works seamlessly with your Booster project, modify your entry file (`index.ts`) to include the `withNexus` configuration before starting the application:

```typescript
// your-app/src/index.ts
import nexus from './config/nexus'

Booster.withNexus(nexus).start(__dirname)
```

## Running Serialize Config

Once you've set up Serialize Config in your Booster project, executing it is straightforward. To generate the serialized Booster configuration JSON file, run the following command from your project's root directory:

```bash
node dist/index.js serialize-config --help
```

This command provides you with additional options and usage information for the Serialize Config command.

By default, the output JSON file will be saved to `.booster/infra-config.json` within your project directory. If you wish to specify a different output location, you can use the `--output` flag followed by your desired path. Here's an example command that demonstrates this:

```bash
node dist/index.js serialize-config --output path/to/your/custom-config.json
```

This flexibility allows you to integrate the serialized configuration seamlessly into your infrastructure automation workflows.

## Getting Help

Should you face any challenges or have questions regarding Serialize Config, please consult the [Booster Framework documentation](https://docs.booster.cloud/) or join our vibrant community on the Discord server (link available in the docs). Our community and contributors are eager to assist.

## Contributing

Contributions to Serialize Config are warmly welcomed. Whether it's enhancing documentation, adding features, or reporting issues, your input helps us improve. Please refer to our [contributing guidelines](https://github.com/boostercloud/booster/blob/main/CONTRIBUTING.md) for more information.

## License

Serialize Config is open-source software licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

---

Dive into the world of efficient infrastructure automation with Serialize Config and elevate your Booster Framework projects to new heights!