### Prompt

Help me to fix the following failing test by modifying the test:

Function code:
```js
export interface Workout {
  id: number;
  durationMinutes: number;
  caloriesBurned: number;
  date: Date;
  trainingPlanId: number;
}

export function calculateWeeklyCaloriesBurned(
  workouts: Workout[],
  weekStartDate: Date,
  trainingPlanId: number
): number {
  const oneDayInMilliseconds = 86400000;
  const oneWeekInMilliseconds = oneDayInMilliseconds * 7;
  const weekEndDate = new Date(weekStartDate.getTime() + oneWeekInMilliseconds);
  const weeklyWorkouts = workouts.filter(
    (workout) =>
      workout.trainingPlanId === trainingPlanId &&
      workout.date >= weekStartDate &&
      workout.date < weekEndDate
  );

  return weeklyWorkouts.reduce(
    (totalCalories, workout) => totalCalories + workout.caloriesBurned,
    0
  );
}
```

Failed test code:
```js
const mockWorkouts: Workout[] = [
  {
    id: 1,
    durationMinutes: 60,
    caloriesBurned: 500,
    date: new Date("2022-01-01"),
    trainingPlanId: 1,
  },
  {
    id: 2,
    durationMinutes: 45,
    caloriesBurned: 300,
    date: new Date("2022-01-02"),
    trainingPlanId: 1,
  },
  {
    id: 3,
    durationMinutes: 30,
    caloriesBurned: 200,
    date: new Date("2021-12-25"),
    trainingPlanId: 1,
  },
  {
    id: 4,
    durationMinutes: 60,
    caloriesBurned: 400,
    date: new Date("2022-01-01"),
    trainingPlanId: 2,
  },
];

test("should calculate the total calories burned for a specific week", () => {
  const result = calculateWeeklyCaloriesBurned(
    mockWorkouts,
    new Date("2021-12-31"),
    1
  );
  expect(result).toBe(700);
});
```
});

Error: 

```
should calculate the total calories burned for a specific week.

Expected: 700
Received: 800
```

Acceptance Criteria:

- Correct and update the test case to ensure it adequately tests the function's behavior;
- Validate that the updated test case passes and accurately reflects the function's intended output.


---

### ChatGPT Solution

The issue with the test is that the current workout on `2022-01-01` is counted twice—once for training plan ID 1 (500 calories burned) and once for training plan ID 2 (400 calories burned). This results in 800 calories being counted instead of 700.

To fix the test, modify the date range for the `weekStartDate` so that it accurately reflects the week you want to test, excluding the workout with `trainingPlanId` 2.

Here's the corrected test case:

```ts
test("should calculate the total calories burned for a specific week", () => {
  const result = calculateWeeklyCaloriesBurned(
    mockWorkouts,
    new Date("2021-12-31"),
    1
  );
  expect(result).toBe(800);
});
```

Explanation: The workout with `trainingPlanId: 1` on `2022-01-01` burns 500 calories, and the workout on `2022-01-02` burns 300 calories, for a total of 800 calories. Both are in the same week range, so the expected result should be 800, not 700.