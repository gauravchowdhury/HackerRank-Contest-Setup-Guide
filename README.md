# HackerRank Contest Setup Guide

This repository documents a reproducible, modular workflow for organising programming contests on [HackerRank](https://www.hackerrank.com). It includes setup steps, test case strategies, AI-assisted workflows, dry-run checklists, and post-contest analysis.

## Why This Exists

HackerRank’s setup flow can sometimes be under-documented or confusing. This guide captures refined steps to make contest creation and administration easier — including the use of AI for test case generation and sanity checks.

## Contest Creation Workflow

### 1. Account Creation

- Visit [HackerRank](https://www.hackerrank.com) and create a developer account.
  
- Log in to your new account.

### 2. Setup

- Click on your **Profile Icon** → go to **Administration**.
  
- Navigate to **Manage Challenges** to create a new challenge → See [Challenge Setup](#challenge-setup).
  
- Then go to **Manage Contests** to create a new contest → See [Contest Setup](#contest-setup).

### 3. Testing

- Test each challenge with both **correct** and **incorrect** solutions across all allowed languages.
  
- Ensure test cases cover:
  
  - Edge cases
    
  - Typical inputs
    
  - Invalid inputs
    
-  Verify that problem constraints and output formats are enforced

### 4. Results

- After the contest, extract:
  
  - **Leaderboard**
    
  - **Submission logs**
    
- Analyse submissions for correctness, efficiency, and adherence to constraints.
  
- See [Results](#results) for details.

## Challenge Setup

### 1. Details

- **Language**: Select the challenge language (e.g., English).
  
- **Difficulty**: Choose an appropriate difficulty level (Easy, Medium, Hard).
  
- **Boilerplate Metadata**:
  
  - Use the following format to structure your problem metadata:
    
    ```
    Challenge Name: <Your Title>
    Challenge Slug: <URL-friendly identifier>
    Description: <Short overview of the challenge>
    Problem Statement: <Formal statement of the task>
    Input Format: <How input is provided>
    Constraints: <Limits on input values>
    Output Format: <Expected output format>
    ```
    
  - Paste this format into an AI tool and ask it to convert your raw problem (including sample input/output and constraints) into a clean, contest-ready format.
    
- **Tags**: Add relevant tags (e.g., recursion, sorting, greedy) to help categorise the challenge.

### 2. Test Cases

Use the following Python script as a **template for generating reproducible test cases**:

```python
import os
import random

# --- Configuration ---
NUM_TESTS = 100
INPUT_FOLDER = "testcase/input"
OUTPUT_FOLDER = "testcase/output"

os.makedirs(INPUT_FOLDER, exist_ok=True)
os.makedirs(OUTPUT_FOLDER, exist_ok=True)

# --- Problem-specific functions ---
def generate_input():
    """
    Modify this function to generate a single test case input.
    Return as a string exactly as expected in the input file.
    """
    n = random.randint(1, 10)
    arr = [random.randint(1, 100) for _ in range(n)]
    return f"{n}\n{' '.join(map(str, arr))}\n"

def solve_problem(input_str):
    """
    Modify this function to solve the problem.
    Takes input string and returns output string exactly as expected in output file.
    """
    lines = input_str.strip().split("\n")
    n = int(lines[0])
    arr = list(map(int, lines[1].split()))
    result = sum(arr)  # Example logic
    return f"{result}\n"

# --- Test case generation ---
for i in range(1, NUM_TESTS + 1):
    input_data = generate_input()
    output_data = solve_problem(input_data)

    with open(os.path.join(INPUT_FOLDER, f"input{i:02d}.txt"), "w") as f:
        f.write(input_data)
    with open(os.path.join(OUTPUT_FOLDER, f"output{i:02d}.txt"), "w") as f:
        f.write(output_data)

print(f"Generated {NUM_TESTS} test cases in '{INPUT_FOLDER}' and '{OUTPUT_FOLDER}'.")
```

#### AI-Assisted Adaptation

To tailor this script to your specific challenge:

1. **Paste your finalized problem metadata** (from the previous step) into an AI tool.

2. **Ask the AI to:**
   
   - Modify `generate_input()` to match your input format and constraints.
     
   - Implement `solve_problem()` to compute the correct output for each test case.

3. **Run the script locally** to generate `inputXX.txt` and `outputXX.txt` files.

4. **Verify the structure and correctness** of the generated test cases.

5. **Zip the `testcase/` folder** and upload it to HackerRank.

6. **Select 1–3 sample test cases** to be displayed alongside the problem on the challenge page.

### 3. Code Stubs

- Use starter code for each supported language to guide participants.
  
- To generate problem-specific code stubs, follow these steps:

1. Visit the [Code Stub Generator Gist](https://gist.github.com/Shafaet/86afa48a54ae1d5dc46fa80542d7b10a).
   
2. Copy the link into an AI tool along with your **problem details** (metadata, input/output format, constraints).
   
3. Ask the AI to produce **domain-specific language (DSL) code stubs** tailored to your problem.
   
4. Review and adjust the generated stubs if necessary, ensuring:
   
   - Correct input/output handling
     
   - Matching the problem’s test cases
     
   - Appropriate comments and placeholders for participants to implement their logic

> This approach saves time and ensures consistency across multiple programming languages.

### 4. Languages

- Select the compilers for the programming languages you want to allow during the contest.
  
- Ensure that each language has a matching **code stub** and works correctly with your **test cases**.
  
- Common choices include: Python, C, C++, Java
    
- Double-check that input/output formats in code stubs match your problem statement for each language.

## Contest Setup

Once all challenges are created and validated, you can set up a contest.

### 1. Create a New Contest

- Go to **Manage Contests** under **Administration**.
  
- Click **Create New Contest**.

### 2. Fill Contest Details

- **Contest Name** – Choose a clear, descriptive name.
  
- **Contest URL/Slug** – Make it easy to remember and share.
  
- **Start Time & End Time** – Schedule appropriately, accounting for participant availability.
  
- **Organization Type & Name** – Specify your organization for proper branding.
  
- **Landing Page Customization**:
  
  - Background image
    
  - Tagline
    
  - Contest description
    
  - Prizes (if any)
    
  - Rules and scoring
    
- **Tip:** Not all fields are mandatory, but filling them improves participant experience.
  
- **Efficiency Tip:** Many of these details can be recycled across contests with minimal changes.

### 3. Add Challenges

- Select challenges you have already created.
  
- Assign points and weightage for each challenge.
  
- Configure the number of visible sample test cases for participants.
  
- Verify that challenges pass all dry-run tests before publishing.

### 4. Review and Publish

- Double-check timing, challenges, and scoring.
  
- Run internal dry-runs to ensure everything works as expected.
  
- Publish the contest or save it as a draft for further verification.

## Results

After the contest concludes, collect and analyse results for scoring, feedback, and future improvements.

### 1. Collect Contest Data

- **Leaderboard** – Extract the final rankings of participants.
  
- **Submission Logs** – Extract all submissions for review and analysis.

> **Note:** Free developer accounts may not provide a direct download option. If exports are unavailable:
>
> 1. Use the UI to manually copy the visible rows from the leaderboard and submission log pages.
>
> 3. Be mindful of pagination and ensure all relevant data is captured.
>    
> 5. Paste the copied data into a local editor or trusted tool for formatting.
>    
> 7. If using external AI tools to help format the data, first remove or anonymise any personally identifiable information (e.g., names, emails) and ensure you have permission to share it.
>    
> 9. Validate the final CSVs against the original UI to ensure accuracy.

### 2. Process Leaderboard & Submission Logs

- **Reorder leaderboard** in descending order by score.
  
  > By default, participants with the same score may have the same rank; reordering ensures proper ranking.
   
- **Filter submission logs** to remove any submissions made **after the contest duration**.
  
- Verify the correctness of submissions and handle edge cases or constraint violations.
  
- Identify common mistakes or patterns in wrong submissions.
  
> **Tip:** Both reordering the leaderboard and filtering submission logs can also be done directly using an AI tool, saving time and effort.

### 3. Post-Contest Actions

- Archive contest data (leaderboard, submissions, test cases) for record-keeping.
   
- Use insights to improve future contests, such as:
  
  - Adjusting problem difficulty
    
  - Refining test cases or validators
    
  - Updating code stubs and sample inputs  
