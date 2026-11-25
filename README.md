# ExpNo:10 Implementation of Classical Planning Algorithm
# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```

## Program : 
```PYTHON
# ExpNo 10 : Implementation of Classical Planning Algorithm
# Name:
# Register Number:

from collections import deque

def is_goal_reached(state, goal_state):
    return all(state.get(k) == v for k, v in goal_state.items())

def is_applicable(state, precondition):
    return all(state.get(k) == v for k, v in precondition.items())

def apply_action(state, effect):
    new_state = state.copy()
    new_state.update(effect)
    return new_state

def find_plan(initial_state, goal_state, actions):
    # Forward state-space search using Breadth-First Search (BFS)
    queue = deque([(initial_state, [])])
    visited = {tuple(sorted(initial_state.items()))}

    while queue:
        current_state, plan = queue.popleft()

        if is_goal_reached(current_state, goal_state):
            return plan

        for action_name, details in actions.items():
            if is_applicable(current_state, details['precondition']):
                next_state = apply_action(current_state, details['effect'])
                state_key = tuple(sorted(next_state.items()))

                if state_key not in visited:
                    visited.add(state_key)
                    queue.append((next_state, plan + [action_name]))

    return None

# --- Example 1 ---
initial_state_1 = {'A': 'Table', 'B': 'Table'}
goal_state_1 = {'A': 'B', 'B': 'Table'}

actions_1 = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

print("Example 1 Plan:", find_plan(initial_state_1, goal_state_1, actions_1))

# --- Example 2 ---
initial_state_2 = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state_2 = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions_2 = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

print("Example 2 Plan:", find_plan(initial_state_2, goal_state_2, actions_2))
```
## Output :

<img width="602" height="230" alt="image" src="https://github.com/user-attachments/assets/a55adff6-9837-409f-8770-537f1fafa9d8" />


## Result :
Thus, the Classical Planning Algorithm was successfully implemented to generate the sequence of actions from the initial state to the goal state, and the output was verified successfully.
