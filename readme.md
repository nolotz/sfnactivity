# SFNActivity

SFNActivity is a parallel activity task worker for AWS Step Functions Activities, written in Go.
It helps users to efficiently manage their pollers, ensuring high throughput and low latency for their systems.
This library is based on the AWS SDK v2.

## Features
- Implements a parallel activity task poller that can be scaled across multiple threads to improve throughput and latency.
- Built-in support for handling polling, sending heartbeats, and returning activity execution results.
- Automatic retries for failed operations.
- Graceful shutdown, ensuring proper termination of running activities.

## Installation
To install SFNActivity, you can use the following command:

```bash
go get github.com/nolotz/sfnactivity
```

## Usage
For detailed usage, please refer to the example tests.

## License
This library is distributed under the MIT License. See LICENSE for more information.

## Contributing
Contributions are welcome! Please feel free to open an issue or submit a pull request with your changes.