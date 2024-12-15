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
