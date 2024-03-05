# Serialize Config for Booster Framework Injectable

Welcome to the **Serialize Config** component for Booster Framework's Injectable! This indispensable tool streamlines your infrastructure automation by serializing the Booster Config object into a JSON file. It allows for easy extraction of names and type information for your project's commands, events, entities, read models, and more. Serialize Config is perfect for use with automation tools like Terraform, enhancing your development workflow.

<h2>Table of Contents</h2>

- [Features](#features)
- [Quick Start](#quick-start)
  - [Installation](#installation)
  - [Configure Injectable](#configure-injectable)
  - [Modify Your Entry File](#modify-your-entry-file)
- [Running Serialize Config](#running-serialize-config)
- [Example: Leveraging Serialize Config for automatic Terraform generation](#example-leveraging-serialize-config-for-automatic-terraform-generation)
  - [Using the CartReadModel JSON for Terraform Preconfiguration](#using-the-cartreadmodel-json-for-terraform-preconfiguration)
  - [Example Terraform configuration for the CartReadModel](#example-terraform-configuration-for-the-cartreadmodel)
- [Getting Help](#getting-help)
- [Contributing](#contributing)
- [License](#license)


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

### Configure Injectable

If you don't already have an Injectable configuration file (`injectable.ts`) in your project, you'll need to create one. Here's how to configure Injectable to use Serialize Config:

```typescript
// your-app/src/config/injectable.ts
import * as Serialize Config from '@boostercloud/serialize-config'
import { Injectable } from '@boostercloud/framework-core'
import { NodeContext, Runtime } from '@effect/platform-node'

export default {
  commands: [SerializeConfig.command],
  runMain: Runtime.runMain,
  contextProvider: NodeContext.layer,
} as Injectable.Injectable
```

### Modify Your Entry File

To ensure Serialize Config works seamlessly with your Booster project, modify your entry file (`index.ts`) to include the `withInjectable` configuration before starting the application:

```typescript
// your-app/src/index.ts
import injectable from './config/injectable'

Booster.withInjectable(injectable).start(__dirname)
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

## Example: Leveraging Serialize Config for automatic Terraform generation

To illustrate how Serialize Config can be used to preconfigure resources with Terraform, let’s consider a simplified example from a JSON output, focusing on a specific section named `CartReadModel`. This model outlines the structure and data types of a shopping cart in an e-commerce application. Here’s a snippet highlighting key properties:

```json
"CartReadModel": {
  "properties": [
    {
      "name": "id",
      "typeInfo": {
        "name": "UUID",
        "typeGroup": "Class",
        "isNullable": false
      }
    },
    {
      "name": "testProperty",
      "typeInfo": {
        "name": "number",
        "typeGroup": "Number",
        "isNullable": false
      }
    },
    {
      "name": "cartItems",
      "typeInfo": {
        "name": "CartItem[]",
        "typeGroup": "Array",
        "isNullable": false
      }
    },
    {
      "name": "shippingAddress",
      "typeInfo": {
        "name": "Address",
        "typeGroup": "Class",
        "isNullable": true
      }
    }
  ]
}
```

This JSON snippet includes an identifier (`id`), a test property (`testProperty`), an array of cart items (`cartItems`), and a shipping address (`shippingAddress`). Each property has associated type information, such as `UUID` for the `id` or `CartItem[]` for the list of items in the cart, indicating the expected data structure and types for these fields.

### Using the CartReadModel JSON for Terraform Preconfiguration

Given the CartReadModel example, you can use this structured information to preconfigure Terraform resources, ensuring that your infrastructure aligns with the application’s data models. Here’s how to approach this:

- **Define Database Schema**: Extract key information from the CartReadModel to define the schema of a database table. Each property in the JSON maps to a column in the table, with the typeInfo indicating the data type.

- **Terraform Resource Definition**: Use the schema information to create a Terraform resource definition for a database table. For instance, if using AWS DynamoDB, define attributes and their types based on the model’s properties.

### Example Terraform configuration for the CartReadModel

```tf
resource "aws_dynamodb_table" "cart_table" {
  name           = "Cart"
  hash_key       = "id"
  billing_mode   = "PROVISIONED"

  attribute {
    name = "id"
    type = "S" # String type for UUID
  }

  attribute {
    name = "testProperty"
    type = "N" # Number
  }

  ...
}
```

By following these steps, developers can leverage the detailed structure provided by Serialize Config to ensure their Terraform configurations accurately reflect the application’s data models, streamlining the infrastructure setup and maintenance process.

## Getting Help

Should you face any challenges or have questions regarding Serialize Config, please consult the [Booster Framework documentation](https://docs.booster.cloud/) or join our vibrant community on the Discord server (link available in the docs). Our community and contributors are eager to assist.

## Contributing

Contributions to Serialize Config are warmly welcomed. Whether it's enhancing documentation, adding features, or reporting issues, your input helps us improve. Please refer to our [contributing guidelines](https://github.com/boostercloud/booster/blob/main/CONTRIBUTING.md) for more information.

## License

Serialize Config is open-source software licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

---

Dive into the world of efficient infrastructure automation with Serialize Config and elevate your Booster Framework projects to new heights!
