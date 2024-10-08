### Prompt

Write unit tests based on the following information:

- Testing library: Jest
- Function: Called `filterWorkouts`. This function is yet to be written but will be used to filter workouts based on user preferences. This function takes an array of workouts, a user's expertise level, and an optional sport type as input
- Requirements:
  - Returns a filtered array of workouts that match the user's expertise level and sport type (if provided).
  - An error will be thrown if no valid expertise level is given or an invalid sport type is provided.
  - Returns an error when the input is not an array of workout objects.
  - Returns an empty array when the provided expertise level doesn't match any workouts in the given input array.
  - The input array should contain at least one workout with a different expertise level.
- Dummy data reference: Use the dummy data that was generated in the previous step
- Additional instructions:
  - Make the expected result shortened by reusing indexes of dummy data

### Acceptance Criteria:

The generated test cases should cover the following scenarios:
- Correct filtering according to a user's expertise level and sport type (if provided);
- Throwing an error when no valid expertise level is given or an invalid sport type is provided;
- Throwing an error when the input is not an array of workout objects.
- Returning an empty array when the provided expertise level doesn't match any workouts in the input array;
- Utilize the specified testing library you use.

---

### ChatGPT Solution

Here are the Jest unit test cases for the `filterWorkouts` function based on your requirements. Since the function hasn't been written yet, we'll create the tests based on the assumptions provided.

### Dummy Workouts Data
We'll assume an array of workouts with varying expertise levels and sport types:

```javascript
const workouts = [
  { id: 'w1', title: 'Beginner Yoga', expertiseLevel: 1, sport: Sport.Yoga },
  { id: 'w2', title: 'Intermediate Basketball', expertiseLevel: 2, sport: Sport.Basketball },
  { id: 'w3', title: 'Advanced Running', expertiseLevel: 3, sport: Sport.Running },
  { id: 'w4', title: 'Expert Martial Arts', expertiseLevel: 4, sport: Sport.MartialArts },
];
```

### Unit Tests

```javascript
const { filterWorkouts } = require('./path/to/filterWorkouts'); // Adjust import path as necessary

describe('filterWorkouts', () => {
  let workouts;

  beforeEach(() => {
    // Dummy workout data
    workouts = [
      { id: 'w1', title: 'Beginner Yoga', expertiseLevel: 1, sport: Sport.Yoga },
      { id: 'w2', title: 'Intermediate Basketball', expertiseLevel: 2, sport: Sport.Basketball },
      { id: 'w3', title: 'Advanced Running', expertiseLevel: 3, sport: Sport.Running },
      { id: 'w4', title: 'Expert Martial Arts', expertiseLevel: 4, sport: Sport.MartialArts },
    ];
  });

  it('should return workouts matching the user expertise level', () => {
    const result = filterWorkouts(workouts, 1);
    expect(result).toEqual([workouts[0]]);
  });

  it('should return workouts matching the user expertise level and sport type', () => {
    const result = filterWorkouts(workouts, 2, Sport.Basketball);
    expect(result).toEqual([workouts[1]]);
  });

  it('should return an empty array if no workouts match the user expertise level', () => {
    const result = filterWorkouts(workouts, 5);
    expect(result).toEqual([]);
  });

  it('should throw an error if the expertise level is not valid', () => {
    expect(() => filterWorkouts(workouts, 'invalid')).toThrow('Invalid expertise level');
  });

  it('should throw an error if the sport type is not valid', () => {
    expect(() => filterWorkouts(workouts, 2, 'InvalidSport')).toThrow('Invalid sport type');
  });

  it('should throw an error if the input is not an array of workout objects', () => {
    expect(() => filterWorkouts('invalid input', 2)).toThrow('Input must be an array of workouts');
  });

  it('should return an empty array if no expertise levels match', () => {
    const result = filterWorkouts(workouts, 10);
    expect(result).toEqual([]);
  });
});
```

### Explanation of Test Cases:

1. **Matching Expertise Level**: Ensures the function filters workouts correctly based on the given expertise level.
2. **Matching Expertise Level and Sport Type**: Tests filtering with both expertise level and an optional sport type.
3. **No Workouts for Expertise Level**: Verifies that an empty array is returned when no workouts match the provided expertise level.
4. **Invalid Expertise Level**: Tests that the function throws an error if an invalid expertise level is provided.
5. **Invalid Sport Type**: Tests that the function throws an error when an invalid sport type is passed.
6. **Invalid Input Type**: Ensures that the function throws an error if the input is not an array of workout objects.
7. **Empty Result for Non-Matching Expertise**: Ensures the function handles a case where no expertise levels match the input.

These tests provide comprehensive coverage for the function's expected behavior.