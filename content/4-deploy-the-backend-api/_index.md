+++
title = "Deploy the backend API"
date = 2020
weight = 4
chapter = false
pre = "<b>4. </b>"
+++


#### Set up Amplify Data

1. On your local machine, navigate to the **`ai-recipe-generator/amplify/data/resource.ts`** file, and **update** it with the following code. Then, **save** the file.

- The following code defines the askBedrock query that takes an array of strings called ingredients and returns a BedrockResponse. The .handler(a.handler.custom({ entry: "./bedrock.js", dataSource: "bedrockDS" })) line sets up a custom handler for this query, defined in bedrock.js, using bedrockDS as its data source.

```typescript
import { type ClientSchema, a, defineData } from "@aws-amplify/backend";

const schema = a.schema({
  BedrockResponse: a.customType({
    body: a.string(),
    error: a.string(),
  }),

  askBedrock: a
    .query()
    .arguments({ ingredients: a.string().array() })
    .returns(a.ref("BedrockResponse"))
    .authorization((allow) => [allow.authenticated()])
    .handler(
      a.handler.custom({ entry: "./bedrock.js", dataSource: "bedrockDS" })
    ),
});

export type Schema = ClientSchema<typeof schema>;

export const data = defineData({
  schema,
  authorizationModes: {
    defaultAuthorizationMode: "apiKey",
    apiKeyAuthorizationMode: {
      expiresInDays: 30,
    },
  },
});
```

2. **Open** a new terminal window, **navigate** to your apps project folder, and **run** the following command to deploy cloud resources into an isolated development space so you can iterate fast.

```bash
npx ampx sandbox
```

{{% notice note %}}
If you got **SSMCredentialsError: AccessDeniedException** Error, you can **attach policies directly** named **AmazonSSMReadOnlyAccess** to your **Users** in **IAM**
{{% /notice %}}

![Image](/images/4-deploy-the-backend-api/addpolicy.png?width=40pc)

3. Once the cloud sandbox has been fully deployed, your terminal will display a confirmation message and the **`amplify_outputs.json`** file will be **generated** and **added** to your project. 