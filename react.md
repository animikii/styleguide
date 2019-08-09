---
layout: page
title: React
permalink: /react
---

## Javascript/React/Babel
Please refer to airbnb's style guide on javascript https://github.com/airbnb/javascript

Rules to live by
- pure functions - *no side effects!*
- use classes for reusable objects
- maintain immutable data
- No trailing whitespace
- Use Semicolons
- 80 characters per line


### No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing whitespace in your JS files before committing. Otherwise the rotten smell of careless neglect will eventually drive away contributors and/or co-workers.

### Use Semicolons

According to [scientific research](http://news.ycombinator.com/item?id=1547647), the usage of semicolons is a core value of our community. Consider the points of [the opposition](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding), but be a traditionalist when it comes to abusing error correction mechanisms for cheap syntactic pleasures.

### 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the last few years, but your brain has not. Use the additional room for split screen, your editor supports that, right?

### Webpack

...

## General

- Only include one React component per file (see below).
  - However, multiple [Stateless, or Pure, Components](https://facebook.github.io/react/docs/components-and-props.html) are allowed per file. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
- Always use JSX syntax.
- Do not use `React.createElement` unless you're initializing the app from a file that is not JSX.

Use the airbnb style guide on react https://github.com/airbnb/javascript/tree/master/react

## Asynchronous Redux Actions

We will not use thunks, because they are not a clean architectural solution. See: http://blog.jakegardner.me/redux-thunk-vs-saga/ for using [redux-saga](https://github.com/redux-saga/redux-saga) instead.

## Action Naming Convention

`<NAME_OF_REDUCER>|<VERB>|<SUCCESS|FAIL>`

```
COMMENT|ADD
COMMENT|ADD|SUCCESS
COMMENT|ADD|FAIL

USER_COMMENT|DELETE
USER_COMMENT|DELETE|SUCCESS
USER_COMMENT|DELETE|FAIL

COMMENT|FLAG_SPAM
```

## File structure

```
  /routers
    /registrars
      - inbox.jsx
    /facilitators
      - inbox.jsx
  /actions
    - index.js                # All actions
  /components
    - MainApp.jsx             # main app component
    - MainAppContainer.js
    /Shared                   # Should there be a shared folder?
      - Modal.jsx
      - Form.jsx
    /Inbox
      - BaseContainer.js      # Smart component (has the mapStateToProps)
      - Base.jsx              # Dumb component does the rendering of state
      - MesaageList.jsx
      - Message.jsx
    /Header
      - BaseContainer.js
      - Base.jsx
      - Menu.jsx
      - MenuItem.jsx
    /Dashboard
      - BaseContainer.js
      - Base.jsx
  /constants
    - index.js
    - ActionTypes.js
  /container
  /reducers
    - index.jsx
  /sagas
    - index.jsx
  /selectors
    - index.jsx
  /startup
  /store
```

### Example using Containers

**MainApp.jsx**

    import InboxContainer from './Inbox/BaseContainer'
    import HeaderContainer from './Header/BaseContainer'

    const MainApp = () => (
      <div className="MainApp">
        <HeaderContainer />
        <InboxContainer />
      </div>
    )

**/Inbox/BaseContainer.js**

    import { connect } from 'react-redux';
    import InboxBase from './Base'
    import { openMessage } from '../.../actions/ActionCreators';

    const mapStateToProps = state => ({
      messages: state.messages,
    });

    const mapDispatchToProps = dispatch => ({
      onClick: (message) => {
        dispatch(openMessage(message));
      },
    });

    export default connect(mapStateToProps, mapDispatchToProps)(InboxBase);

**/Inbox/Base.jsx**

    import MessageList from './MessageList'

    const Inbox = ({ messages, onClick }) => (
      <div className="Inbox">
        <MessageList messages={messages} onClick={onClick} />
      </div>
    );

**/Inbox/MessageList.jsx**

    import Message from './Message'

    const MessageList = ({ messages, onClick }) => (
      <div className="MessageList">
        {messages.map(item => {
          <Message {...item} onClick={() => onClick(item)} />
        })}
      </div>
    );

**/Inbox/Message.jsx**

    const Message = ({ title, body, onClick }) => (
      <div className="Message" onClick={onClick}>
        <div>{title}</div>
        <div>{body}</div>
      </div>
    );


## Using Sagas
When using sagas for Api calls, side effects, async things.
Try to keep to a `SUCCESS` or `FAIL` convention with a payload of the response.

    if (response) {
      yield put({ type: 'FILE|FETCH|SUCCESS', file: response.data });
    } else {
      yield put({ type: 'FILE|FETCH|FAIL', error: error });
    }

The initial takeLatest will be a `FILE|FETCH` using our naming convention.

## Shape of the Redux Store

http://redux.js.org/docs/recipes/reducers/NormalizingStateShape.html#designing-a-normalized-state

### Problem having client out of sync with the back-end.

Solution: Have the version sent in every api call.

```
/api/somecall/0001
{
  ...
  version: 1.0.2
}
```

Check version with the front end send return error if it different or force reload.
