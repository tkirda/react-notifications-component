[![npm version](https://badge.fury.io/js/react-notifications-component.svg)](https://badge.fury.io/js/react-notifications-component) [![devDependencies Status](https://david-dm.org/teodosii/react-notifications-component/dev-status.svg)](https://david-dm.org/teodosii/react-notifications-component?type=dev)

# :alien: react-notifications-component

Highly configurable and easy to use React Component to notify your users!

## :star: Demo

https://teodosii.github.io/react-notifications-component/

## :boom: Features

- Touch support
- Responsive notifications
- Predefined standard notification types (`default`, `success`, `info`, `danger`, `warning`)
- Custom notification types
- Custom notification content (`images`, `icons` etc)
- Dismiss after number of seconds
- Dismissable by swiping
- Dismissable by clicking
- Dismissable by custom X icon
- Custom animations on show
- Custom animations on exit
- Custom transitions on sliding
- Custom transitions on swiping
- Top/bottom notification insertion

## :eyes: Install

```
npm install react-notifications-component
```

## :hammer: Usage

You must place `ReactNotificationsComponent` component at the root level of the application in order to work properly, otherwise it might conflict with other DOM elements due to the positioning.

Use ref arrow syntax when declaring `ReactNotificationsComponent` in order to have access to internal method `addNotification`. All API methods provided must be called like this.

For further information on supported options, check documentation.

```jsx
import React from "react";
import ReactNotification from "react-notifications-component";

class App extends React.Component {
  constructor(props) {
    super(props);
    this.addNotification = this.addNotification.bind(this);
  }

  addNotification() {
    this.notificationDOMRef.addNotification({
      title: "Awesomeness",
      message: "Awesome Notifications!",
      type: "success",
      insert: "top",
      container: "top-right",
      animationIn: ["animated", "fadeIn"],
      animationOut: ["animated", "fadeOut"],
      dismiss: { duration: 2000 },
      dismissable: { click: true }
    });
  }

  render() {
    return (
      <div className="app-content">
        <ReactNotification ref={input => this.notificationDOMRef = input} />
        <button onClick={this.addNotification} className="btn btn-primary">
          Add Awesome Notification
        </button>
      </div>
    );
  }
}
```

**Note:** It is important to import `react-notifications-component` CSS theme, which is located in `dist\theme.css`

## :metal: Development

```
npm run build:library
npm run start
```

## :wrench: Test

```
npm run test
```

## :fire: API

`addNotification(options)`

Render a new notification. Method returns a unique ID representing the rendered notification. Supplied options are internally validated and an exception will be thrown if validation fails.

`removeNotification(id)`

Manually remove a notification by ID. Nothing will happen if notification does not exist.

## :sparkles: Examples

1. #### Custom notification type
Following example shows usage of custom notification type defined as option

```jsx
import React from "react";
import ReactNotification from "react-notifications-component";

class App extends React.Component {
  constructor(props) {
    super(props);
    this.addNotification = this.addNotification.bind(this);
  }

  addNotification() {
    this.notificationDOMRef.addNotification({
      // other properties have been omitted for brevity
      type: "awesome",
      title: "Custom",
      message: "Notifications can be customized to suit your needs",
      container: "top-right"
    }));
  }

  render() {
    return (
      <div className="app-content">
        <ReactNotification
          types={[{
            htmlClasses: ["notification-awesome"],
            name: "awesome"
          }]}
          ref={input => this.notificationDOMRef = input}
        />
      </div>
    );
  }
}
```

Custom types need to use custom CSS (not included in `react-notifications-component`)

```scss
.notification-awesome {
  background-color: #685dc3;
  border-left: 8px solid darken(#685dc3, 15%);
}
```

2. #### Custom content with FontAwesome's check mark
This example shows usage of Font Awesome check mark to be included in your notification along with desired custom content

```jsx
this.reactNotificationRef.addNotification({
  // other properties have been omitted for brevity
  container: "top-right",
  content: (
    <div className="notification-custom-success">
      <div className="notification-custom-icon">
        <i className="fa fa-check" />
      </div>
      <div className="notification-custom-content">
        <p className="notification-message">GitHub is awesome!</p>
      </div>
    </div>
  )
}));
```

You also need to update your CSS correspondingly to your custom markup

```scss
.notification-custom-icon {
  flex-basis: 20%;
  position: relative;
  display: inline-block;
  padding: 8px 8px 8px 12px;

  .fa {
    top: 50%;
    left: 50%;
    color: #fff;
    font-size: 28px;
    position: relative;
    transform: translate(-50%, -50%);
  }
}

.notification-custom-success {
  width: 100%;
  display: flex;
  background-color: #28a745;

  .notification-custom-icon {
    border-left: 8px solid darken(#28a745, 15%);
  }
}
```

## :pencil: Options

<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>title</td>
    <td><code>String</code></td>
    <td>Title of the notification. Option is ignored if <code>content</code> is set</td>
  </tr>
  <tr>
    <td>message</td>
    <td><code>String</code></td>
    <td>Message of the notification. Option is ignored if <code>content</code> is set, otherwise it is <b>required</b></td>
  </tr>
  <tr>
    <td>content</td>
    <td><code>React.Component</code></td>
    <td>Custom notification content, must be a valid <code>React</code> component</td>
  </tr>
  <tr>
    <td>type</td>
    <td><code>String</code></td>
    <td>Type of the notification (<code>success</code>, <code>danger</code>, <code>default</code>, <code>info</code>, <code>warning</code> or <code>custom</code>). Option is ignored if <code>content</code> is set, otherwise it is <b>required</b></td>
  </tr>
  <tr>
    <td>container</td>
    <td><code>String</code></td>
    <td>Container in which the notification will be displayed (<code>top-left</code>, <code>top-right</code>, <code>bottom-left</code>, <code>bottom-right</code>). Option is <b>required<b></td>
  </tr>
  <tr>
    <td>insert</td>
    <td><code>String</code></td>
    <td>Insert notification at the <code>top</code> or at the <code>bottom</code> of the container. Option defaults to <code>top</code></td>
  </tr>
  <tr>
    <td>userDefinedTypes</td>
    <td><code>Array</code></td>
    <td>Define allowed types when rendering <code>custom</code> types <ul><li>htmlClasses - <code>Array</code> - CSS classes to be applied to the notification element</li><li>name - <code>String</code> - name of the custom type</li></ul></td>
  </tr>
  <tr>
    <td>dismissable</td>
    <td><code>Object</code></td>
    <td>Specify how a notification should be manually dismissed <ul><li>click - <code>Boolean</code> - dismiss by clicking (option defaults to <b>true</b>)</li><li>touch - <code>Boolean</code> - dismiss by swiping on mobile devices (option defaults to <b>true</b>)</li></ul></td>
  </tr>
  <tr>
    <td>dismissIcon</td>
    <td><code>Object</code></td>
    <td>Custom X icon <ul><li>className - <code>Array</code> - CSS classes to be applied to icon's parent</li><li>content - <code>React.Component</code> - must be a valid React component</li></ul></td>
  </tr>
  <tr>
    <td>animationIn</td>
    <td><code>Array</code></td>
    <td>CSS classes used to animate notification on <code>show</code></td>
  </tr>
  <tr>
    <td>animationOut</td>
    <td><code>Array</code></td>
    <td>CSS classes used to animate notification on <code>removal</code></td>
  </tr>
  <tr>
    <td>slidingEnter</td>
    <td><code>Object</code></td>
    <td>Transition to be used when sliding to show a notification <ul><li>duration - <code>Number</code> (ms)</li><li>cubicBezier - <code>String</code></li><li>delay - <code>Number</code> (ms)</li></ul>
  </tr>
  <tr>
    <td>slidingExit</td>
    <td><code>Object</code></td>
    <td>Transition to be used when sliding to hide a notification <ul><li>duration - <code>Number</code> (ms)</li><li>cubicBezier - <code>String</code></li><li>delay - <code>Number</code> (ms)</li></ul>
  </tr>
  <tr>
    <td>touchSlidingBack</td>
    <td><code>Object</code></td>
    <td>Transition to be used when sliding back after an incomplete swipe <ul><li>duration - <code>Number</code> (ms)</li><li>cubicBezier - <code>String</code></li><li>delay - <code>Number</code> (ms)</li></ul>
  </tr>
  <tr>
    <td>touchSlidingExit</td>
    <td><code>Object</code></td>
    <td>Transition to be used when sliding on swipe<ul><li>duration - <code>Number</code> (ms)</li><li>cubicBezier - <code>String</code></li><li>delay - <code>Number</code> (ms)</li></ul>
  </tr>
  <tr>
    <td>dismiss</td>
    <td><code>Object</code></td>
    <td>Automatically dismiss a notification after specified timeout <ul><li>duration - <code>Number</code> (ms - <code>0</code> means <code>Infinite</code>)</li></ul></td>
  </tr>
  <tr>
    <td>width</td>
    <td><code>Number</code></td>
    <td>Overwrite notification's <code>width</code> defined by stylesheets</td>
  </tr>
</table>

## :sunglasses: Roadmap

- Release `v1.0.0`
- Improve tests for better coverage (up to `100%`)
- Move `react-notifications-component` theme to a separate `npm` package

## :rocket: Ideas

- Containers for other positions (`top-center`, `bottom-center`, `center` or even `custom`)
- Events support (`onShow`, `onRemoved`, `onClicked`, `onTimeoutDismissed` etc)
- Show time left (`progress-bar` like)
- `Modal` notification

**Note:** Feedback on wanted/existing features is **_appreciated_**