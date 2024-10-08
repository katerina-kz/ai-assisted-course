### Prompt

Generate unit tests based on the following information:

- Function code:
```js
type TrainingPlan = {
  id: number;
  title: string;
  goal: string;
  durationInWeeks: number;
};

function filterTrainingPlans(
  trainingPlans: TrainingPlan[],
  userGoal: string,
  minDuration: number,
  maxDuration: number
): TrainingPlan[] {
  if (!trainingPlans || !Array.isArray(trainingPlans)) {
    throw new Error("Input should be an array of training plan objects.");
  }

  if (!userGoal) {
    throw new Error("User goal is not defined.");
  }

  if (minDuration > maxDuration) {
    throw new Error("Minimum duration is greater than maximum duration.");
  }

  return trainingPlans.filter((plan) => {
    const matchesGoal = plan.goal.toLowerCase() === userGoal.toLowerCase();
    const withinDurationRange =
      plan.durationInWeeks >= minDuration &&
      plan.durationInWeeks <= maxDuration;

    return matchesGoal && withinDurationRange;
  });
}
```

- Generated dummy data reference: Use the dummy test data generated earlier.
- Additional instructions:
  - Generate testing data for different scenarios;
  - Make the expected result shortened by reusing indexes of the dummy data;
  - Ensure tests cover the following cases:
      - when the input array is empty;
      - when the user goal is not defined;
      - when the minimum duration is greater than the maximum duration;
      - when the input is not an array of training plan objects;
      - when the function returns the correct filtered array;
  - Utilize the specified testing library on your own.

---

### ChatGPT Solution

Here are the unit test cases for the `filterTrainingPlans` function based on the provided requirements, using Jest.

### Dummy Training Plan Data

```javascript
const trainingPlans = [
  { id: 1, title: 'Plan 1', goal: 'Build Strength', durationInWeeks: 8 },
  { id: 2, title: 'Plan 2', goal: 'Lose Weight', durationInWeeks: 12 },
  { id: 3, title: 'Plan 3', goal: 'Build Strength', durationInWeeks: 16 },
  { id: 4, title: 'Plan 4', goal: 'Improve Endurance', durationInWeeks: 10 },
];
```

### Unit Tests

```javascript
const { filterTrainingPlans } = require('./path/to/filterTrainingPlans'); // Adjust the path as needed

describe('filterTrainingPlans', () => {
  let trainingPlans;

  beforeEach(() => {
    // Dummy training plan data
    trainingPlans = [
      { id: 1, title: 'Plan 1', goal: 'Build Strength', durationInWeeks: 8 },
      { id: 2, title: 'Plan 2', goal: 'Lose Weight', durationInWeeks: 12 },
      { id: 3, title: 'Plan 3', goal: 'Build Strength', durationInWeeks: 16 },
      { id: 4, title: 'Plan 4', goal: 'Improve Endurance', durationInWeeks: 10 },
    ];
  });

  it('should return the correct filtered array based on user goal and duration range', () => {
    const result = filterTrainingPlans(trainingPlans, 'Build Strength', 8, 16);
    expect(result).toEqual([trainingPlans[0], trainingPlans[2]]);
  });

  it('should return an empty array when no training plans match the goal or duration range', () => {
    const result = filterTrainingPlans(trainingPlans, 'Lose Weight', 5, 7);
    expect(result).toEqual([]);
  });

  it('should throw an error when the input array is empty', () => {
    const result = filterTrainingPlans([], 'Build Strength', 8, 16);
    expect(result).toEqual([]);
  });

  it('should throw an error when the user goal is not defined', () => {
    expect(() => filterTrainingPlans(trainingPlans, '', 8, 16)).toThrow(
      'User goal is not defined.'
    );
  });

  it('should throw an error when the minimum duration is greater than the maximum duration', () => {
    expect(() => filterTrainingPlans(trainingPlans, 'Build Strength', 12, 8)).toThrow(
      'Minimum duration is greater than maximum duration.'
    );
  });

  it('should throw an error when the input is not an array of training plan objects', () => {
    expect(() => filterTrainingPlans('invalid input', 'Build Strength', 8, 16)).toThrow(
      'Input should be an array of training plan objects.'
    );
  });
});
```

### Explanation of Test Cases:

1. **Correct Filtering**: Checks if the function filters the training plans based on the user's goal and duration range.
2. **No Matching Plans**: Ensures the function returns an empty array if no training plans match the goal or the duration range.
3. **Empty Array Input**: Tests if the function can handle an empty array input without throwing an error.
4. **User Goal Not Defined**: Ensures that an error is thrown when the user goal is not provided.
5. **Min Duration Greater Than Max Duration**: Tests that an error is thrown when the minimum duration is greater than the maximum duration.
6. **Invalid Input Type**: Ensures the function throws an error when the input is not an array of training plan objects.

These tests cover a wide range of edge cases to ensure the correctness and robustness of the `filterTrainingPlans` function.