##The Hardest Thing About React-Redux

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
To pass down store data and methods to a component, use the **connect** function:
```
connect(mapStateToProps, mapDispatchToProps)(componentName)
```
IMPORTANT! The connect function's arguments must be in a specific order: **mapStateToProps must come before mapDispatchToProps** in order for the connect function to work.

A basic React component that accesses data from the redux store and updates the redux store will typically contain the following elements:
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
