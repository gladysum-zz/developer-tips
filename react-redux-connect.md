## What Does the Connect() Function Do in React-Redux?

When I started learning React-Redux, I had no difficulty understanding the concept of the redux store, reducers, action objects, and action creators. The redux store contains the state of the entire application. Reducers update the redux store. Action objects contain an action type and a payload. Action creators are functions that return action objects.

The hard part was figuring out how to access and update redux store data inside a component. I was not alone in my confusion. Many of my fellow developers were bewildered by the concept of **mapStateToProps**, **mapDispatchToProps**, and the **connect** function. Hopefully this article will help clear a major hurdle for those learning React-Redux.

**Question:** How do I access store data from inside a component?

**Answer:** Use mapStateToProps. It returns an object filled with store data, which are added to the component's props via connect().

**SYNTAX**
```
const mapStateToProps = state => ({
   propertyX:  state.propertyX
})
Note: "state" refers to the redux store.
```
**Question:** How do I update the store from inside a component?

**Answer:** Use mapDispatchToProps. It returns a an object filled with functions that update the store. These functions are also added to the component's props via connect().

**SYNTAX**
```
const mapDispatchToProps = dispatch => ({
   methodName: arg => {
      dispatch(actionCreator(arg))
   }
})
```
Finally, to pass down store data and functions to a component, use the **connect** function:
```
connect(mapStateToProps, mapDispatchToProps)(ComponentName)
```
IMPORTANT! The connect function's arguments must be in a specific order: **mapStateToProps must come before mapDispatchToProps** in order for the connect() function to work.

**EXAMPLE**

```
import React from 'react'
import {connect} from 'react-redux'
import {actionCreator1, actionCreator2} from './action-creators'


class ComponentX extends React.Component {
  constructor(){
     super()
  }

  render() {
    return (
      <div>
        some JSX that involves accessing data from the redux store
        and updating the redux store
      </div>
    )
  }
}

const mapStateToProps = state => ({
  property1: state.property1,
  property2: state.property2
})

const mapDispatchToProps = dispatch => ({
  function1: input1 => {
    dispatch(actionCreator1(input1))
  },
  function2: input2 => {
    dispatch(actionCreator2(input2))
  }
})

export default connect(mapStateToProps, mapDispatchToProps)(ComponentX)
```
Thanks to the connect() function, you can now access the following from inside ComponentX:

{this.props.property1}
{this.props.property2}
{this.props.function1}
{this.props.function2}
