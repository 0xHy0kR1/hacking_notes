- Data Execution Prevention (DEP) is a special tool that helps keep your computer safe from bad programs that might try to harm it.
- Imagine you have a room where you keep all your toys. Sometimes, a new toy might look fun to play with, but it could be dangerous and might break some of your other toys. DEP works like a toy inspector.
# In technical way - 
- DEP works by separating a computer's memory into two parts: one part for storing data and one part for storing executable code. Data, such as pictures and documents, is stored in the data section of memory, while code that programs run, such as instructions to open a file or display an image, is stored in the code section.
- DEP checks to make sure that code is only run in the code section of memory. If a program tries to run code in the data section of memory, DEP stops it and shows a warning message to the user.
- This helps protect your computer from certain types of attacks, such as [[buffer overflow ]]attacks, which can trick a program into running code in the data section of memory.
- DEP is enabled by default in Windows, but it can be turned off or configured for specific programs.