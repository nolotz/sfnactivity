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

### Create an activity worker instance

To create an instance, you need to use the `sfnactivity.New` function, providing an AWS Step Functions client (`sfnactivity.SFNClient`) and a configuration object (`sfnactivity.Config`). The configuration object must include the WorkerName and the ActivityArn (Amazon Resource Name) of your activity.

```go
activity := sfnactivity.New(sfnClient, sfnactivity.Config{
	WorkerName:   "test",
	ActivityArn:  "arn:aws:states:us-east-1:00000000000:activity:my-activity",
})
```

### Start the activity worker

To start the activity worker, call the `Start` method on the `activity` instance created in the previous step. The `Start` method accepts a `sfnactivity.TaskFunc` function as an argument, which will be executed whenever a task is received from AWS Step Functions.

```go
err := activity.Start(func(ctx context.Context, t *sfnactivity.Task) (string, error) {
    return `{"works": true}`, nil
})
if err != nil {
    panic(err)
}
```

### Stop the activity worker

To stop the activity worker, call the `Stop` method on the activity instance. This method accepts a context object, such as `context.TODO()`, which can be used to cancel the graceful shutdown if needed.

```go
activity.Stop(context.TODO())
```
When you call the `Stop` method, the activity worker will stop polling for new tasks and will wait for all the in-progress tasks to complete before returning. If the context object's cancellation function is called, it will interrupt the graceful shutdown, causing the activity worker to terminate immediately without waiting for in-progress tasks to finish.

For more detailed usage, please refer to the example tests.

## License
This library is distributed under the MIT License. See LICENSE for more information.

## Contributing
Contributions are welcome! Please feel free to open an issue or submit a pull request with your changes.