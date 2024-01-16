# Dataset Generator
## Video Demo:  <URL>

## Description
This tool is designed to provide a simple yet flexible generation of random datasets.

### Backstory
Having worked in no-code data analysis throughout my career, as I decided to learn the programming tools used by “regular” data analysts I found myself facing a challenge: I needed realistic datasets I could use to practice, but existing online resources either required excessive customization or lacked the flexibility I required.

My intention is that this tool can be used by other data analysis and programming students who might have similar needs.

### Key Features
Generate datasets based on three dimensions:

* Number of sets
* Length of each set
* Number of digits

The latter is given by three parameters: minimum/maximum digits and a "currency" flag, which adds two decimal points to the numbers.

## Table of Contents
Include a table of contents to help users navigate through the README easily.
* [Installation](#installation)
* [Usage](#usage)
* [File Structure](#file-structure)
* [Back end](#back-end)
* [Results Page](#results-page)
* [Help Page](#help-page)
* [Contributing](#contributing)
* [Known Issues](#known-issues)
* [License](#license)
* [Contact Information](#contact-information)

## Requirements
* **Back end**
  * This project is written in Python 3.11.

  * **Python Libraries:**
    * [Flask](https://flask.palletsprojects.com/en/3.0.x/) v.3.0.0
    * [Jinja2](https://jinja.palletsprojects.com/en/3.1.x/) v.3.1.2

  * **Python Standard Libraries:**
    * random
    * csv

* **Front end**
  * HTML5
  * CSS3

  * **Style tools**
    * [Bootstrap](https://getbootstrap.com/) v.5.3

## File Structure
* **static/**
  * **files/** - Stores the .csv files created by the generator. See [back end section](#back-end) for details.
  * **images/** - Images used in the HTML layouts.
  * **styles.css** - CSS override code for styling.

* **templates/**
  * **layout.html** - HTML file for the standard page layout (header/footer). The remaining template files modify the body of the pages.
  * **setup.html** - HTML file for the setup form.
  * **download.html** - HTML file displaying the download link.
  * **help.html** - HTML file for user support page.
  * **heart.html** - HTML file for an "Easter-egg" page.

* **Other files**
  * **app.py** - Back end file.
  * **readme.md** - Documentation file.

## Usage
- Run instructions - Provide instructions on how to run your website.
- Accessing pages - Explain how users can navigate to the setup, results, and help pages.

   ### Results Page
   - Interpretation and usage - Provide information on how users can interpret and use the results page.

   ### Help Page
   - Purpose and guidance - Explain the purpose of the help page and provide guidance on using it.

## Backend
- Overview - Briefly describe the purpose and functionality of the backend file.
- APIs/Endpoints - If applicable, document the APIs or endpoints provided by the backend.

## Known Issues
- List of known issues and workarounds

## Laundry List
List of future/possible features

## Credits and Acknowledgements
Navbar icon: Spreadsheet by Zach Bogart from [The Noun Project] (https://thenounproject.com/search/icons/?q=spreadsheet)

## Contributing
- Guidelines for contributing - If you're open to contributions, provide guidelines on how others can contribute to your project.

## Contact Information
Include your contact information or ways for users to reach out for help or feedback.
- Your contact details










### Features
For the front end, I have designed two functional pages (`setup` and `results`) and a `help` section for the end user.

The `setup` form allows the user to submit the parameters that will be used for dataset generation:

> [!NOTE]
> The `currency` field **adds** two digits to the `min` and `max` submitted by the user, which will later be converted into decimals.

Those parameters will be processed in the backend (more on that later), resulting in a `.csv` file that can be downloaded via a link available in the `results` page.

For future versions, I'll be adding a `login` feature that allows users to save favourite parameters that can be reused, thus skipping the `setup` form entirely. I'm also studying the feasibility of a tool for re-generating sets; however, how useful that might be is still up to debate.

### app.py
The program in `app.py` can be divided in two sections: the set-up and the generation itself.

#### Setting up the number generation
This section consists in translating the parameters submitted in the front-end into the variables that we'll use later for the actual number generation. The steps involved are:

1. Obtain parameters from the setup form --> Saves the values from the `setup` form as variables.

2. Check if the min and max submitted are valid --> Ensures that `max digits` is at least equal to `min digits`.
   > [!NOTE]
   > This checkpoint triggers a `setup` form reload if the submitted values aren't valid. In this case, the hidden alert in the `setup.html` file is set to on and most of the fields are pre-filled with the values originally submitted by the user; however, I was unable to set the currency switch back to on.

3. Adjust max and min values if currency is set to on --> Adds the two extra digits required for proper decimal generation. They'll be removed later, so the correct `min` and `max` digits are displayed in the `results` page.

4. Randomly generate a unique file name --> A randomized numerical suffix is appended to the structure dataset_[number].csv, creating a unique name that will be used in the next steps.
   > [!NOTE]
   > At the moment, there's no automated file deletion feature.

#### Number generation
1. Obtain a randomized numeric range for each row --> Looping over the rows, the program picks a random value from the length range. The range for the values in each row is set as numbers between `10^(n-1)` (lowest) and `10^n - 1` (highest).

2. Generate numbers --> For each column, we'll generate a random integer between the lowest and highest numbers defined above. If the currency filter is enabled, this is also the step where the decimal conversion happens.

3. Write numbers in the file --> Each row is stored in a `numbers` list, which is subsequently written into the unique file created in the step "Randomly generate a unique file name".

4. Adjust max, min and currency values for display --> This step is for displays reasons only: it undoes the changes from the step "Adjust max and min values if currency is set to on", and also sets currency to `off` (instead of `None`) if applicable.

The variables `rows`, `columns`, `min`, `max`, and `currency` are submitted to the `results` page, where they'll be displayed as a review of the settings submitted by the user. `filename` (but not its path) is also submitted and will be used to create the custom `download` link.






when you're writing your project's README, it should be able to answer the what, why, and the how of the project.
Here are some guide questions that will help you out:
What was your motivation?
Why did you build this project?
What problem does it solve?
What did you learn?
What makes your project stand out?


A good one takes advantage of the opportunity to explain and showcase:

What your application does,
Why you used the technologies you used,
Some of the challenges you faced and features you hope to implement in the future.



Your README.md file should be minimally multiple paragraphs in length, and should explain
what your project is,
what each of the files you wrote for the project contains and does,
and if you debated certain design choices, explaining why you made them.

Ensure you allocate sufficient time and energy to writing a README.md that documents your project thoroughly. Be proud of it! A README.md in the neighborhood of 750 words is likely to be sufficient for describing your project and all aspects of its functionality. If unable to reach that threshold, that probably means your project is insufficiently complex.

