# BGOperation
BGOperation is an elegant background operation library for iOS. It's compatible with native NSOperation, but with additional set of library to make creating and running NSOperations easy.

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
* `BGOperationQueue`: Background queue that can continuously run background operations
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
