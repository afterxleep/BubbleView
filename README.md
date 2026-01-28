# BubbleView

[![Swift Package Manager compatible](https://img.shields.io/badge/Swift%20Package%20Manager-compatible-brightgreen.svg)](https://github.com/apple/swift-package-manager)

A SwiftUI view that displays content within a customizable chat-bubble shape with an arrow pointer.

<img src="https://raw.githubusercontent.com/afterxleep/BubbleView/main/bubble-demo.gif" width="300">


## Features

-   Displays any SwiftUI `View` content inside a bubble.
-   Customizable arrow pointer:
    -   Length (`arrowLength`)
    -   Width (`arrowWidth`)
    -   Position along the bubble's edge (`arrowPositionPercent`, calculated along flat edges).
    -   Bend (`bend`) for a shark-fin style (left/right lean).
    -   Side curvature (`finSideCurve`) for curved fin edges.
    -   Tip roundness (`finTipRoundness`) to limit tip rounding.
-   Customizable bubble appearance:
    -   Corner radius (`cornerRadius`).
    -   Fill color (`fillColor`).
    -   Border color (`borderColor`).
    -   Border width (`borderWidth`).
-   Customizable padding between content and bubble edges (`paddingAmount`).
-   Automatically sizes itself based on the content.
-   Arrow automatically avoids corners and adjusts its position to fit on flat edges.

## Requirements

-   iOS 14.0+ / macOS 11.0+ / watchOS 7.0+ / tvOS 14.0+
-   Swift 5.3+
-   Xcode 12.0+

## Installation

### Swift Package Manager

1.  In Xcode, open your project and navigate to **File > Swift Packages > Add Package Dependency...**
2.  Enter the repository URL: `https://github.com/afterxleep/BubbleView.git`
3.  Choose the version rules (e.g., "Up to Next Major") and click **Next**.
4.  Select the `BubbleView` library product and click **Finish**.

Alternatively, add it to the `dependencies` value of your `Package.swift` file:

```swift
dependencies: [
    .package(url: "https://github.com/afterxleep/BubbleView.git", from: "1.0.0") // Replace 1.0.0 with your desired version
]
```

## Usage

Import the package into your SwiftUI file:

```swift
import SwiftUI
import BubbleView
```

Then, use `BubbleView` like any other SwiftUI view, providing the content via a trailing closure:

```swift
struct ContentView: View {
    var body: some View {
        VStack(spacing: 40) {
            BubbleView(
                arrowLength: 15,
                arrowWidth: 30,
                arrowPositionPercent: 10, // Near top-left corner
                cornerRadius: 12,
                bend: 0.35,
                finSideCurve: 0.6,
                finTipRoundness: 0.7,
                fillColor: .blue,
                borderColor: .black,
                borderWidth: 1,
                paddingAmount: 10
            ) {
                Text("This is a message inside a blue bubble!")
                    .foregroundColor(.white)
                    .padding(5) // Optional inner padding for content
            }

            BubbleView(
                arrowPositionPercent: 60, // Bottom edge
                cornerRadius: 0, // Sharp corners
                bend: -0.25,
                finSideCurve: 0.4,
                finTipRoundness: 0.7,
                fillColor: Color(white: 0.95),
                borderColor: .gray,
                borderWidth: 0.5
            ) {
                HStack {
                    Image(systemName: "info.circle.fill")
                    Text("Another bubble, different style.")
                }
                .foregroundColor(.black)
            }
        }
        .padding()
    }
}
```

## Customization Parameters

You can customize the appearance and behavior of the `BubbleView` using its initializer parameters:

-   `arrowLength`: `CGFloat` - The length of the arrow extending from the bubble edge. Default: `15`.
-   `arrowWidth`: `CGFloat` - The width of the base of the arrow. Default: `30`.
-   `arrowPositionPercent`: `CGFloat` - A percentage (0-100) determining the arrow's center position along the *flat* perimeter of the bubble (top -> right -> bottom -> left). Default: `10`. The position is clamped to ensure the arrow fits on a flat edge.
-   `cornerRadius`: `CGFloat` - The radius of the rounded corners. Default: `10`.
-   `bend`: `CGFloat` - Fin bend amount. `0` is straight; positive bends right, negative bends left. Values beyond `1` push the tip further along the edge. Default: `0`.
-   `finSideCurve`: `CGFloat` - Curvature of the fin sides. `0` keeps sides straight; higher values curve the long side outward and short side inward. Default: `0`.
-   `finTipRadius`: `CGFloat` - Radius of the fin tip rounding. Default: `.greatestFiniteMagnitude`.
-   `finTipRoundness`: `CGFloat` - 0-1 multiplier to cap tip rounding to a safe amount; values > 0 separate the tip endpoints and add a curve between them. Default: `0` (sharp).
-   `fillColor`: `Color` - The background color of the bubble. Default: `.blue`.
-   `borderColor`: `Color` - The color of the bubble's outline. Default: `.clear`.
-   `borderWidth`: `CGFloat` - The width of the bubble's outline. Default: `0`.
-   `paddingAmount`: `CGFloat` - The padding applied *between* the content and the inside edge of the bubble shape. Default: `10`.
-   `content`: `@ViewBuilder () -> Content` - The SwiftUI view(s) to display inside the bubble.

## Playground

A `BubbleViewDemo.playground` is included in the `Examples` directory of this repository to demonstrate various configurations. You can open and run this playground in Xcode to see the `BubbleView` in action.

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue.

## License

This project is licensed under the terms of the MIT license. See the [LICENSE](LICENSE) file for details. 
