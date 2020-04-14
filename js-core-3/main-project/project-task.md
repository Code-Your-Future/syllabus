# TV Show DOM Project

### Overview

You must make a web app using HTML, CSS, and JavaScript which shows details of all of the episodes of a TV show.

The episode data is provided for you as an array of objects.

The page of episodes should be generated using JavaScript (which will read the properties of each episode object).

This project challenge is split into various levels of difficulty. You should challenge yourself to complete as many levels as possible.

# Rules about technology

- You should not use React, Vue, JQuery or other libraries. Why? This project is specifically for practicing the **built-in** DOM-manipulation functions you learned about in JS2.

- You can use bootstrap CSS but NOT bootstrap JS. (We recommend that you do NOT use bootstrap CSS.)

# Level 1 - Minimal features:

1. All episodes must be shown
1. For each episode, AT LEAST following must be displayed:
   1. the episode's title
   1. the season number
   1. the episode number
   1. the episode's medium-sized image
   1. the episode's summary text
1. You should combine season number and episode number into an **episode code**:
   1. Each part should be zero-padded to two digits.
   1. Example: `S02E07` would be the code for the 7th episode of the 2nd season. `S2E7` would be incorrect.

## Screenshot of minimal version

To be successful with the minimal version, you can style and lay out your application however you like. However, here is an example of one way you could lay out the required content.

![Example Screenshot](./example-screenshots/example-level-1.png)

# Level 2 - Add Search

1. Complete all requirements from Level 1
1. Add a "live" search input:
   1. Only episodes whose summary **OR** title contains the search term should be displayed
   1. The search should be case-**in**sensitive
   1. The display should update **immediately** after each keystroke changes the input.
   1. Display how many episodes match the current search
   1. If the search box is cleared, **all** episodes should be shown.

If you have been fetching the episode data from the API, be careful not to cause many frequent requests with this search feature. The search should look through an _in-memory_ copy of the episode list. **Do not** fetch the data again each time something is typed!

### Example screenshot of search

![Example Search screenshot](./example-screenshots/example-search.jpg)

# Level 3 - Add an Episode Selector

1. Complete all requirements from level 2
1. Add a `select` input which allows you to jump quickly to an episode:
   1. The select input should list all episodes in the format: "S01E01 - Winter is Coming"
   1. When the user makes a selection, they should be taken directly to that episode in the list
   1. Bonus: if you prefer, when the select is used, ONLY show the selected episode. If you do this, be sure to provide a way for the user to see all episodes again.

### Example screenshot of Episode Selector

![Example Episode Selector screenshot](./example-screenshots/example-episode-selector.jpg)

# Getting started

Follow the instructions in [getting-started.md](./getting-started.md)

# Getting a code review

You will be instructed when to ask for a code review. When it's time to do so, follow the instructions in [code-review.md](./code-review.md)
