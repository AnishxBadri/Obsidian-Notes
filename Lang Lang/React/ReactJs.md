
React Syntax Stuff:

- export default vs export.     
- export default allows you to export a single value from a module as the default export. So no need to mention which component is benign exported since that is the only thing that will be exported from the file.
- Export with named exports allows you to export multiple values from a module using named exports.

React Server Components:

[Source](https://www.joshwcomeau.com/react/server-components/)

- Server Side Rendering (SSR):     
- Before everything was client side rendered in react. The bundle.js script includes everything needed to mount and run the application.
- Once the JS is downloaded and parsed, React spring to action conjuring all of the DOM nodes for our entire application, and housing it in an empty div id=”root”.
- In SSR, the server will redner our application to generate the actual HTML. the user receives a fully-formed HTML document. Client side React after the rendered HTML is delivered then picks up where server-side React left off, adopting the DOM and sprinkling interactivity.
- CSR on the left and SSR on the right.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc4u9Szm6nn3lNwnNUhPxR8Zqr5qQ8Uhdz80K2T-Mj_C-gRfguXgX5Cwsj4GOEZIZEgRhNW6KhvDQwXwsBHbjsS9ChFIOH_Sn9LZssyVfuG_jdI-V3ikQFTy1nalckQ2u6Kj5iMdmfDOyP6e5colwrjLREW?key=hovy-OenfX6NFW0oYWzO0Q)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdUihyhVdTGj4MC4ZMkNCQuTCnjG9q8XTHIclDr3I_pjPRHdgwyUIsF5S9xgMzvHjHrD_XgvbzcFNs4PjCoXZ07Sw9H4-qJBvqNfN-fh886SH4tfgoRyGyw2lQxe33XJyTMBPXtU5qfRHPW932P0zM4W5RL?key=hovy-OenfX6NFW0oYWzO0Q)

- Before RSC as seen above, there is a back and forth in SSR. The Render Shell is first 
- rendered in server, then hydrated in client, then back to server for database query and then back to client to render. 
    
- Server components never re-render. Once the server generates the UI. The rendered value is sent to the client and locked in place. As far as React is concerned, this output is immutable and will never change. So we can’t use things like useState or useEffect
    
- Also important to understand that client components both renders on server and client, while server component renders only on the server.
    
- RSC tried to prevent the back and forth.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeYXti1uJ9JuNLgJA6ELHq2wcD29gLInqaB5sdFMlyy8Vmxnh09tU4qIxJWQTxrn2hpSGCt9LgkxcM7MwtojZQk3fsZ_BhjCy-PX4MPQTFbSatEyI_oPvw1rI38FHOhrFIebWyyw_7K_SzBGs6FrQtvYbNR?key=hovy-OenfX6NFW0oYWzO0Q)  

- With RSC we can create components that can run exclusively on the server like writing database queries etc.
    
- Components are treated as server components by default, when you write use client then only it can be rendered in client.
    
- Client components can only import other client components.
    
- The parent-child relationship does not determine the client server boundary. The component that imports and renders other component decides their nature.
    

React Internals Stuff

  

- Some important functions from call stack.
    

- ReactDOMRoot.render() is the user-side code we write, we first createRoot() and then render()
    
- scheduleUpdateOnFiber() tells React where to render.
    
- ensureRootIsScheduled() is an important call to ensure performConcurrentWorkOnRoot is scheduled.
    
- scheduleCallback() is the actual scheduling.
    
- workLoop() is how React Schedule processes the tasks.
    
- performConcurrentWorkOnRoot() is the scheduled task that is now being run in which our component is actually rendered.
    
- After the above render phase is the commit phase.
    
- commitRoot() commits the necessary DOM updates.
    
- commitMutationEffects()is actual update of host DOM
    
- flushPassiveEffects() flushes all passive effects created by useEffect()
    
- ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdUikSn9yocQnJ3BOj82CV-8F9gWgUFqfsTbRqPyJ2bc0o7U28frVtXe8C6kJ5Y2KUiY4jY6cFlM68pgwihXUR2rOUxN_a_Zmk-yMfvhjUl7T-9IpVRCz2HQljhJTosRMo97DSAKCsZapl0tkY_XzGqXOZd?key=hovy-OenfX6NFW0oYWzO0Q)
    

- Trigger: All the work starts here, initial mount or re-render by state hook, everything starts here. Here we tell React runtime which part of the app needs to be rendered and how it should be done. 
    
- Schedule: It is a Priority Queue.  scheduleCallback() is called in runtime code to schedule tasks like rendering or running effects. workLoop()inside the scheduler is how tasks are actually run.
    
- Render: It is the task scheduled, it means calculating the new Fiber Tree and figure out what updates are needed to apply to host DOM. performConcurrentWorkOnRoot() is created in the Trigger phase, prioritized in Scheduler and then actually run here. Think of it as if there is a little man, who walks around the Fiber Tree and checks if they need to re-render and figures out the necessary updates on host DOM.
    
- Commit: After a new Fiber tree is constructed and the minimum updates are derived, it is time to “commit” the updates to the host DOM.
    

- React Initial Mount:![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfTk-wcie0nJRakSelCR8_P-IQoxnqLCHSA9EeBx4DrWcHffK5_AyiJQT9to-_d541NUVDVFlpQ4l7VhnjDKjPPwCImKzZOW4C6E9itFnDWZ3ULa4Il7l3rly-Kqi_pJHlARXD0j9t2Ez282wV48iOdmnaR?key=hovy-OenfX6NFW0oYWzO0Q)
    

