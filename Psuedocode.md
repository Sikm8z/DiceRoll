# Advanced Dice Roll Simulation (Conceptual Pseudocode)

**Project Context:** This project was developed as part of a university coursework focusing on fundamental programming concepts and algorithm design. This version presents the core logic in an anonymised pseudocode format to respect academic integrity policies while effectively showcasing problem-solving methodology.

---

## I. Main Program Flow

1.  **Initialize Global Statistics:**
    * `total_rolls_processed`: Counter for all dice rolled during program execution.
    * `non_exploding_rolls`: Counter for dice rolls that do not trigger the explosion mechanic.
    * `total_explosions_recorded`: Counter for the total number of dice rolls that result in an explosion.

2.  **Display Welcome & Heading:**
    * Call `display_framed_heading` function with title "Dice Roll Simulator".
    * Display a friendly welcome message to the user.

3.  **Enter Main Interaction Loop:**
    * Begin an indefinite loop that continues until the user explicitly chooses to exit.
    * **Prompt User Input:** Request user to enter a dice roll command (e.g., "3d6"), "h" for help, or "x" to exit.
    * **Process Input (Case-Insensitive):** Convert user input to lowercase.

4.  **Handle 'Help' Command:**
    * If input is 'h':
        * Call `display_framed_heading` function with heading "Help Information".
        * Present details on valid command formats (e.g., "[quantity]d[sides]", "exploding dice with '!' suffix").
        * Continue to the next iteration of the main loop (prompt for new input).

5.  **Handle 'Exit' Command:**
    * If input is 'x':
        * Call `display_framed_heading` function with heading "Session Concluded".
        * Exit the main program loop.

6.  **Detect Exploding Dice Option:**
    * If the input command ends with '!':
        * Set `is_exploding_enabled` flag to `True`.
        * Initialize `current_explosion_value` to 0 (for tracking re-rolls within a single die).
        * Remove the '!' character from the input command.
    * Otherwise:
        * Set `is_exploding_enabled` flag to `False`.

7.  **Parse & Validate Roll Command:**
    * Split the input command string by 'd' to get quantity and sides.
    * **Validate Format & Values:**
        * Check if exactly two parts were obtained after splitting.
        * Confirm both parts are valid integers.
        * Verify that quantity is at least 1 and sides is at least 2.
    * If validation fails:
        * Display an invalid input error message.
        * Continue to the next iteration of the main loop.

8.  **Extract Roll Parameters:**
    * Assign the parsed integers to `num_dice_to_roll` and `die_sides`.

9.  **Confirm Roll Type to User:**
    * If `is_exploding_enabled` is `True`, confirm an "exploding" roll is being performed.
    * Otherwise, confirm a standard roll.

10. **Execute Dice Rolls:**
    * Initialize `individual_roll_results` as an empty list to store each die's outcome.
    * Initialize `explosions_this_roll_set` to 0 (for current set of dice).
    * **Loop for Each Die:** Iterate from 1 up to `num_dice_to_roll`:
        * Increment `total_rolls_processed` by 1.
        * `current_die_result = roll_single_die(die_sides)`.
        * Add `current_die_result` to `individual_roll_results`.
        * Display `current_die_result` to the user.
        * **Track Non-Exploding Rolls:** If `current_die_result` is less than `die_sides` OR `is_exploding_enabled` is `False`, increment `non_exploding_rolls`.
        * **Handle Explosions (Conditional Loop):**
            * While `is_exploding_enabled` is `True` AND (`current_die_result` is `die_sides` OR `current_explosion_value` is `die_sides`):
                * If `current_die_result` is `die_sides` (initial explosion for this die):
                    * Increment `explosions_this_roll_set`.
                * `re_roll_value = roll_single_die(die_sides)`.
                * `accumulated_total_for_die = current_die_result + re_roll_value`.
                * Display a message indicating an explosion, including `re_roll_value` and `accumulated_total_for_die`.
                * Update `current_die_result` to `accumulated_total_for_die` for subsequent checks.
                * `current_explosion_value` = `re_roll_value` (for nested explosion check).
        * Introduce a short delay for user readability.

11. **Update Session Statistics & Display Summary:**
    * Add `explosions_this_roll_set` to `total_explosions_recorded`.
    * Calculate `minimum_roll = min(individual_roll_results)`.
    * Calculate `maximum_roll = max(individual_roll_results)`.
    * Calculate `sum_of_rolls = sum(individual_roll_results)`.
    * Determine correct grammatical suffix for "occurrence/occurrences" for min/max.
    * Determine `max_explosions_from_single_die` (if applicable).
    * Call `display_framed_heading` with heading "Roll Summary".
    * Display roll statistics: individual results, total sum, average (rounded), minimum (with count), maximum (with count).
    * If `is_exploding_enabled` is `True`, display explosion statistics: total exploding rolls, most subsequent explosions for a single die.

**When the user chooses to exit the program, display overall statistics on exit including:**
* The total number of dice rolled.
* The total number of ‘Normal’ rolls – those that did not explode.
* The total number of ‘Exploding’ rolls – Those that did explode.

---

## II. Functions

1.  **Define `display_framed_heading(heading_text, frame_width)`:**
    * Parameters: `heading_text` (string), `frame_width` (integer, default 51).
    * Action: Prints a decorative box around the `heading_text`, centered within the specified `frame_width`, using generic text symbols (e.g., `-`, `|`, `+`) instead of Unicode characters to ensure wide compatibility.

---

**Disclaimer:** This pseudocode is provided for illustrative purposes to demonstrate algorithmic thinking and problem-solving skills acquired during university coursework. It is a conceptual representation and not directly executable production code. All specific university course identifiers or proprietary elements have been removed or generalized to adhere to academic integrity policies.