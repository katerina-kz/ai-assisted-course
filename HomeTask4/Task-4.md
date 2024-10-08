### Prompt

Write unit tests based on the following information:

Testing purpose: Corner case coverage
Function code:
```js
// This function takes an array of users, a sport type, and a range of
// experience (minimum and maximum years) as input.
// It will return a filtered array of users that match the given sport
// type and have experience within the specified range.
// If no valid sport type is given, or the minimum/maximum years
// constraints are not met, an error will be thrown.

type User = {
 id: number;
 name: string;
 sport: string;
 yearsOfExperience: number;
};

function filterUsersBySportAndExperience(
 users: User[],
 sportType: string,
 minYears: number
 maxYears: number
): User[] {
 if (!users || !Array.isArray(users)) {
  throw new Error("Input should be an array of user objects.");
 }

 if (!sportType) {
  throw new Error("Sport type is not defined.");
 }

 if (minYears > maxYears) {
  throw new Error("Minimum years of experience is greater than maximum years.");
 }

 return users.filter(user => {
  const matchesSportType = user.sport.toLowerCase() === sportType.toLowerCase();
  const withinExperienceRange = user.yearsOfExperience >= minYears &&
user.yearsOfExperience <= maxYears;

  return matchesSportType && withinExperienceRange;
 });
}
```

Existing unit tests:
```js
describe("filterUsersBySportAndExperience", () => {
  const testData: User[] = [
    { id: 1, name: "Alice", sport: "Basketball", yearsOfExperience: 5 },
    { id: 2, name: "Bob", sport: "Soccer", yearsOfExperience: 3 },
    { id: 3, name: "Charlie", sport: "Basketball", yearsOfExperience: 1 },
    { id: 4, name: "David", sport: "Tennis", yearsOfExperience: 4 },
    { id: 5, name: "Eva", sport: "Basketball", yearsOfExperience: 7 },
  ];

  test("should throw error when input is not an array", () => {
    expect(() =>
      filterUsersBySportAndExperience("invalidInput" as any, "Basketball", 3, 5)
    ).toThrow("Iput should be an array of user objects.");
  });

  test("should throw error when sport type is not defined", () => {
    expect(() => filterUsersBySportAndExperience(testData, "", 3, 5)).toThrow(
      "Sport type is not defined."
    );
  });

  test("should throw error when minYears is greater than maxYears", () => {
    expect(() =>
      filterUsersBySportAndExperience(testData, "Basketball", 6, 5)
    ).toThrow("Minimum years of experience is greater than maximum years.");
  });

  test("should return an array with correct users filtered by sport type and experience range", () => {
    const expectedResult = [testData[0], testData[4]];
    expect(
      filterUsersBySportAndExperience(testData, "Basketball", 3, 8)
    ).toEqual(expectedResult);
  });

  test("should return an empty array when no users match the criteria", () => {
    expect(filterUsersBySportAndExperience(testData, "Golf", 3, 5)).toEqual([]);
  });

  test("should handle case-insensitive sport types correctly", () => {
    const expectedResult = [testData[1]];
    expect(filterUsersBySportAndExperience(testData, "sOcCeR", 2, 4)).toEqual(
      expectedResult
    );
  });
});
```

Acceptance Criteria:

- Analyze the provided unit tests for the filterUsersBySportAndExperience function.
- Identify any missing test scenarios, especially corner cases.
- Add or update the unit tests as required.
- Ensure the updated tests follow the provided code style and contain relevant responses.
- Ensure tests cover the following cases:
    - Throw an error when users input is not an array;
    - Throw an error when sport type is not defined;
    - Throw an error when minYears is greater than maxYears;
    - Return an array with correct users filtered by sport type and experience range;
    - Return an empty array when no users match the criteria;
    - Handle case-insensitive sport types correctly;

---

### ChatGPT Solution

Here’s an enhanced set of unit tests for the `filterUsersBySportAndExperience` function, including corner case coverage and analysis of the existing tests:

