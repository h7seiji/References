# AWS Lambda

AWS Lambda is a cloud computing service that lets developers run code without managing servers.
It's an example of serverless architecture and function as a service (FaaS).

## Lambda Layers

AWS Lambda Layers are ZIP archives that contain libraries, frameworks, or other dependencies that can be shared across multiple Lambda functions.
They allow you to keep your function code small and focused while maintaining a clean separation of concerns between your core logic and supporting libraries.

### Layer Code Package

- ZIP archive containing dependencies
- Maximum size limit of 250MB uncompressed
- Can include multiple versions

### Runtime Compatibility

- Specific to Lambda runtime environments
- Ensures compatibility across functions
- Supports version-specific dependencies

### Version Control

- Each layer version is immutable
- Allows rollbacks to previous versions
- Enables testing of new versions
