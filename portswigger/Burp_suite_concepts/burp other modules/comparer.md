## Introduction
_Comparer_ allows us to compare two pieces of data, either by ASCII words or by bytes.
![[burp_basics24.png]]

**This interface can be split into three main parts:**
1. On the left, we have the items being compared. When we load data into Comparer, it will appear as rows in these tables.
2. On the upper right, we have options for pasting data in from the clipboard (Paste), loading data from a file (Load), removing the current row (Remove) and clearing all datasets (Clear).
3. Finally, on the bottom right, we have the option to compare our datasets by either words or bytes. Don't worry about which of these buttons you select as this can be changed later on.

**When we have loaded data in to compare, we get a pop-up window showing us the comparison:**
![[burp_basics25.png]]
**there are three distinct parts to this window:**
1. The compared data takes up most of the window; this can be viewed in either text or hex format.
2. The key for comparisons is at the bottom left, showing which colours denote modified, deleted, and added data between the two datasets.
3. "Sync views" when selected, this means that both sets of data will sync formats -- i.e. if you change one of them into Hex view, the other will do the same to match.