- FiberRoot Node: This is the root node of the Fiber tree. It represents the React application at its highest level.
    
- Current: This points to a child FiberNode, which in this case is a:
    

- HostRoot: This FiberNode represents the root DOM node for the React app. It acts as a bridge between the React component tree and the browser’s DOM tree.
    
- From the HostRoot, there’s a branch representing a functional component:
    

- * **FunctionComponent**: This represents a React component defined using a JavaScript function. 
    

  

This functional component has three child nodes, each being:

- * **HostComponent**: These FiberNodes represent HTML elements like `<div>`, `<a>`, and `<button>` that the functional component renders.  
    

  

React starts by creating a Fiber tree that mirrors the component hierarchy.

1. It starts at the FiberRoot and iterates through its children (in this case the HostRoot).
    
2. For each HostComponent encountered, React creates a corresponding DOM node in the browser.
    

The image depicts this initial render where React creates the following DOM structure:

HTML

- <div>
    
-   <a></a>
    
-   <button></button>
    
- </div>
    

  

-   
    
- Fiber is the architecture of how React holds internal representation of the App state. A tree consisting of  FiberRootNode and FiberNodes.
    

- FiberRootNode: Special node acts like React root. Holds meta info about the app. Current points to actual Fiber Tree, and re-points to new HostRoot every time a new Fiber Tree is constructed.
    
- FiberNode: important properties are
    

- Tag
    
- stateNode: points to other backing data.  For a HostComponent FiberNode, the "backing DOM node" refers to the actual HTML element in the browser's DOM that this React component creates and manages. Essentially, it's highlighting the connection between React's internal representation (Fiber) and the real element displayed on the screen (DOM). The HostComponent FiberNode acts as a bridge between the two, with its stateNode property pointing to the corresponding DOM element. 
    
- child sibling and return together form a tree-like structure.
    
- elementType which is the component function or intrinsic HTML tag we provide.
    
- Flags indicate updates to apply in Commit phase and subtreeFlags are for subtree.
    
- Lanes indicate the priority of pending updates. childLanes for subtree.
    
- memoizedState points to important data for FunctionComponent it means the hooks.
    

-   
    

  

Managing State best practices:

- Group Related States:
    

- Maybe if two state variables change together, it might be a good idea to unify them into a single state variable.
    

|   |
|---|
|// For example if we have something like this  <br>  <br>const [x, setX] = useState(0);  <br>const [y, setY] = useState(0);  <br>  <br>// And we both change together, we might want to format it to something like this:  <br>  <br>const [position, setPosition] = useState({ x: 0, y: 0});|

- Avoid contradictions in state
    

|   |
|---|
|// Something like this can be confusing and can cause errors. We probably do not want isSending and isSent true at the same time  <br>  <br>const [isSending, setIsSending] = useState(false);  <br>const [isSent, setIsSent] = useState(false);  <br>  <br>// Instead we can probably replace it something like an enum:<br><br>  <br><br>const [status, setStatus] = useState('typing');|

- Avoid redundant states: If you calculate some information from the component’s props or its existing state variables during rendering you should not put that information into that component state. A common example:
    

|   |
|---|
|function Message({ messageColor }) {  <br>  const [color, setColor] = useState(messageColor);  <br>  <br>// Here the problem is if the parent component passes a different value of messageColor later, the state variable would not be updated. State is only initialized during the first render. This is also called "Mirroring". Instead you should use the prop directly in your code. Mirroring only makes sense when you want to ignore all updates for a specific prop  <br>  <br>function Message({ initialColor }) {  <br>// The `color` state variable holds the *first* value of `initialColor`.  <br>// Further changes to the `initialColor` prop are ignored.  <br>const [color, setColor] = useState(initialColor);|
||

- Avoid duplication in state
    
- Avoid deeply nested states: Instead consider flattening it.
    
-   
    

Lifting state:

- Sometimes, you want the state of two components to always change together. To do it, remove state from both of them, move it to their closest common parent, and then pass it down to them via props. This is known as lifting state up,
    
- This allows for a single source of truth
    
- Consider components as “controlled” (driven by props) or “uncontrolled” (driven by state).
    

  

Updating Arrays in State:

- [1](https://react.dev/learn/updating-arrays-in-state#adding-to-an-array), 
    

- Arrays are mutable in Javascript but you should treat them as immutable when you store them in state, When changing make a copy or create a new one.
    
- Use spread syntax, slice, map, filter etc.
    
-   
    

  

Prop Drilling:

- Refers to the process of passing down props through multiple layers of components.
    
- As components get nested deeper, managing the flow of props becomes challenging.
    
- This also causes tight coupling of elements.
    
- Performance overhead is also introduced.
    
- Solution would be to use the State Management Libraries , HOCs or the Context API.
    

  

React Contexts:

- Context API is a React API that can solve a lot of problems with state management and how to pass them to different components.
- It can be used to share data with multiple components without having to pass data through props manually.
- createContext is required as a function for React
- Provider is required to wrap the components that are going to access the context.
- Consumer tells the context api which components are going to access or consume the data.
- useContext is a hook for the Context API. It receives a single argument, which is the context you want to have access to. Use useContext over Consumer.
- const notes = useContext(NotesContext);