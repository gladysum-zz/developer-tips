## The Hardest Thing About React-Redux

When I started learning React-Redux, I had no difficulty understanding the concept of the redux store, reducers, action objects, action creators. The redux store contains the state of the entire application. Reducers update the redux store. Action objects contain an action and a payload. Action creators are functions that return action objects.

The hard part was figuring out how to access and update redux store data inside a component. I was not alone in my confusion. Many of my developers were bewildered by the concept of mapStateToProps, mapDispatchToProps, and the connect function. I saw developers invoking the connect function in instances where it was not needed. I wrote this article to explain these tricky concepts in plain English.

**Question:** How do I access store data from inside a component?

**Answer:** Use mapStateToProps. It returns an object filled with store data, which are added to the component's props via connect().

**SYNTAX**
```
const mapStateToProps = state => ({
   key:  value
})
```
**Question:** How do I update the store from inside a component?

**Answer:** Use mapDispatchToProps. It returns a an object filled with methods that update the store. These methods are also added to the component's props via connect().

**SYNTAX**
```
const mapDispatchToProps = dispatch => ({
   methodName: arg => {
      dispatch(actionCreator(arg))
   }
})
```
Finally, to pass down store data and methods to a component, use the **connect** function:
```
connect(mapStateToProps, mapDispatchToProps)(componentName)
```
IMPORTANT! The connect function's arguments must be in a specific order: **mapStateToProps must come before mapDispatchToProps** in order for the connect function to work.

**EXAMPLE**

```
import React from 'react'
import { connect } from 'react-redux'
import {actionCreator1, actionCreator2} from './action-creators'


class ComponentX extends React.Component {
  constructor(props){
     super(props)
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
  object1: state.object1,
  object2: state.object2
})

const mapDispatchToProps = dispatch => ({
  method1: input1 => {
    dispatch(actionCreator1(input1))
  },
  method2: input2 => {
    dispatch(actionCreator2(input2))
  }
})

export default connect(mapStateToProps, mapDispatchToProps)(componentX)
```
