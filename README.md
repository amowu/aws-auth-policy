# aws-auth-policy

Module version of AWS AuthPolicy for generating auth policies for AWS Gateway API Authorizers.

## Install

```sh
$ npm install aws-auth-policy --save
```

## Input

```js
var AuthPolicy = require("aws-auth-policy");

var apiOptions = {};
apiOptions.region = "us-east-1";
apiOptions.restApiId = "XXXX";
apiOptions.stage = "dev";

var authPolicy = new AuthPolicy("user|XXXX", 51505150, apiOptions);
authPolicy.allowMethod(AuthPolicy.HttpVerb.ALL, "/*");
var generated = authPolicy.build();

var policyJson = JSON.stringify(generated);
console.log(policyJson);
```

## Output

```json
{
  "principalId": "user|XXXX",
  "policyDocument": {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Action": "execute-api:Invoke",
        "Effect": "Allow",
        "Resource": [
          "arn:aws:execute-api:us-east-1:51505150:XXXX/dev/*/*"
        ]
      }
    ]
  }
}
```