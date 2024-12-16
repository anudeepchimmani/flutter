import 'package:flutter_test/flutter_test.dart';
import 'package:anvitha/test.dart'; // Make sure this imports your Counter class

void main() {
  group('Counter', () {
    late Counter counter;

    setUp(() {
      counter = Counter(); // Initialize the Counter before each test
    });

    test('value should start at 0', () {
      expect(counter.value, 0);
    });

    test('value should be incremented', () {
      counter.increment();
      expect(counter.value, 1);
    });

    test('value should be decremented', () {
      counter.increment(); // Increment first to avoid negative value
      counter.decrement();
      expect(counter.value, 0);
    });
  });
}
....
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

// The root of your application
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      title: 'Slide Transition Widget',
      home: SlideTransitionWidget(),
    );
  }
}

// SlideTransitionWidget - A stateful widget with slide animation
class SlideTransitionWidget extends StatefulWidget {
  const SlideTransitionWidget({super.key});

  @override
  State<SlideTransitionWidget> createState() => SlideTransitionWidgetState();
}

// State for SlideTransitionWidget with SingleTickerProviderStateMixin
class SlideTransitionWidgetState extends State<SlideTransitionWidget>
    with SingleTickerProviderStateMixin {
  late final AnimationController _controller;
  late final Animation<Offset> _offsetAnimation;

  @override
  void initState() {
    super.initState();
    // Initialize the AnimationController
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat(reverse: true);

    // Define the offset animation
    _offsetAnimation = Tween<Offset>(
      begin: Offset.zero,
      end: const Offset(1.5, 0.0),
    ).animate(
      CurvedAnimation(
        parent: _controller,
        curve: Curves.elasticIn,
      ),
    );
  }

  @override
  void dispose() {
    // Dispose of the animation controller to free resources
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('SlideTransition Sample'),
        backgroundColor: Colors.green,
      ),
      body: Center(
        child: SlideTransition(
          position: _offsetAnimation,
          child: Padding(
            padding: const EdgeInsets.all(8.0),
            child: Image.network(
              'https://media.geeksforgeeks.org/wp-content/cdn-uploads/20210419113249/gfg-new-logo-min.png',
            ),
          ),
        ),
      ),
    );
  }
}