### Additional Corner Cases:
1. **Negative `minYears` and `maxYears` values**: Ensure that negative values for experience years are handled properly.
2. **Zero `minYears` or `maxYears` values**: Check that zero is treated as a valid number of experience years.
3. **Empty `users` array**: Ensure the function handles an empty array without throwing errors.
4. **Identical `minYears` and `maxYears`**: Validate behavior when `minYears` and `maxYears` are the same.

### Updated Unit Tests

```javascript
describe("filterUsersBySportAndExperience", () => {
  const testData: User[] = [
    { id: 1, name: "Alice", sport: "Basketball", yearsOfExperience: 5 },
    { id: 2, name: "Bob", sport: "Soccer", yearsOfExperience: 3 },
    { id: 3, name: "Charlie", sport: "Basketball", yearsOfExperience: 1 },
    { id: 4, name: "David", sport: "Tennis", yearsOfExperience: 4 },
    { id: 5, name: "Eva", sport: "Basketball", yearsOfExperience: 7 },
  ];

  test("should throw error when input is not an array", () => {
    expect(() =>
      filterUsersBySportAndExperience("invalidInput" as any, "Basketball", 3, 5)
    ).toThrow("Input should be an array of user objects.");
  });

  test("should throw error when sport type is not defined", () => {
    expect(() => filterUsersBySportAndExperience(testData, "", 3, 5)).toThrow(
      "Sport type is not defined."
    );
  });

  test("should throw error when minYears is greater than maxYears", () => {
    expect(() =>
      filterUsersBySportAndExperience(testData, "Basketball", 6, 5)
    ).toThrow("Minimum years of experience is greater than maximum years.");
  });

  test("should throw error when minYears or maxYears are negative", () => {
    expect(() =>
      filterUsersBySportAndExperience(testData, "Basketball", -1, 5)
    ).toThrow("Years of experience cannot be negative.");
    
    expect(() =>
      filterUsersBySportAndExperience(testData, "Basketball", 3, -1)
    ).toThrow("Years of experience cannot be negative.");
  });

  test("should return an array with correct users filtered by sport type and experience range", () => {
    const expectedResult = [testData[0], testData[4]];
    expect(
      filterUsersBySportAndExperience(testData, "Basketball", 3, 8)
    ).toEqual(expectedResult);
  });

  test("should return an empty array when no users match the criteria", () => {
    expect(filterUsersBySportAndExperience(testData, "Golf", 3, 5)).toEqual([]);
  });

  test("should handle case-insensitive sport types correctly", () => {
    const expectedResult = [testData[1]];
    expect(filterUsersBySportAndExperience(testData, "sOcCeR", 2, 4)).toEqual(
      expectedResult
    );
  });

  test("should return an empty array when the users array is empty", () => {
    expect(filterUsersBySportAndExperience([], "Basketball", 3, 5)).toEqual([]);
  });

  test("should handle zero years of experience correctly", () => {
    const zeroExperienceData = [
      { id: 6, name: "Frank", sport: "Tennis", yearsOfExperience: 0 },
    ];

    expect(
      filterUsersBySportAndExperience(zeroExperienceData, "Tennis", 0, 1)
    ).toEqual([zeroExperienceData[0]]);
  });

  test("should return users when minYears equals maxYears", () => {
    const expectedResult = [testData[0]];
    expect(filterUsersBySportAndExperience(testData, "Basketball", 5, 5)).toEqual(expectedResult);
  });
});
```

### Summary of Corner Case Coverage:
1. **Negative Years**: Added a test case to ensure negative values for `minYears` and `maxYears` throw an error.
2. **Zero Years**: Added a test case to check how the function handles users with zero experience.
3. **Empty Array**: Added a test to check that the function works with an empty input array without errors.
4. **Identical `minYears` and `maxYears`**: Added a case to test when `minYears` equals `maxYears`.

These new cases strengthen the original tests, covering various edge conditions.