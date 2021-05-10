# Understanding Questions:
1. What are the steps of execution from the pressing of the 1 button to the rendering of our updated value? List what part of the code executes for each step.
* The user presses the 1 button.
```javascript

```
* CalcButton handles click and dispatches addOne reducer.
```javascript
<CalcButton
                value={1}
                // onClick={() => dispatch(addOne(1))}
                onClick={() => dispatch(applyNumber(1))}
              />
```
```javascript
export const applyNumber = (number) => {
    return({type:APPLY_NUMBER, payload:number});
}
```
* addOne reducer copies previous state.
```javascript
        case(APPLY_NUMBER):
            return ({ 
                ...state, 
                total: calculateResult(state.total, action.payload, state.operation)
            });
```
* addOne reducer gets current state total and adds 1 to it.
```javascript
const calculateResult = (num1, num2, operation) => {
    // eslint-disable-next-line default-case
    switch(operation) {
        case("+"):
            return num1 + num2;
        case("*"):
            return num1 * num2;
        case("-"):
            return num1 - num2;
    }
}
```
* TotalDisplay renders the total plus 1.
```javascript
const TotalDisplay = (props) => {
    const { value } = props;
    
    return(
    <div className="row">
        <div className="col-md-12 p-0"> 
            <div className="form-group">
                <textarea className="form-control" readOnly value={value} rows="1" id="total" type="text" name="ans"></textarea>
            </div>
        </div>
    </div>);
}

export default TotalDisplay;
```

