# BGOperation
Elegant Background Operation Library for iOS

* BGOperation: Background operation
* BGOperationTask: Background task composed of set number of background operation to execute once
* BGOperationQueue: Background queue that can continuously enqueue background operations

```
@interface MyOperation : BGOperation

- (id)initWithMyArg:(MyArg *)arg;

@end

@implementation MyOperation

// Override execute()
- (void)execute {

    // Do Something
    [self progress:0.25];
    
    [self callMyFunction:^(BOOL success) {
    
        if (success) {
            return [self success];
        } else {
            return [self fail];
        }
    }]
}

@end
```

```
MyOperation *op = [[MyOperation alloc]initWithMyArg:arg];
[op run:^(BGOperationResult *result) {
    // Done!
}];
```
