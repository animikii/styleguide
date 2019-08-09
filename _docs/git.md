---
layout: page
title: Git
permalink: /git
---

### Gitflow Workflow

The overall flow of Gitflow is:

- A develop branch is created from master
- A release branch is created from develop
- Feature branches are created from develop
- When a feature is complete it is merged into the develop branch
- When the release branch is done it is merged into develop and master
- If an issue in master is detected a hotfix branch is created from master
- Once the hotfix is complete it is merged to both develop and master

[More info](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

#### Develop and Master Branches

![img](https://wac-cdn.atlassian.com/dam/jcr:2bef0bef-22bc-4485-94b9-a9422f70f11c/02%20(2).svg?cdnVersion=jo)

#### Feature Branches

![img](https://wac-cdn.atlassian.com/dam/jcr:a9cea7b7-23c3-41a7-a4e0-affa053d9ea7/04%20(1).svg?cdnVersion=jo)

#### Hotfix Branches

![img](https://wac-cdn.atlassian.com/dam/jcr:61ccc620-5249-4338-be66-94d563f2843c/05%20(2).svg?cdnVersion=jo)


## Commit Messages

_This is an adaptation of [Thoughtbot's guide](https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message)._

The first line of the commit message should be no more than 50 characters. It should answer the question, "Why is this change necessary?". Treat the first line of the commit message as you would a title, that is, it should start with a capital letter, be grammatically correct, but need not end with a period.

If the change is sufficiently complex, leave a blank line under the first line, and describe the change in more detail. Try to answer the questions, "How does it address the issue?", and, "What side effects does this change have?". Consider referencing (through means of a link) an issue from the project management board.

Here's an example of a good commit:

```text
Make email field optional for OAuth users

https://trello.com/path/to/relevant/card

Due to the variety of OAuth providers and their different permissions, we can't
always guarantee the existence of an email address as part of the response.
```

Here's an example of a bad commit:

```text
fix stuff
```

The level of detail in the good example is not always necessary. The important piece is the first line of the commit message, since that's what people see when reading over commits.
