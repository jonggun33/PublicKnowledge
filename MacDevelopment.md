# Mac/iOS Development

## Management
[Sign in with your Apple ID](https://developer.apple.com/account/#/welcome)

## Objective-C
[Objective-C Hello World Tutorial - JournalDev](https://www.journaldev.com/9512/objective-c-hello-world-tutorial)

### Basic Structure
- main.h
```objective-c
#import <Foundation/Foundation.h>
@interface BMI : NSObject{    //@interface ## class
  int weight; //definition of INSTANCE VARIABLE
}
@property (nonatomic, readwrite) double height; //nonatomic:?? , readwrite: can read and change the value
-(double) bmi;  //-instance method, +class method
@end
```

main.m
```objective-c
#import "main.h"
@implementation BMI
@synthesize height; //.h에서 정의된 property의 구현
-(id) init{
  self = [super init];  weight = 68; //initialization of INSTANCE VARIABLE
  return self;
}
-(double) bmi{
  return weight/(height*height);
}
int main(int argc, const char* argv[]){
  @autoreleasepool {
    BMI * person = [[BMI alloc] init];
    double result = 0.0;
    person.height = 1.78;
    result = [person bmi];
    NSLog(@"BMI of Person is : %f", result); //@"": creates a NSString
  }
  return 0;
}
```

### Method (Function, Message) Definition/Calling
```objective-c
- (int)addX: (int)x toY:(int)y {
  return x+y;
}
int points = 100;
int newScore = [score addX: 24 toY:points];
```

### Collections
```objective-c
NSArray* colors = @[@"Red", @"Yellow", @"Green"];
for(NSString* item in colors){
  NSLog(@colors displayed: %@", item);
}
NSMutableArray* sports = [NSMutableArray arrayWithObjects: @"Cricket", @"Football", nil];
[sports addObject:@"Basketball"];
[sports removeLastObject];
NSSet countries;
NSDictionary capitals;
```
## Application Structure
### Objective-C, iOS
.Files
main.m, main file
AppDelegate, :UIResponder <UIApplicationDelegate>
ViewController, :UIViewController
Main.storyboard,
LaunchScree.storyboard,
info.plist, 

```objective-c
```


.ViewController.h
```objective-c

```C
@interface ViewController: UIViewController{
  IBOutlet UILabel* label;
}
-(IBAction)showLabel;
@end
```

.ViewController.m
```objective-c
-(IBAction)showLabel{
  label.text = @"Hello";
}
```

#### Wiring
. Place UI components from [Object Library]
. Modify attributes from [Attributes Inspector]
. Connect the button component to the [View Controller] to choose [showLabel] as the [Sent Events]
. You can pair codes and UI components from the [Assistant Editor] 

#### Multiple ViewControllers

#### Using Firestore as the backend


### Swift, iOS

## SwiftUI
[SwiftUI Tutorial from Apple Developer site](https://developer.apple.com/tutorials/swiftui/)


## Links


[Building an iOS Search Controller](https://academy.realm.io/posts/building-an-ios-search-controller-in-objective-c/)

[iOS Development Tutorial - 26 - Creating and using Delegates](https://www.youtube.com/watch?v=eNmZEXNQheE)

[AppleProgramming](https://www.youtube.com/channel/UCDg-YmnNehm3KB0BpytkUJg)

[개발과 투자 : 네이버 블로그. segue 에 대해서 잘 설명 되어 있군](http://blog.naver.com/jdub7138/220393890771)
