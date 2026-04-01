# GitHub Copilot Usage Guide for OOPtutorials

## Starting a New Copilot Chat Session

If your Copilot chat has disappeared or you need to start fresh, don't worry! Here's how to restart and continue your work:

### 1. Opening a New Chat

**In VS Code:**
- Press `Ctrl+Shift+I` (Windows/Linux) or `Cmd+Shift+I` (Mac) to open Copilot Chat
- Alternatively, click on the chat icon in the Activity Bar on the left side
- Or use the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) and type "GitHub Copilot: Open Chat"

**In GitHub.com:**
- Navigate to your repository
- Click on the Copilot icon in the top right corner
- Select "Start new chat"

### 2. Restoring Context

When you start a new chat session, Copilot won't have the context from your previous conversation. Here's how to quickly restore context:

#### Provide Repository Context
```
I'm working on the OOPtutorials repository. This is a collection of 
Object-Oriented Programming tutorial documents for Java, aimed at 
students learning OOP concepts.
```

#### Reference Specific Files
If you were working on a specific tutorial, open the file and reference it:
```
I'm working on the [filename].md tutorial. Can you help me continue 
with [specific task]?
```

#### Share Your Goal
Clearly state what you're trying to achieve:
```
I need to [add/update/fix] [specific content] in the [specific tutorial]. 
Previously, we were discussing [topic].
```

### 3. Best Practices for Working with Copilot

#### Keep Context Fresh
- **Open relevant files** in your editor before asking Copilot questions
- **Use @workspace** to refer to your entire repository
- **Use @filename** to refer to specific files

#### Be Specific
Instead of:
```
How do I continue?
```

Try:
```
I'm updating the ArraysAndArrayLists.md tutorial. I need to add 
a section about ArrayList methods. Can you help draft content 
explaining add(), remove(), and get() methods?
```

#### Save Your Progress Frequently
- Commit your changes regularly with descriptive messages
- This helps you (and Copilot) understand what's been done
- Use: `git commit -m "Descriptive message about changes"`

### 4. Common Scenarios

#### Scenario: Lost Chat Mid-Edit

**What to do:**
1. Check what files you've modified: `git status`
2. Review your changes: `git diff`
3. Open a new Copilot chat
4. Share: "I was editing [file]. Here's what I've changed so far: [brief description]. I need to [next task]."

#### Scenario: Can't Remember What You Were Working On

**What to do:**
1. Check your git log: `git log --oneline -5`
2. Look at recent changes: `git diff HEAD~1`
3. Review uncommitted changes: `git diff`
4. Tell Copilot: "Based on my recent commits and changes, what should I work on next?"

#### Scenario: Need to Continue Someone Else's Work

**What to do:**
1. Review the pull request or issue comments
2. Check recent commits related to the task
3. Tell Copilot: "I'm continuing work on [issue/PR]. The previous work included [summary]. I need to [next steps]."

### 5. Repository-Specific Tips

#### For This Repository (OOPtutorials):

- **Consistency**: Check existing tutorials for formatting and style before adding new content
- **Target Audience**: Remember these are for students learning Java OOP concepts
- **Code Examples**: Focus on Java examples; include Python comparisons only when helpful for context
- **Clarity**: Aim for clear, concise explanations

#### Example Prompts for This Repository:

```
Help me add a new section to ClassesAndObjects.md about [topic], 
following the existing style and format.
```

```
Review the Methods.md file and suggest improvements for clarity 
for students new to Java.
```

```
I need to create a new tutorial about [topic]. Can you help me 
structure it similar to the existing tutorials?
```

### 6. Recovering from Issues

#### If Copilot Gives Incorrect Suggestions:
- Provide feedback: "That's not quite right. I need [clarification]."
- Give context: "This repository focuses on [specific aspect]."
- Show examples: "Like in JavaPrimer.md, we use [approach]."

#### If You're Stuck:
- Break down the task: "Let's start with just [small part]."
- Ask for options: "What are different ways to [accomplish task]?"
- Request step-by-step: "Can you break this down into steps?"

### 7. Quick Reference Commands

```bash
# Check what you've changed
git status
git diff

# See recent history
git log --oneline -10

# Undo changes to a file (if needed)
git restore filename.md

# Create a new branch for your work
git switch -c your-branch-name

# Save your work
git add .
git commit -m "Your message"
git push
```

### 8. Getting Help

If you're stuck and Copilot isn't helping:
1. Check the README.md for project information
2. Review existing tutorials for patterns and examples
3. Contact the maintainer: d.mullier@leedsbeckett.ac.uk
4. Check GitHub issues for similar questions

---

## Summary

When your Copilot chat disappears:
1. ✅ Open a new chat (Ctrl+Shift+I or Cmd+Shift+I)
2. ✅ Provide context about what you're working on
3. ✅ Reference specific files and goals
4. ✅ Use git commands to understand your current state
5. ✅ Be specific in your requests

Remember: Copilot is a tool to assist you, but you're in control. 
Always review its suggestions and ensure they align with the 
repository's goals and style!
