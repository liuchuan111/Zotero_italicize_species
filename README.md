This is the updated `README.md` content, incorporating the new features, simplifying the procedure, and adding a note about community maintenance.

***

# :sparkles: Italicize Genus and Species Names in Zotero (Community Fork) :sparkles:

This repository presents a streamlined procedure to automatically *italicize* species names (or any other word) in the titles of your documents in your Zotero library.

---
## Community Fork Notice

This repository is a **community-maintained fork** of the original Zotero italicization script by LPDagallier/Zotero_italicize_species.

Since the original project appears inactive, this fork provides crucial **stability and usability enhancements**, including preventing nested italic tags and adding a dedicated cleanup utility. Users are encouraged to use this version for continued maintenance and bug fixes.

---

---

##  Key Optimizations in This Fork

This version of the script includes crucial logic enhancements to improve stability and usability:

1.  **Nesting Prevention:** The script now features an advanced **pre-check** to prevent the creation of incorrect nested HTML tags (e.g., `<i><i>Genus</i> species</i>`), ensuring clean and correct formatting even when running the script multiple times.
2.  **Cleanup Utility:** A new variable, `toDelete`, allows users to easily specify words or phrases to **remove** existing incorrect or redundant italic tags (`<i>` and `</i>`).

---

##  Introduction

[Zotero](https://www.zotero.org/) is a powerful bibliography management tool. However, correctly formatting scientific names often requires manual effort:

-   Nomenclature standards require genus and species names to be in italic.
-   Titles imported into Zotero rarely include the required italic formatting.
-   Manually applying italics to titles is tedious.

Zotero uses HTML tags (**``<i>``** and **``</i>``**) for rich text formatting. This script automates the process of adding these tags around a user-defined list of scientific names.

---

##  The Step-by-Step Procedure

The process is fast and only requires interacting with the script variables.

1.  **Backup your Zotero data** (Always a safe practice, see instructions [here](https://www.zotero.org/support/zotero_data#backing_up_your_zotero_data)).
2.  **Open the Script:** Open the `zotero_italicize_species.js` script in any text editor (Gedit, Notepad, VS Code).
3.  **Define Words to Italicize (`toModify`):**
    * In the `toModify` variable, list all words (genera, species, or other terms) you want italicized.
    * **Crucially:** Separate the genus and species name (e.g., `["Quercus", "pubescens"]` **NOT** `["Quercus pubescens"]`).
4.  **Define Words to Clean Up (`toDelete` - New!):**
    * In the new `toDelete` variable, list any words or phrases that were **incorrectly italicized** in a previous run or manually added, and you wish to remove the `<i>` tags from (e.g., `["Rockfish", "Marbled"]`).
5.  **Run the Script:**
    * Select the entire script and copy it.
    * Open Zotero, go to **Tools** > **Developer** > **Run JavaScript**.
    * Paste the script into the code box, and **tick the 'Run as async function' box**.
    * Click **Run** or press **Ctrl + R**.

That's it! The script will first clean up any entries in `toDelete`, and then safely apply new italics based on the `toModify` list, skipping any terms already formatted.

---

##  Technical Explanations

### 1. Robust Italicization Logic

The script iterates through every character string in the `toModify` variable and uses regular expressions with word boundaries (`\b`) to wrap the word with HTML tags.

The reason you must keep genus and species names separated (e.g., `["Quercus", "pubescens"]`) is to handle various title formats where only the genus, or the full binomial, might appear.

**The Stability Improvement:**
The updated script includes a core check that asks: **"Is this word/phrase already wrapped in `<i>` or `</i>`?"**

* If **Yes**, the script skips the replacement, effectively preventing the formation of double tags (`<i><i>...</i></i>`).
* If **No**, the script safely applies the `<i>...</i>` tags.

This eliminates the complex, error-prone post-processing cleanup step used in older versions of this script.

### 2. The Cleanup Utility (`toDelete`)

The script now executes a full **cleaning pass** before adding new italics:

* It searches for items containing any word listed in `toDelete`.
* It uses robust replacement patterns to remove all forms of `<i>` tags associated with that word (whether `<i>Word</i>` or parts of a split italic phrase like `<i>Word One</i> <i>Word Two</i>`).
* This feature is designed for bulk correction of titles.

---

##  PDF File Renaming

If you use Zotero's default "Rename File from Parent Metadata" function, Zotero will correctly omit the HTML tags in the filename.

If you are using the **[Zotfile](http://zotfile.com/)** extension, you can follow the steps in the original documentation below to define a user wildcard (`%1`) that removes HTML tags before renaming.

*(The original Zotfile configuration steps remain valid here.)*

---

##  Ressources

-   [https://www.zotero.org/support/dev/client_coding/javascript_api#batch_editing](https://www.zotero.org/support/dev/client_coding/javascript_api#batch_editing)
-   See also [Mazospega](https://github.com/IdoBar/Mazospega) that also intends to italicize species names in Zotero, but in a different way (with Python and interface).
