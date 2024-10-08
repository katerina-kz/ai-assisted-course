### Prompt

I need dummy test data based on the following details:

- Web application: the VirtualCoach web application, which allows users to access personalized training plans, workout routines, and expert advice from certified coaches, you are required to generate test data for user profiles within the application
- Data type: An array of 5 User objects and one separate User object for testing purposes around the application.
- Array length: 3
- Model details:

```js
enum Gender {
  Male,
  Female,
  Other,
}

enum Sport {
  Basketball,
  Soccer,
  Tennis,
  Running,
  Swimming,
  Cycling,
  Yoga,
  Weightlifting,
  Boxing,
  MartialArts,
}

type User = {
  id: string;
  email: string;
  username: string;
  password: string;
  fullName: string;
  gender: Gender;
  primarySport: Sport;
  interests: Sport[];
  trainingPlanID: string;
  performanceMetrics: {
    currentLevel: number;
    targetLevel: number;
    improvementRate: number;
  };
  premiumUser: boolean;
  age: number;
};
```

### Acceptance Criteria:

- The ChatGPT prompt should effectively present the task of generating dummy data for the User objects and clearly convey the requirements and constraints.
- The generated test data should:
  - be an array of 5 User objects and one separate User object.
  - use realistic values for all properties of the User objects.
  - cover various combinations of properties and values within the User type, such as different genders, sports, and performance metrics.
---

### ChatGPT Solution

Here’s the dummy test data for the VirtualCoach web application based on the provided model:

### Test Data Array (3 User Objects)
```javascript
const users = [
  {
    id: 'user-001',
    email: 'john.smith@test.com',
    username: 'john_smith',
    password: 'password123',
    fullName: 'John Smith',
    gender: Gender.Male,
    primarySport: Sport.Basketball,
    interests: [Sport.Cycling, Sport.Weightlifting, Sport.Yoga],
    trainingPlanID: 'plan-001',
    performanceMetrics: {
      currentLevel: 3,
      targetLevel: 5,
      improvementRate: 1.2,
    },
    premiumUser: true,
    age: 28,
  },
  {
    id: 'user-002',
    email: 'emily.jones@test.com',
    username: 'emily_jones',
    password: 'password456',
    fullName: 'Emily Jones',
    gender: Gender.Female,
    primarySport: Sport.Swimming,
    interests: [Sport.Running, Sport.Cycling, Sport.Boxing],
    trainingPlanID: 'plan-002',
    performanceMetrics: {
      currentLevel: 4,
      targetLevel: 6,
      improvementRate: 1.5,
    },
    premiumUser: false,
    age: 32,
  },
  {
    id: 'user-003',
    email: 'alex.taylor@test.com',
    username: 'alex_taylor',
    password: 'password789',
    fullName: 'Alex Taylor',
    gender: Gender.Other,
    primarySport: Sport.MartialArts,
    interests: [Sport.Boxing, Sport.Tennis, Sport.Running],
    trainingPlanID: 'plan-003',
    performanceMetrics: {
      currentLevel: 2,
      targetLevel: 4,
      improvementRate: 0.8,
    },
    premiumUser: true,
    age: 24,
  },
];
```

### Separate Test User Object
```javascript
const testUser = {
  id: 'user-test-001',
  email: 'test.user@test.com',
  username: 'test_user',
  password: 'testpassword123',
  fullName: 'Test User',
  gender: Gender.Female,
  primarySport: Sport.Yoga,
  interests: [Sport.Weightlifting, Sport.Swimming, Sport.Cycling],
  trainingPlanID: 'plan-test-001',
  performanceMetrics: {
    currentLevel: 5,
    targetLevel: 7,
    improvementRate: 1.3,
  },
  premiumUser: false,
  age: 30,
};
```

This test data includes user profiles with different attributes like gender, primary sports, interests, performance metrics, and premium status to cover various cases during testing.