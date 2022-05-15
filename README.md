# Flutter interview questions and answers.

> You can :star: the project if you like it. Pull Requests are highly appreciated.

## Table of Contents

| No. | Questions                                                                                                                                                         |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | [What is flutter](#what-is-flutter)                                         |
| 2   | [Architectural layers](#architectural-layers)                                         |
| 3   | [What is a widget](#what-is-a-widget)                                         |
| 4   | [What is a Stateless widget](#what-is-a-stateless-widget)                                         |
| 5   | [What is a Stateful widget](#what-is-a-stateful-widget)                                         |
| 6   | [What is an Inherited widget](#what-is-an-inherited-widget)                                         |
| 7   | [What is a State](#what-is-a-state)                                         |
| 8   | [What is a Build context](#what-is-a-build-context)                                         |

1. ### What is flutter

Flutter is an open source framework that was ***developed by Google*** for building beautiful, natively compiled, multi-platform applications(Android, iOS, Linux, macOS, Windows, Google Fuchsia, and the web) from a single codebase. Flutter framework uses [Dart programming language](https://dart.dev/) for creating apps.

2. ### Architectural layers

***Platform-specific embedder layer*** - is written in a language that is appropriate for the platform: currently Java and C++ for Android, Objective-C/Objective-C++ for iOS and macOS, and C++ for Windows and Linux. It provides an entrypoint, coordinates with the underlying operating system for access to services like rendering surfaces, accessibility, and input. It also manages the message event loop.

***Flutter engine*** - is a core of Flutter, which is mostly written in C++ and supports the primitives necessary to support all Flutter applications. The engine is responsible for rasterizing composited scenes whenever a new frame needs to be painted. It provides the low-level implementation of Flutter’s core API, including graphics (through Skia), text layout, file and network I/O, accessibility support, plugin architecture, and a Dart runtime and compile toolchain.

The engine is exposed to the Flutter framework through [dart:ui](https://github.com/flutter/engine/tree/master/lib/ui), which wraps the underlying C++ code in Dart classes.

***Flutter framework*** - reactive framework written in the Dart language.
It consists of:
- the foundational level - classes, and building block services such as animation, painting, and gestures that offer commonly used abstractions over the underlying foundation.
- the rendering layer - provides an abstraction for dealing with layout. With this layer, you can build a tree of renderable objects. You can manipulate these objects dynamically, with the tree automatically updating the layout to reflect your changes.
- the widgets layer is a composition abstraction. Each render object in the rendering layer has a corresponding class in the widgets layer. In addition, the widgets layer allows you to define combinations of classes that you can reuse.
- the Material and Cupertino libraries offer comprehensive sets of controls that use the widget layer’s composition primitives to implement the Material or iOS design languages.

3. ### What is a widget

Widgets are the central class hierarchy in the ***Flutter framework***. Widget is a way to declare and construct UI. You can consider that a widget is a blueprint of the UI element.

There are 3 types of widgets:
 - [StatelessWidget](#what-is-a-stateless-widget)
 - [StatefulWidget](#what-is-a-stateful-widget)
 - [InheritedWidget](#what-is-an-inherited-widget)

4. ### What is a Stateless widget

A stateless widget is a widget that describes part of the user interface and does not require mutable state.

Stateless widget are useful when the part of the user interface you are describing does not depend on anything other than the configuration information in the object itself and the [BuildContext](#what-is-build-context) in which the widget is inflated.

The build method of a stateless widget is typically only called in three situations: 
 - the first time the widget is inserted in the tree;
 - when the widget's parent changes its configuration;
 - when an [Inherited Widget](#what-is-inherited-widget) it depends on changes.

#### Stateless widget example

```dart
class MyCustomStatelessWidget extends StatelessWidget {
    final Color color;
    final Widget? child;
    
    const MyCustomStatelessWidget({ 
        Key? key,
        this.color = Colors.red,
        this.child,
    }) : super(key: key);
 
    @override
    Widget build(BuildContext context) {
        return Container(color: color, child: child);
    }
}
```

*Note: By convention, widget constructors only use named arguments. Also by convention, the first argument is key, and the last argument is child, children, or the equivalent.*

5. ### What is a Stateful widget

A stateful widget is a widget that describes part of the user interface that can change dynamically.

Stateful Widgets have an internal state and can re-render if the input data changes or if Widget’s state changes.

#### Stateful widget example

```dart
class MyCustomStatefulWidget extends StatefulWidget {
    const MyCustomStatefulWidget({ 
        Key? key,
    }) : super(key: key);
 
    @override
    State<MyCustomStatefulWidget> createState() => _MyCustomStatefulWidgetState();
}

class _MyCustomStatefulWidgetState extends State<MyCustomStatefulWidget> {
    Color _color = Colors.red;

    void _changeColor() {
        setState(() { _color = Colors.green; });
    }

    @override
    Widget build(BuildContext context) {
        return Container(
            color: _color,
            child: ElevatedButton(
                onPressed: _changeColor,
                child: Text('change color'),
            ),
        );
    }
}
```
7. ### What is an Inherited widget
