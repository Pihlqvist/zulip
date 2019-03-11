# Report for assignment 4

## Project

Name: Zulip

URL: https://github.com/Pihlqvist/zulip

Zulip is a powerful, open source group chat application similar to Slack.

## Selected issue(s)

Title: RealmAuditLog: Add an old_value and new_value field, and update existing calls. [#10274](https://github.com/zulip/zulip/issues/10274)

URL: https://github.com/zulip/zulip/issues/10274

The audit log stores important changes like when a user changes their email or name. The old value is not saved, so this issue is meant to fix that.

## Onboarding experience

#### Contribution documentation

Starting out on this project was simply because of its great documentation. All we needed to do was follow the instructions that were presented to us on GitHub, development wiki and chatroom. The contributors working on the project was also keen to help if we had questions. We had no issue claiming an _issue_ in the correct fashion. The general chatroom was active and contained discussion and information on issues and ideas.

#### Did it build as documented?
    
The [building documentation](https://zulip.readthedocs.io/en/latest/development/overview.html) is very good, all we need to do was follow step by step instructions.  There were some issues here, some of us encountered errors while building the project, the general errors and solutions to them provided by the documentation didn't help. We could not resolve this on some machines so continued on the once we could build it for.

#### Installation

The project required many tools, libraries and components. Fortunately, they were bundled up in a virtual environment called Vagrant, which took some time to download. However, when the download was complete everything worked without any issues. The tools and commands were briefly documented in the [project's documentation](https://zulip.readthedocs.io/en/latest/development/setup-vagrant.html), which made it relatively easy to get started. There was one command we couldn’t find in the documentation, which we had to Google for. This command could have been seen as a prerequisite for the Django framework though.

## Requirements affected by functionality being refactored

<!--“Identify requirements of the functions to be refactored. If the requirements are not documented yet, try to describe them based on code reviews and existing test cases. Create a project plan for testing these requirements, and refactoring the code.” -->

There were no requirements documented for the code or the refactoring. In the test file related to the code to be refactored, there are a number of tests for some different events that the code takes care of, such as activating a user, changing a user’s password and email, and changing the owner of a bot. All of the tests pass before refactoring, and should, of course, pass after the refactoring as well.

The information we had on the refactoring came from a GitHub issue where the issue was brefily described. More information could be found in the [chatroom](https://chat.zulip.org/#narrow/stream/49-development-help/subject/realm.20audit.20log.20changes/near/628995) where several contributors discussed what they wanted the refactoring to achieve.

### Refactoring scope

The refactoring wanted by the project contributors is to change how a [Logger class](https://github.com/Pihlqvist/zulip/blob/master/zerver/models.py#L2304-L2381) stores value that it logs. Before the refactoring the Logger stores the event happening with information on what and when the change happend. To store what actually happened a specific `extra_value` field had to be used. Instead of using this crude method the refactoring wants to make sure the database can store `new/old_value` in place of the `extra_value`. This would mean that all relevant callbacks should be updated in the refactoring, as well as testing for the callbacks and class.

### Requirements
* Implement `new/old_value` for TestRealmAuditLog (database entry)
* Refactor callbacks to functions that uses TestRealmAuditLog
* Test the refactoring for all callback functions and new functionality.

## Existing test cases relating to refactored code

The existing tests related to the class were neatly put in a unittest class, [TestRealmAuditLog](https://github.com/Pihlqvist/zulip/blob/master/zerver/tests/test_audit_log.py#L18-L141). The assertions are decent but never check the actual values of the entry, just that an entry has happened. So they don’t provide good coverage, but at least it shows that the entry was added successfully. All tests ran successfully.

We modified the unittest to check the values of the ‘old_value’ and ‘new_value’ columns we added. The modified values can be found in the updated [TestRealmAuditLog](https://github.com/Pihlqvist/zulip/blob/issue-10274/zerver/tests/test_audit_log.py#L19-L166).

## The refactoring carried out

![Before Refactoring](https://github.com/Pihlqvist/zulip/blob/master/g21/ULM-Before_refactoring.png "Before Refactoring")

![After Refactoring](https://github.com/Pihlqvist/zulip/blob/master/g21/ULM-After_refactoring.png "After Refactoring")

(Link to) a UML diagram and its description

The refactoring carried out was to add a `new_value` field and an `old_value` field to the database in the class RealmAuditLog in `models.py`. This will make Zulip able to keep track of the old value when a change stored in the audit log is made.

## Test logs

Backend unit tests were used for testing the success of the refactoring. All automated test successfully ran but we only tried this once because of time consumptions. The unit tests involve the class itself so should cover all of the functionalities of the refactoring.

#### logs
* [test before](https://github.com/Pihlqvist/zulip/blob/master/g21/testlog_before.txt)
* [test after](https://github.com/Pihlqvist/zulip/blob/master/g21/testlog_after.txt)

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

I'm again reminded of the importance of documentation. It took us so long to find a project with the correct requirements for the assignment. After many failed projects that we just could not get to work. All because of poor documentation.

The assignment also opened my eyes to how different open source projects are. The project we ended up with communicated very well. Other projects didn't even have any external communication with their contributors, very polarised.

#### Is there something special you want to mention here?

