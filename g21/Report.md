# Report for assignment 4

## Project

Name: Zulip

URL: https://github.com/Pihlqvist/zulip

Zulip is a powerful, open source group chat application similar to Slack.

## Selected issue(s)

Title: RealmAuditLog: Add an old_value and new_value field, and update existing calls. #10274

URL: https://github.com/zulip/zulip/issues/10274

The audit log stores important changes like when a user changes their email or name. The old value is not saved, so this issue is meant to fix that.

## Onboarding experience

#### Contribution documentation

How to get onboard was very well documented, everything from where to find the infromation to how to contribute was written in detail. The people working on the project was also keen to help if we had questions. We had no issue claiming a _issue_ and working on it. The general chatroom was active and contained information and discussion around issues. 

#### Did it build as documented?
    
The building documentation is very good, but building only worked for same of us. Building worked fine on Ubuntu and Mac, but with Windows there was a lot of errors that we couldn’t find any information about.

#### Installation

The project required many tools, libraries and components. Fortunately, they were bundled up in a virtual environment called Vagrant, which took some time to download. However, when the download was complete everything worked without any issues. The tools and commands were briefly documented in the projects documentation, which made it relatively easy to get started. There was one command we couldn’t find in the documentation, which we had to Google for. This command could have been seen as a prerequisite for the Django framework though.

## Requirements affected by functionality being refactored

“Identify requirements of the functions to be refactored. If the requirements are not documented yet, try to describe them based on code reviews and existing test cases. Create a project plan for testing these requirements, and refactoring the code.”

There were no requirements documented for the code or the refactoring. In the test file related to the code to be refactored, there are a number of tests for some different events that the code takes care of, such as activating a user, changing a user’s password and email, and changing the owner of a bot. All of the tests pass before refactoring, and should of course pass after the refactoring as well. 

## Existing test cases relating to refactored code

The tests related to the class are in the file test_audit_logs.py. The assertions are decent but never check the actual values of the entry, just that an entry has happened. So they don’t provide a good coverage, but at least it show that the entry was added successfully. All tests ran successfully.

We modified the unittest to check the values of the ‘old_value’ and ‘new_value’ columns we added.

## The refactoring carried out

(Link to) a UML diagram and its description

The refactoring carried out was to add a new_value field and an old_value field to the database in the class RealmAuditLog in `models.py`. This will make Zulip able to keep track of the old value when a change stored in the audit log is made.

## Test logs

Backend unit tests were used for testing the success of the refactoring. All automated test successfully ran but we only tried this once because of time consumptions. The unit tests involve the class itself so should cover all of the functionalities of the refactoring.

#### logs
* [test before](https://github.com/Pihlqvist/zulip/blob/master/g21/testlog_before.txt)
* [test_after](https://github.com/Pihlqvist/zulip/blob/master/g21/testlog_before.txt)

The refactoring itself is documented by the git log.

## Effort spent

| Area | Fredrik | Emma | Ted |
|--|--|--|--|
| plenary discussions/meetings | 12h | 12h | 12h |
| discussions within parts of the group| 1h | 1h | 1h |
| reading documentation | 6h | 3h | 8h |
| configuration | 4h | 2h | 4h |
| analyzing code/output | 2h | 2h | 1h |
| writing documentation | 2h | 3h | 3h |
| writing code | 2h | 1h | 3h |
| running code | 4h | 4h | 7h |

## Overall experience

#### What are your main take-aways from this project? What did you learn?

#### Ted

#### Emma

#### Fredrik


#### Is there something special you want to mention here?

