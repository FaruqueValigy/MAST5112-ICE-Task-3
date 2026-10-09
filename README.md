# MAST5112 ICE Task 3 — Album Collection

## Introduction

This React Native TypeScript application is an album collection manager. Users can enter an album title, artist, release year, genre, and rating, add valid albums to their favourites, and delete saved albums.

The task focused on debugging and improving the supplied app while preserving its original album-collection concept.

## Development Environment

- Expo SDK 54
- React Native 0.81.5
- React 19.1.0
- TypeScript 5.9.2
- Expo Go
- BlueStacks 5 Android emulator
- Institutional virtual machine used for development and testing

The project uses a single `App.tsx` entry point. It uses `@react-native-picker/picker` version `2.11.1` for genre selection.

## Running the Project

```bash
npm install
npx expo-doctor
npx expo start
```

Open the project in Expo Go on BlueStacks 5. Test adding an album, validation messages, genre selection, and deletion.

## Detailed Error Log

### Problem 1 — Picker dependency and import compatibility

The supplied source used a picker import that was not aligned with the installed project dependency.

The final app imports `Picker` from `@react-native-picker/picker` and uses the Expo SDK 54-compatible version `2.11.1` declared in `package.json`.

### Problem 2 — Incorrect TypeScript model types

The supplied `Album` type declared `year` and `rating` as strings, but the save function converted both values to numbers.

The `Album` type now declares `year` and `rating` as numbers, matching the values stored by the application.

### Problem 3 — Impossible validation conditions

The original title and artist length checks used `&&` between the minimum and maximum conditions. A value cannot be below the minimum and above the maximum at the same time, so invalid lengths were not rejected.

The checks now use `||`. Year validation rejects years before 1900 and years after the current year. Rating validation accepts only whole numbers from 1 to 5.

### Problem 4 — Incorrect picker, collection, and delete state logic

The original picker used `title` as its selected value, every genre item used the same value, saving replaced the collection, and deletion retained only the selected album.

The picker is now controlled by `genre`, each item uses its own genre value, new albums are appended to the collection, and deletion removes only the album with the selected ID.

## Testing

The project should be tested with the following commands and interactions:

```bash
npx tsc --noEmit
npx expo-doctor
```

Functional tests:

1. Launch the app in Expo Go on BlueStacks 5.
2. Submit an empty form and confirm that a validation message appears.
3. Enter a valid album and confirm that it appears in the favourites list.
4. Select a genre and confirm that the selected genre is saved.
5. Add a second album and confirm that both albums remain visible.
6. Delete one album and confirm that the other album remains visible.
7. Enter invalid title, artist, year, and rating values and confirm that validation messages appear.

## Screenshot Evidence

The final submission should include a genuine screenshot captured while the corrected app is running in Expo Go on BlueStacks 5. The screenshot should show the album collection interface and at least one saved album.

## Conclusion

The album collection app was debugged while preserving its original concept. The final implementation addresses picker compatibility, TypeScript model accuracy, validation boundaries, picker state, collection updates, and deletion behaviour.

## References

- [Expo SDK 54 reference](https://docs.expo.dev/versions/v54.0.0/)
- [Expo SDK 54 Picker documentation](https://docs.expo.dev/versions/v54.0.0/sdk/picker/)
- [React Native Picker documentation](https://github.com/react-native-picker/picker)
