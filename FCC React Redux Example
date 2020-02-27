//Import any modules from libraries
const { Provider, connect } = ReactRedux; //The <Provider /> makes the Redux store available to any nested components that have been wrapped in the connect() function.
//equivalent: const Provider = ReactRedux.Provider; const connect = ReactRedux.connect;

//Redux
const ADD = 'ADD'; //action
const addMessage = (message) => { //action creator, used by reducer
  return {
    type: ADD,
    message
  }
}
const messageReducer = (state = [], action) => {  //Reducers specify how the application's state changes in response to actions sent to the store. The first time the reducer is called, the state value will be undefined. The reducer needs to handle this case by supplying a default state value before handling the incoming action.
  switch (action.type) {
    case ADD:
      return [...state, action.message];
    default:
      return state;
  }
}

const store = Redux.createStore(messageReducer); //Need combineReducers (additional import) if more than 1 reducer

//React
class Presentational extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      //messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    //const currentMessage = this.state.input;
    this.props.submitNewMessage(this.state.input);
    this.setState({
      input: ''
      //messages: this.state.messages.concat(currentMessage)
    });
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.props.messages.map( (message, idx) => { //change this.state to this.props for Redux
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

const mapStateToProps = (state) => { //Redux uses store.subscribe behind the scenes to implement this; adds a change listener
  return {
    messages: state //normally need to specify state property, but this app keeps everything in one array so here it's just 'state'
  }
}

const mapDispatchToProps = (dispatch) => { //store.dispatch: dispatches an action. This is the only way to trigger a state change
  return{
    submitNewMessage: (message) => {
      dispatch(addMessage(message))
    }
  }
}

const Container = connect(mapStateToProps, mapDispatchToProps)(Presentational); //connects a React component to a Redux store

class AppWrapper extends React.Component{
  render(){
    return(
      <Provider store={store}>
        <Container/>
      </Provider>
    );
  }
};

ReactDOM.render(<AppWrapper/>, document.getElementById('root'));
