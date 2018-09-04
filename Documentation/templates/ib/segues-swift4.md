## Template Information

| Name      | Description       |
| --------- | ----------------- |
| File name | ib/segues-swift4.stencil |
| Invocation example | `swiftgen ib -t segues-swift4 …` |
| Language | Swift 4 |
| Author | Olivier Halligon |

## When to use it

- When you need to generate *Swift 4* code for your storyboard *segues*.
- The generated code supports both UIKit platforms (iOS, tvOS and watchOS) and AppKit platform (macOS).

## Customization

You can customize some elements of this template by overriding the following parameters when invoking `swiftgen` in the command line, using `--param <paramName>=<newValue>`

| Parameter Name | Default Value | Description |
| -------------- | ------------- | ----------- |
| `enumName` | `StoryboardSegue` | Allows you to change the name of the generated `enum` containing all storyboard segues. |
| `module` | N/A | By default, the template will import the needed modules for custom classes, but won’t import the target’s module to avoid an import warning — using the `PRODUCT_MODULE_NAME` environment variable to detect it. Should you need to ignore an additional module, you can provide it here. |
| `ignoreTargetModule` | N/A | Setting this parameter will disable the behaviour of prefixing classes with their module name for (only) the target module. |
| `publicAccess` | N/A | If set, the generated constants will be marked as `public`. Otherwise, they'll be declared `internal`. |

## Generated Code

Note: the generated code may look differently depending on the platform the storyboard file is targeting.

**Extract:**

```swift
enum StoryboardSegue {
  enum Message: String, SegueType {
    case embed
    case nonCustom
  }
}
```

[Full generated code](https://github.com/SwiftGen/templates/blob/master/Tests/Fixtures/Generated/IB-iOS/swift4-context-all.swift)

## Usage example

```swift
// You can perform segues using:
vc.perform(segue: StoryboardSegue.Message.embed)

// or match them (in prepareForSegue):
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
  switch StoryboardSegue.Message(rawValue: segue.identifier!)! {
  case .embed:
    // Prepare for your custom segue transition
  case .nonCustom:
    // Pass in information to the destination View Controller
  }
}
```
