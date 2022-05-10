# Flutter interview questions and answers.

> You can :star: the project if you like it. Pull Requests are highly appreciated.

## Table of Contents

| No. | Questions                                                                                                                                                         |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | [What is flutter](#what-is-flutter)                                         |
| 2   | [What is widget](#what-is-a-widget)                                         |
| 3   | [What is a widget](#what-is-a-widget)                                         |
| 4   | [What is a Stateless widget](#what-is-a-stateless-widget)                                         |
| 5   | [What is a Stateful widget](#what-is-a-stateful-widget)                                         |
| 6   | [What is an Inherited widget](#what-is-an-inherited-widget)                                         |
| 7   | [What is a State](#what-is-a-state)                                         |
| 8   | [What is a Build context](#what-is-a-build-context)                                         |

1. ### What is flutter

Flutter is an open source framework that was ***developed by Google*** for building beautiful, natively compiled, multi-platform applications(Android, iOS, Linux, macOS, Windows, Google Fuchsia, and the web) from a single codebase. Flutter framework uses [Dart programming language](https://dart.dev/) for creating apps.

2. ### What is a widget

Widgets are the central class hierarchy in the ***Flutter framework***. Widget is a way to declare and construct UI. You can consider that a widget is a blueprint of the UI element.

There are 3 types of widgets:
 - [StatelessWidget](#what-is-a-stateless-widget)
 - [StatefulWidget](#what-is-a-stateful-widget)
 - [InheritedWidget](#what-is-an-inherited-widget)

3. ### What is a Stateless widget

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
