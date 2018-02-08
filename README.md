# Animikii Style Guide
Welcome to the Animikii style guide where we layout our code conventions, patterns and solutions to problems we encounter.

Please keep in mind that **master** is the production branch. If you merge anything to the **master** branch it will be pushed.

**Note: if you need review, make a pull request and assign to the person(s) you would like to review.**

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
