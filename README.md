# BGOperation
BGOperation is a light-weight extension of [iOS Operation Library (NSOperations/NSOperationQueue)](https://developer.apple.com/documentation/foundation/operation). It makes using operations/queues really easy.

* 100% compatible with iOS operations framework
* Supports async operation
* Profiling/monitoring built-in
* Advanced policy to control operation execution

As subclasses of NSOperation, BGOperation inherits the following advantages as well:

* Configure operation dependency
* Concurrency management (max concurrent operation count)
* Serial/Concurrent modes

## Installation

### Using CocoaPods

## Architecture

* `BGOperation`: Background operation (subclass of NSOperation)
  - `BGOperationDelegate`
  - `BGOperationStatus`
  - `BGOperationResult`
* `BGOperationTask`: Background task to run a set of background operations once
  - `BGOperationTaskDelegate`
  - `BGOperationTaskPolicy`
  - `BGOperationTaskStatus`
  - `BGOperationTaskResult`
* `BGOperationQueue`: Background queue that can continuously run operations (subclass of NSOperationQueue)
  - `BGOperationQueueDelegate`
  - `BGOperationQeueuPolicy`
  - `BGOperationQueueStatus`

## Usage

### Creating BGOperation
```objective-c
@interface MyOperation : BGOperation

- (id)initWithMyArg:(MyArg *)arg;

@end

@implementation MyOperation

// Override execute()
- (void)execute {
    [self myAsyncFunction:^(BOOL success) {
        if (success) {
            return [self success];
        } else {
            return [self fail];
        }
    }]
}

@end
```

### Running BGOperation
```objective-c
MyOperation *op = [[MyOperation alloc]initWithMyArg:arg];
[op run:^(BGOperationResult *result) {
    // Done!
}];
```
