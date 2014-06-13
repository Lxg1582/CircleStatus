<p align="center" ><img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/outlook1.png" alt="CircleStatus" title="CircleStatus" height="480"></p>


Small project to show circular chart with customizable number and range of colors on outer ring with background transparency/colors configuration. Demo project included. Works ok during orientation changes & redrawing. Supports also legend view.

## Examples:
Customizable colors, legend can be turned off or on (to see legend on look at big screenshots below)
<p align="center" ><img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/demo1.png" alt="CircleStatus img1" title="Customizable colors" height="100"></p>
Customizable percentage of each color in ring. You can also change the point where you want to start drawing colors:
<p align="center" ><img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/demo2.png" alt="CircleStatus img2" title="Customizable percentage of each color in ring. You can also change the point where you want to start drawing colors" height="100"></p>
You can attach image or text (or nothing) in the middle:
<p align="center" ><img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/demo3.png" alt="CircleStatus img3" title="You can attach image or text (or nothing) in the middle" height="100"></p>
Border width can be changed:
<p align="center" ><img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/demo4.png" alt="CircleStatus img4" title="Border width can be changed" height="100"></p>
Background can be clear or with any color. If total percentage is lower than 100%, rest of circle is transparent (like on the right):
<p align="center" ><img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/demo5.png" alt="CircleStatus img5" title="Background can be clear or with any color. If total percentage is lower than 100%, rest of circle is empty" height="100"></p>

## Outlook:
You can do much more than this ^^
<p align="center" >
<img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/outlook2.png" alt="CircleStatus" title="CircleStatus" height="480">
<img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/outlook3.png" alt="CircleStatus" title="CircleStatus" height="480">
<img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/outlook4.png" alt="CircleStatus" title="CircleStatus" height="480">
<img src="https://raw.github.com/natalia-osa/CircleStatus/master/ReadmeImages/outlook5.png" alt="CircleStatus" title="CircleStatus" height="480">
</p>

## Installation:
#### Installation with CocoaPods
[CocoaPods](http://cocoapods.org) is a dependency manager for Objective-C, which automates and simplifies the process of using 3rd-party libraries like AFNetworking in your projects. See the ["Getting Started" guide for more information](https://github.com/AFNetworking/AFNetworking/wiki/Getting-Started-with-AFNetworking).
```ruby
pod "CircleStatus", "~> 1.0"
```
#### Submodule
In your projects git foler type:
```bash
git submodule init
git submodule add --copy link to the repo--
git submodule update
```
Copy CSView.h and CSView.m to your project.
#### Just download & attach
This is strongly disadvised as you won't be able to see code updates. Clone or download the source, copy CSView.h and CSView.m to your project.

## Implementation:
Clone and see the demo for more examples about implementation. You can add the view via Storyboard or using code:
```objective-c
// in your view.h download the library
#import <CircleStatus/CSView.h>
// then add a property
@property (nonatomic, strong) CSView *csView;

// alloc & init the view or setup this via storyboard
- (id)initWithFrame:(CGRect)frame {
    self = [super initWithFrame:frame];
    if (self) {
        _csView = [[CSView alloc] init];
        [self addSubview:_csView];
    }
    return self;
}

// update the frame
- (void)layoutSubviews {
    [super layoutSubviews];
    
    CGRect bounds = self.bounds;
    CGSize csSize = CGSizeMake(CGRectGetWidth(bounds) - 20.f, 100.f); // chart size
    csSize.height = [_csView.legendView heightForChartSize:csSize]; // request chart height from legendView
    
    [_csView setFrame:CGRectIntegral(CGRectMake(CGRectGetMidX(bounds) - (csSize.width / 2), CGRectGetMidY(bounds) - (csSize.height / 2), csSize.width, csSize.height))];
}

// in your controller you can change outlook of the control
- (void)viewDidLoad {
    [super viewDidLoad];
    
    // fill with data
    [_csExampleView.csView setPercentageColorArray:@[[[CSPercentageColor alloc] initWithColor:[UIColor greenColor] percentage:0.7f],
                                                     [[CSPercentageColor alloc] initWithColor:[UIColor yellowColor] percentage:0.3f]]];
    // setup middle view: either text or image or nothing
    [_csExampleView.csView.textLabel setText:@"Chart"];
//    [_csExampleView.csView.imageView setImage:[UIImage imageNamed:@"test"]];
    // setup chart view
    [_csExampleView.csView setRadius:50.f];
    [_csExampleView.csView setFillColor:[UIColor colorWithWhite:1.f alpha:0.4f]];
    [_csExampleView.csView setStartAngle:15];
    [_csExampleView.csView setLineWidth:10];
    // setup legend
    [_csExampleView.csView setShowsLegend:NO];
    [_csExampleView.csView.legendView setLegendPosition:CSLegendPositionRight];
}
```
