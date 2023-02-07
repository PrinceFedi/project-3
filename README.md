# UOCIS322 - Project 3 #

You'll learn about JQuery and asynchronous requests in this project.

## Overview

The program is a simple anagram game designed for English-learning students in elementary and middle school. It presents a list of words to students and an anagram. The anagram is a jumble of some of the words, which are randomly chosen. Students attempt to type words that can be created from the jumble. When a matching word is typed, it is added to a list of solved words.

The vocabulary word list is fixed for one invocation of the server, so multiple students connected to the same server will see the same vocabulary list but may have different anagrams.

## Getting started

`flask_vocab.py` runs the anagram game, with the template `vocab.html`. This example uses a conventional interaction through a form, interacting only when the user submits the form. The vocabulary and anagram are currently loaded using basic JINJA. What you're supposed to do is to change the form interaction into an AJAX interaction (using JQuery).

## Tasks

* Familiarize yourself with `flask_vocab.py` and `flask_minijax.py` by running them separately. You need to understand them to do this project.

* Your task is to replace the form interaction (in `flask_vocab.py`) with AJAX interaction on each keystroke using `flask_minijax.py`. 

  **NOTE:** You MUST remove the submit button, check for validity per keystroke, and redirect to the success page as soon as the required number of words are found.

* As always, revise the README file, and add your info to `Dockerfile`. These have points!

* As always, submit your `credentials.ini` through Canvas. It should contain your name and git repo URL.

## FAQ
### What is `src`?
This is a sub-package which contains modules related to the game. You should not make any changes there, but feel free to review them to get a better understanding.

### What is `data`?
This directory contains a few word lists in the form of text files. You should not make any changes to the ones that already exist. However, you can add your own (but don't have to). You can change the word list file in your `credentials.ini`.

### What is minijax?

`flask_minijax.py`, along with its template `templates/minijax.html`, is a tiny example of using JQuery with flask for an AJAX application. They should not be included in the version of the project you turn in. You can use this example to figure out how to implement an AJAX version of the game. Delete the two (along with `static/img`) when you're done with the project.

### How do I run the tests?
The `tests` directory contains a test suite for the `src` package. There's a `run_tests.sh`, which you can run in your container while it's running. However, it is not required, since you will not be changing anything in `src`.

## Details

### flask_vocab.py:

The main functionality for most of this project is centered around the refactoring the previous flask framework and reimplementing it so that JavaScript ("jQuery) can process
the form information it receives for our game. In order to do this, I had to heavily focus on a single method `check`. This function was originally implemented with `POST` requests functionality in the back end and heavily dependent 
on JINJA in the front-end. To modify this, I used the `GET` request equivalent of `flask.request.form` which was `flask.request.args.get`. From then on I refactored the previous cases implementing a JSON redirect for each of the following cases:
* Case 1: If there is a matching word in the list of vocab words that can be created from our anagram.
* Case 2: If the vocab word or input cannot be derived from our anagram and isn't valid
* Case 3: If the amount of matched words equals the intended success count given
### vocab.html

In order to satisfy the given tasks, I removed the submit button functionality. This involved removing the html linked to displaying the button, as well as adding an event function that upon entry prevents our page from being reset. Once that was done,
I began implementing various jQuery logic. An initial function checked the validity of every keystroke to make sure the user input was alphabetical. Then after this I replaced the previous JINJA logic with jQUERY. This involved a function that responds to the result of the
`check` method in `flask_vocab.py` and instantiates the json file it returns as a variable. Building off of this logic, I used the data returned in that JSON file as conditions depending on the cases listed above. For case 1 we would append the matched vocab word to a list right below our
`YOU FOUND` header. After this we would clear the entry from the text box as it waits for another input. Case two is handled next as we display a string stating the current text entered is invalid until a match is found. Finally, if the json file from case 3 is returned, we redirect to our 
success template. 
### Notes

* Information about the JavaScript redirect can be found here: https://www.w3schools.com/howto/howto_js_redirect_webpage.asp
* `DISCLAIMER:` It is up to the user to handle and delete invalid input and try again upon entry.

	 

## Authors

Fedi Aniefuna