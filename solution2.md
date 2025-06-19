# Solution nested votes and vote types
```JS
import { useState } from "react";
import './App.css'

interface VoteCount {
  up: number;
  down: number;
}

interface Votes {
  Readability: VoteCount;
  Performance: VoteCount;
  Security: VoteCount;
  Documentation: VoteCount;
  Testing: VoteCount;
}

function App() {
  const [votes, setVotes] = useState<Votes>({
    Readability: { up: 0, down: 0 },
    Performance: { up: 0, down: 0 },
    Security: { up: 0, down: 0 },
    Documentation: { up: 0, down: 0 },
    Testing: { up: 0, down: 0 }
  });

  function handleVote(aspect: keyof Votes, voteType: 'up' | 'down') {
    setVotes(prev => ({
      ...prev,
      [aspect]: {
        ...prev[aspect],
        ...(voteType === 'up'
          ? { up: prev[aspect].up + 1 }
          : { down: prev[aspect].down + 1 })
      }
    }));
  }

  const aspects: (keyof Votes)[] = ['Readability', 'Performance', 'Security', 'Documentation', 'Testing'];

  return (
    <div>
      <h1>Code Review Feedback</h1>
      
      {aspects.map(aspect => (
        <div key={aspect}>
          <h3>{aspect}</h3>
          <button onClick={() => handleVote(aspect, 'up')}>Upvote</button>
          <span>{votes[aspect].up}</span>
          <br />
          <button onClick={() => handleVote(aspect, 'down')}>Downvote</button>
          <span>{votes[aspect].down}</span>
        </div>
      ))}
    </div>
  );
}

export default App;

```
## The Complete Function
```jsx
function handleVote(aspect, type) {
  setVotes(prev => ({
    ...prev,
    [aspect]: {
      ...prev[aspect],
      [type]: prev[aspect][type] + 1
    }
  }));
}
```

## Step-by-Step Breakdown

### Step 1: Function Parameters
```jsx
function handleVote(aspect, type)
```
- `aspect` = which aspect (like 'Readability', 'Performance')
- `type` = 'up' or 'down'

### Step 2: setVotes with prev
```jsx
setVotes(prev => ({
```
- `prev` = the current state object
- Example of what `prev` looks like:
```jsx
{
  Readability: { up: 2, down: 1 },
  Performance: { up: 0, down: 0 },
  Security: { up: 1, down: 0 },
  Documentation: { up: 0, down: 0 },
  Testing: { up: 0, down: 0 }
}
```

### Step 3: Spread Operator (...prev)
```jsx
...prev,
```
- This copies ALL existing aspects
- Keeps Performance, Security, Documentation, Testing unchanged

### Step 4: Target Specific Aspect
```jsx
[aspect]: {
```
- If `aspect = 'Readability'`, this becomes `Readability: {`
- We're about to update just this one aspect

### Step 5: Spread the Aspect's Current Values
```jsx
...prev[aspect],
```
- If `prev[aspect]` is `{ up: 2, down: 1 }`
- This copies both `up: 2` and `down: 1`

### Step 6: Update the Specific Vote Type
```jsx
[type]: prev[aspect][type] + 1
```
- If `type = 'up'` and `prev[aspect][type] = 2`
- This becomes `up: 2 + 1` = `up: 3`

## Complete Example

**Before clicking:** `aspect = 'Readability'`, `type = 'up'`
```jsx
prev = {
  Readability: { up: 2, down: 1 },
  Performance: { up: 0, down: 0 },
  Security: { up: 1, down: 0 }
}
```

**After the function runs:**
```jsx
{
  ...prev,                    // Copy Performance, Security, etc.
  Readability: {              // Update Readability
    ...prev[aspect],          // Copy up: 2, down: 1
    up: prev[aspect][up] + 1  // up: 2 + 1 = 3
  }
}
```

**Result:**
```jsx
{
  Readability: { up: 3, down: 1 },  // up increased by 1
  Performance: { up: 0, down: 0 },  // unchanged
  Security: { up: 1, down: 0 }      // unchanged
}
```

## Key Points to Remember

1. **We never modify the original state directly** - React state is immutable
2. **We create a new object** by copying the old one and updating just one value
3. **The spread operator (...)** copies all existing properties
4. **Dynamic property names [aspect]** let us target any aspect dynamically
5. **Nested spread operators** handle the nested object structure

## Why This Pattern?

This is the standard React pattern for updating nested state objects. It ensures:
- State immutability (React requirement)
- Only the changed part gets re-rendered
- All other data remains unchanged 