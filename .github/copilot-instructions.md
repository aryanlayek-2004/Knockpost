# Knockpost Codebase Instructions for AI Agents

## Project Overview
**Knockpost** is a Flutter mobile app for social networking. Currently in early development with a single-file architecture focused on demonstrating a social feed UI with user profiles and posts.

## Architecture & Key Files

### Current Structure
- **[lib/main.dart](../../lib/main.dart)**: Single entry point containing all UI logic - `MyApp` (root widget), `HomeScreen` (main feed screen)
- **[pubspec.yaml](../../pubspec.yaml)**: Minimal dependencies; no state management, backend, or data persistence yet
- **[analysis_options.yaml](../../analysis_options.yaml)**: Uses `flutter_lints` with default recommended rules

### Data Organization (Current Pattern)
Data is currently hardcoded as static lists in widgets:
```dart
static const List<String> _profiles = ['Ava', 'Ben', ...];
static const List<Map<String, String>> _posts = [{'user': 'Ava Morgan', 'time': '2h ago', ...}];
```
**Future refactor**: Anticipate moving to model classes (e.g., `User`, `Post`) and service layer as app grows.

## UI/Widget Patterns

### Established Practices
1. **Stateless widgets preferred** - All existing screens use `StatelessWidget` (no mutable state yet)
2. **Material Design** - Uses `MaterialApp` with Material components (AppBar, Scaffold, ListView)
3. **Theme consistency** - Blue seed color (`Colors.blue`) with light background (`#FFF3F5F9`)
4. **Helper widgets** - `CircleAvatar` for user initials, `ListView.separated` for spacing
5. **Responsive layouts** - `ListView` with `shrinkWrap: true` and `SingleChildScrollView` to handle different screen sizes

### Code Style
- Dart naming: `_profiles` for private constants, `MyHomeScreen` for public classes
- Widget composition: Build complex UIs by nesting simple widgets
- Padding/spacing: Use `SizedBox` and `EdgeInsets` consistently (e.g., 16px horizontal padding is standard)

## Key Conventions

### When Adding Features
1. **Start in HomeScreen** until architecture pattern emerges
2. **Keep data with widget** for now (avoid premature service layer)
3. **Use const constructors** when possible (`const MyWidget()`)
4. **Follow Material guidelines** for spacing and colors (Material 3 with `colorScheme`)

### Building New Screens
1. Create `StatelessWidget` extending from `Scaffold`
2. Use `AppBar` for top navigation
3. Wrap scrollable content in `SingleChildScrollView` or `ListView`
4. Apply consistent 16px horizontal padding

### Flutter Commands (Common Dev Workflows)
```bash
flutter pub get          # Update dependencies
flutter analyze          # Run lint checks
flutter test            # Run widget tests
flutter run             # Run on connected device/emulator
flutter run -d <device> # Specify device
flutter build apk       # Build Android release
```

## Critical Notes for AI Agents

- **No state management yet** - If adding interactivity (likes, follows), decide on approach (Provider, Riverpod, etc.) first
- **No persistence** - All data is in-memory; backend integration needed for real app
- **Single file migration**: As features grow, extract `HomeScreen` into separate files (`screens/home_screen.dart`), then add models (`models/user.dart`, `models/post.dart`)
- **Hardcoded dependencies**: User names/initials are substring extractions; plan for proper name formatting in future
- **Color scheme**: Blue-based with soft shadows; maintain consistency

## Testing
- **Widget tests** use standard Flutter test patterns in [test/widget_test.dart](../../test/widget_test.dart)
- **New tests**: Add to `test/` directory following existing test structure

## Next Likely Steps
1. Extract UI into separate widget files
2. Add navigation between screens
3. Implement state management for interactivity
4. Connect to backend API (if needed)
