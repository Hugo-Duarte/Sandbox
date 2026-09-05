Stage 2 — Controlled defect

Date - 05-09-2026
Time spent - 15m

Observed lifecycle order 
    1. Game1() Constructor
    2. Initialize()
    3. LoadContent()
    4. Update()
    5. Draw()
    6. Update()
    7. Draw()
    and so on until exit.

Methods executed once:
    1. Game1() Constructor
    2. Initialize()
    3. LoadContent()

Methods executed repeatedly
    1. Update()
    2. Draw()

Meaning of ElapsedGameTime - Duration of the current loop step

Meaning of TotalGameTime - Total time since game started

What the Update and Draw call stacks showed - That they repeat

Your controlled-defect prediction:
- Will compilation succeed? No
- If it runs, approximately when will it fail? At Initialize
- What service do you think will be unavailable? Graphics drawing to the screen

Actual exception type and message:
Type -  System.InvalidOperationException
Message - 'No Graphics Device Service'


Where the exception became visible
At G:\code\Sandbox\Sandbox\Program.cs:line 2

Actual root cause
- Could not use the service graphics device since it had not been initialisedd

Confirmation that you restored the graphics manager and the game runs again
- yes

Anything that remains uncertain
- No
