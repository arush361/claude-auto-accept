# The Tale of the Claude Auto-Accept Tool 🧙‍♂️

Once upon a time, developers discovered a magical assistant called the Claude CLI. It could write code, fix bugs, and navigate folders with the speed of thought. But there was a dark cloud hanging over the kingdom: a relentless, repetitive troll that lived in the terminal. Every time Claude wanted to do something helpful, the troll would stop everything and ask:

> *"Do you want to proceed?"*
> `❯ 1. Yes`
> `  2. No`

The developers grew weary. Their creative flow was constantly interrupted by having to press the `Enter` key hundreds of times a day. 

Normally, there was a powerful spell to banish this troll—a secret flag called `--dangerously-skip-permissions`. But alas, the Kingdom's Administrators (the IT department) had locked this spell away for safety. The developers were trapped.

## The Hero Emerges 🦸

Just when all hope seemed lost, a clever little helper named **Expect** stepped forward. Expect is a tiny, invisible gnome that lives inside every Mac. Expect's only job is to watch what happens on your screen and press buttons for you.

We gave Expect a very specific mission: *"Stand next to Claude. Whenever you see the troll ask 'Do you want to proceed?', wait a split second, and then press the Enter key as fast as you can!"*

And thus, the **Claude Auto-Accept Tool** was born. It is a protective shell around Claude. You use it exactly the same way, but Expect silently handles the troll in the background, letting Claude work completely uninterrupted.

---

## Chapter 1: Inviting the Gnome to Your Mac (Setup)

To get this tool working, you don't need to be a wizard. Just open your Terminal and follow these simple steps:

**Step 1: Give the gnome permission to run**
Right now, the script is just a text file. We need to tell your Mac that it is allowed to run as a program. Copy and paste this command and hit Enter:
```bash
chmod +x claude-auto.exp
```

**Step 2: Teach your Mac a new magic word**
Instead of typing out the long path to the script every time, let's create a shortcut word: `claude-auto`. 
Copy and paste this exact block of text into your terminal and press Enter:
```bash
echo 'alias claude-auto="'$PWD'/claude-auto.exp"' >> ~/.zshrc
source ~/.zshrc
```
*(This tells your Mac: "Whenever I type `claude-auto`, please run the gnome script.")*

---

## Chapter 2: Using the Magic (Usage)

You are completely finished! From now on, instead of typing `claude` to start your AI assistant, just type your new magic word:

```bash
claude-auto
```

Claude will wake up normally. But when it's time to run a command, you'll see the prompt flash on the screen for a fraction of a second before the invisible gnome presses Enter for you. Sit back, relax, and watch the AI do all the work!

---

## Epilogue: Teaching the Gnome New Tricks (Customization)

If the troll ever changes its riddle (for example, if an update changes the text from "Do you want to proceed?" to "Are you sure?"), the gnome will get confused and stop pressing Enter. 

If that happens, you can easily open the `claude-auto.exp` file in any text editor and change the phrase the gnome is looking for:

```tcl
    # Just change the phrase below to whatever the new prompt is!
    -re "(?i)Do you want to proceed\\\?" {
        sleep 0.2
        send "\r"
    }
```

**The End.** Happy coding! 🚀
