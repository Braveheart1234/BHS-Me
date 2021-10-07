---
title: Working with Svelte stores
slug: Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_stores
tags:
  - Beginner
  - Frameworks
  - JavaScript
  - Learn
  - Stores
  - Svelte
  - client-side
---
<div>{{LearnSidebar}}<br>
{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_reactivity_lifecycle_accessibility","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_TypeScript", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}</div>

<p>In the last article we completed the development of our app, finished organizing it into components, and discussed some advanced techniques for dealing with reactivity, working with DOM nodes, and exposing component functionality. In this article we will show another way to handle state management in Svelte — <a href="https://svelte.dev/tutorial/writable-stores">Stores</a>. Stores are global data repositories that hold values. Components can subscribe to stores and receive notifications when their values change.</p>

<table>
 <tbody>
  <tr>
   <th scope="row">Prerequisites:</th>
   <td>
    <p>At minimum, it is recommended that you are familiar with the core <a href="/en-US/docs/Learn/HTML">HTML</a>, <a href="/en-US/docs/Learn/CSS">CSS</a>, and <a href="/en-US/docs/Learn/JavaScript">JavaScript</a> languages, and have knowledge of the <a href="/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line">terminal/command line</a>.</p>

    <p>You'll need a terminal with node + npm installed to compile and build your app.</p>
   </td>
  </tr>
  <tr>
   <th scope="row">Objective:</th>
   <td>Learn how to use Svelte stores</td>
  </tr>
 </tbody>
</table>

<p>Using stores we will create an <code>Alert</code> component that shows notifications on screen, which can receive messages from any component. In this case, the <code>Alert</code> component is independent from the rest — it is not a parent or child of any other — so the messages don't fit into the component hierarchy.</p>

<p>We will also see how to develop our own custom store to persist the todo information to <a href="/en-US/docs/Web/API/Web_Storage_API">web storage</a>, allowing our todos to persist over page reloads.</p>

<h2 id="Code_along_with_us">Code along with us</h2>

<h3 id="Git">Git</h3>

<p>Clone the github repo (if you haven't already done it) with:</p>

<pre class="brush: bash">git clone https://github.com/opensas/mdn-svelte-tutorial.git</pre>

<p>Then to get to the current app state, run</p>

<pre class="brush: bash">cd mdn-svelte-tutorial/06-stores</pre>

<p>Or directly download the folder's content:</p>

<pre class="brush: bash">npx degit opensas/mdn-svelte-tutorial/06-stores</pre>

<p>Remember to run <code>npm install &amp;&amp; npm run dev</code> to start your app in development mode.</p>

<h3 id="REPL">REPL</h3>

<p>To code along with us using the REPL, start at</p>

<p><a href="https://svelte.dev/repl/d1fa84a5a4494366b179c87395940039?version=3.23.2">https://svelte.dev/repl/d1fa84a5a4494366b179c87395940039?version=3.23.2</a></p>

<h2 id="Dealing_with_our_app_state">Dealing with our app state</h2>

<p>We have already seen how our components can communicate with each other using props, two-way data binding, and events. In all these cases we were dealing with communication between parent and child components.</p>

<p>But not all application state belongs inside your application's component hierarchy. For example, information about the logged in user, or whether the dark theme is selected or not.</p>

<p>Sometimes, your app state will need to be accessed by multiple components that are not hierarchically related, or by a regular JavaScript module.</p>

<p>Moreover, when your app becomes complicated and your component hierarchy gets complex, it might become too difficult for components to relay data between each other. In that case, moving to a global data store might be a good option. If you’ve already worked with <a href="https://redux.js.org/">Redux</a> or <a href="https://vuex.vuejs.org/">Vuex</a>, then you'll be familiar with how this kind of store works. Svelte stores offer similar features for state management.</p>

<p>A store is an object with a <code>subscribe()</code> method that allows interested parties to be notified whenever the store value changes, and an optional <code>set()</code> method that allows you to set new values for the store. This minimal API is known as the <a href="https://svelte.dev/docs#Store_contract">store contract</a>.</p>

<p>Svelte provides functions for creating <a href="https://svelte.dev/docs#readable">readable</a>, <a href="https://svelte.dev/docs#writable">writable</a>, and <a href="https://svelte.dev/docs#derived">derived</a> stores in the <code>svelte/store</code> module.</p>

<p>Svelte also provides a very intuitive way to integrate stores into its reactivity system using the <a href="https://svelte.dev/docs#4_Prefix_stores_with_%24_to_access_their_values">reactive <code>$store</code> syntax</a>. If you create your own stores honoring the store contract, you get this reactivity syntactic sugar for free.</p>

<h2 id="Creating_the_Alert_component">Creating the Alert component</h2>

<p>To show how to work with stores, we will create an <code>Alert</code> component. These kind of widgets might also be known as popup notifications, toast, or notification bubbles.</p>

<p>Our <code>Alert</code> component will displayed by the <code>App</code> component, but any component can send notifications to it; whenever a notification arrives the <code>Alert</code> component will be in charge of displaying it on screen.</p>

<h3 id="Creating_a_store">Creating a store</h3>

<p>Let's start by creating a writable store. Any component will be able to write to this store, and the <code>Alert</code> component will subscribe to it and display a message whenever the store is modified.</p>

<ol>
 <li>
  <p>Create a new file — <code>stores.js</code> — inside your <code>src</code> directory.</p>
 </li>
 <li>
  <p>Give it the following content:</p>

  <pre class="brush: js">import { writable } from 'svelte/store'

export const alert = writable('Welcome to the To-Do list app!')</pre>
 </li>
</ol>

<div class="notecard note">
<p><strong>Note:</strong> Stores can be defined and used outside of Svelte components, so you can organize them in any way you please.</p>
</div>

<p>In the above code we import the <code>writable()</code> function from <code>svelte/store</code> and use it to create a new store called <code>alert</code> with an initial value of "Welcome to the To-Do list app!". We then <code>export</code> the store.</p>

<h3 id="Creating_the_actual_component">Creating the actual component</h3>

<p>Let's now create our <code>Alert</code> component and see how we can read values from the store.</p>

<ol>
 <li>
  <p>Create another new file named <code>src/components/Alert.svelte</code>.</p>
 </li>
 <li>
  <p>Give it the following content:</p>

  <pre class="brush: html">&lt;script&gt;
  import { alert } from '../stores.js'
  import { onDestroy } from 'svelte'

  let alertContent = ''

  const unsubscribe = alert.subscribe(value =&gt; alertContent = value)

  onDestroy(unsubscribe)
&lt;/script&gt;

{#if alertContent}
&lt;div on:click={() =&gt; alertContent = ''}&gt;
  &lt;p&gt;{ alertContent }&lt;/p&gt;
&lt;/div&gt;
{/if}

&lt;style&gt;
div {
  position: fixed;
  cursor: pointer;
  margin-right: 1.5rem;
  margin-left: 1.5rem;
  margin-top: 1rem;
  right: 0;
  display: flex;
  align-items: center;
  border-radius: 0.2rem;
  background-color: #565656;
  color: #fff;
  font-size: 0.875rem;
  font-weight: 700;
  padding: 0.5rem 1.4rem;
  font-size: 1.5rem;
  z-index: 100;
  opacity: 95%;
}
div p {
  color: #fff;
}
div svg {
  height: 1.6rem;
  fill: currentColor;
  width: 1.4rem;
  margin-right: 0.5rem;
}
&lt;/style&gt;</pre>
 </li>
</ol>

<p>Let's walk through this piece of code in detail.</p>

<ul>
 <li>At the beginning we import the <code>alert</code> store.</li>
 <li>Next we import the <code>onDestroy()</code> lifecycle function, which lets us execute a callback after the component has been unmounted.</li>
 <li>We then create a local variable named <code>alertContent</code>. Remember that we can access top-level variables from the markup, and whenever they are modified the DOM will update accordingly.</li>
 <li>Then we call the method <code>alert.subscribe()</code>, passing it a callback function as a parameter. Whenever the value of the store changes, the callback function will be called with the new value as its parameter. In the callback function we just assign the value we receive to the local variable, which will trigger the update of the component's DOM.</li>
 <li>The <code>subscribe()</code> method also returns a clean-up function, which takes care of releasing the subscription. So we subscribe when the component is being initialized, and use <code>onDestroy</code> to unsubscribe when the component is unmounted.</li>
 <li>Finally we use the <code>alertContent</code> variable in our markup, and if the user clicks on the alert we clean it.</li>
 <li>At the end we include a few CSS lines to style our <code>Alert</code> component.</li>
</ul>

<p>This setup allows us to work with stores in a reactive way. When the value of the store changes, the callback is executed. There we assign a new value to a local variable, and thanks to Svelte reactivity all our markup and reactive dependencies are updated accordingly.</p>

<h3 id="Using_the_component">Using the component</h3>

<p>Let's now use our component.</p>

<ol>
 <li>
  <p>In <code>App.svelte</code> we'll import the component; add the following import statement below the existing one:</p>

  <pre class="brush: js">import Alert from './components/Alert.svelte'</pre>
 </li>
 <li>
  <p>Then call the <code>Alert</code> component just above the <code>Todos</code> call, like this:</p>

  <pre class="brush: html">&lt;Alert /&gt;
&lt;Todos {todos} /&gt;</pre>
 </li>
 <li>
  <p>Load your test app now, and you should now see the <code>Alert</code> message on screen. You may click on it to dismiss it.</p>

  <p><img alt="A simple notification in the top right hand corner of an app saying welcome to todo list app" src="01-alert-message.png"></p>
 </li>
</ol>

<h2 id="Making_stores_reactive_with_the_reactive_store_syntax">Making stores reactive with the reactive <code>$store</code> syntax</h2>

<p>This works, but you'll have to copy and paste all this code every time you want to subscribe to a store:</p>

<pre class="brush: js">&lt;script&gt;
  import myStore from './stores.js'
  import { onDestroy } from 'svelte'

  let myStoreContent = ''

  const unsubscribe = myStore.subscribe(value =&gt; myStoreContent = value)

  onDestroy(unsubscribe)
&lt;/script&gt;

{myStoreContent}</pre>

<p>That's too much boilerplate for Svelte! Being a compiler, Svelte has more resources to make our lives easier. In this case Svelte provides the reactive <code>$store</code> syntax, also known as auto-subscription. In simple terms, you just prefix the store with the <code>$</code> sign and Svelte will generate the code to make it reactive automatically. So our previous code block can be replaced with this:</p>

<pre class="brush: html">&lt;script&gt;
  import myStore from './stores.js'
&lt;/script&gt;

{$myStore}</pre>

<p>And <code>$myStore</code> will be fully reactive. This also applies to your own custom stores. If you implement the <code>subscribe()</code> and <code>set()</code> methods, like we'll do later, the reactive <code>$store</code> syntax will also apply to your stores.</p>

<ol>
 <li>
  <p>Let's apply this to our <code>Alert</code> component. Update the <code>&lt;script&gt;</code> and markup sections of <code>Alert.svelte</code> as follows:</p>

  <pre class="brush: html">&lt;script&gt;
  import { alert } from '../stores.js'
&lt;/script&gt;

{#if $alert}
&lt;div on:click={() =&gt; $alert = ''}&gt;
  &lt;p&gt;{ $alert }&lt;/p&gt;
&lt;/div&gt;
{/if}

</pre>
 </li>
 <li>
  <p>Check your app again and you'll see that this works just like before. That's much better!</p>
 </li>
</ol>

<p>Behind the scenes Svelte has generated the code to declare the local variable <code>$alert</code>, subscribe to the <code>alert</code> store, update <code>$alert</code> whenever the store's content is modified, and unsubscribe when the component is unmounted. It will also generate the <code>alert.set(...)</code> statements whenever we assign a value to <code>$alert</code>.</p>

<p>The end result of this nifty trick is that you can access global stores just as easily as using reactive local variables.</p>

<p>This is a perfect example of how Svelte puts the compiler in charge of better developer ergonomics, not only saving us from typing boiler plate, but also generating less error-prone code.</p>

<h2 id="Writing_to_our_store">Writing to our store</h2>

<p>Writing to our store is just a matter of importing it and executing <code>$store = 'new value'</code>. Let's use it in our <code>Todos</code> component.</p>

<ol>
 <li>
  <p>Add the following <code>import</code> statement below the existing ones:</p>

  <pre class="brush: js">import { alert } from '../stores.js'</pre>
 </li>
 <li>
  <p>Update your <code>addTodo()</code> function like so:</p>

  <pre class="brush: js">function addTodo(name) {
  todos = [...todos, { id: newTodoId, name, completed: false }]
  $alert = `Todo '${name}' has been added`
}</pre>
 </li>
 <li>
  <p>Update <code>removeTodo()</code> like so:</p>

  <pre class="brush: js">function removeTodo(todo) {
  todos = todos.filter(t =&gt; t.id !== todo.id)
  todosStatus.focus()             // give focus to status heading
  $alert = `Todo '${todo.name}' has been deleted`
}  </pre>
 </li>
 <li>
  <p>Update the <code>updateTodo()</code> function to this:</p>

  <pre class="brush: js">function updateTodo(todo) {
  const i = todos.findIndex(t =&gt; t.id === todo.id)
  if (todos[i].name !== todo.name)            $alert = `todo '${todos[i].name}' has been renamed to '${todo.name}'`
  if (todos[i].completed !== todo.completed)  $alert = `todo '${todos[i].name}' marked as ${todo.completed ? 'completed' : 'active'}`
  todos[i] = { ...todos[i], ...todo }
}</pre>
 </li>
 <li>
  <p>Add the following reactive block beneath the block that starts with <code>let filter = 'all'</code>:</p>

  <pre class="brush: js">$: {
  if (filter === 'all')               $alert = 'Browsing all todos'
  else if (filter === 'active')       $alert = 'Browsing active todos'
  else if (filter === 'completed')    $alert = 'Browsing completed todos'
}</pre>
 </li>
 <li>
  <p>And finally for now, update the <code>const checkAllTodos</code> and <code>const removeCompletedTodos</code> blocks as follows:</p>

  <pre class="brush: js">const checkAllTodos = (completed) =&gt; {
  todos = todos.map(t =&gt; ({...t, completed}))
  $alert = `${completed ? 'Checked' : 'Unchecked'} ${todos.length} todos`
}
const removeCompletedTodos = () =&gt; {
  $alert = `Removed ${todos.filter(t =&gt; t.completed).length} todos`
  todos = todos.filter(t =&gt; !t.completed)
}</pre>
 </li>
 <li>
  <p>So basically, we've imported the store and updated it on every event, which causes a new alert to show each time. Have a look at your app again, and try adding/deleting/updating a few todos!</p>
 </li>
</ol>

<p>As soon as we execute <code>$alert = ...</code>, Svelte will run <code>alert.set(...)</code>. Our <code>Alert</code> component — like every subscriber to the alert store — will be notified when it receives a new value, and thanks to Svelte reactivity its markup will be updated.</p>

<p>We could do the same within any component or <code>.js</code> file.</p>

<div class="notecard note">
<p><strong>Note:</strong> Outside of Svelte components you cannot use the <code>$store</code> syntax. That's because the Svelte compiler won't touch anything outside of Svelte components. In that case you'll have to rely on the <code>store.subscribe()</code> and <code>store.set()</code> methods.</p>
</div>

<h2 id="Improving_our_Alert_component">Improving our Alert component</h2>

<p>It's a bit annoying having to click on the alert to get rid of it. It would be better if the notification just disappeared after a couple of seconds.</p>

<p>Lets see how to do that. We'll specify a prop with the milliseconds to wait before clearing the notification, and we'll define a timeout to remove the alert. We'll also take care of clearing the timeout when the <code>Alert</code> component is unmounted to prevent memory leaks.</p>

<ol>
 <li>
  <p>Update the <code>&lt;script&gt;</code> section of your <code>Alert.svelte</code> component like so:</p>

  <pre class="brush: js">&lt;script&gt;
  import { onDestroy } from 'svelte'
  import { alert } from '../stores.js'

  export let ms = 3000
  let visible
  let timeout

  const onMessageChange = (message, ms) =&gt; {
    clearTimeout(timeout)
    if (!message) {               // hide Alert if message is empty
      visible = false
    } else {
      visible = true                                              // show alert
      if (ms &gt; 0) timeout = setTimeout(() =&gt; visible = false, ms) // and hide it after ms milliseconds
    }
  }
  $: onMessageChange($alert, ms)      // whenever the alert store or the ms props changes run onMessageChange

  onDestroy(()=&gt; clearTimeout(timeout))           // make sure we clean-up the timeout

&lt;/script&gt;</pre>
 </li>
 <li>
  <p>And update the <code>Alert.svelte</code> markup section like so:</p>

  <pre class="brush: html">{#if visible}
&lt;div on:click={() =&gt; visible = false}&gt;
  &lt;svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"&gt;&lt;path d="M12.432 0c1.34 0 2.01.912 2.01 1.957 0 1.305-1.164 2.512-2.679 2.512-1.269 0-2.009-.75-1.974-1.99C9.789 1.436 10.67 0 12.432 0zM8.309 20c-1.058 0-1.833-.652-1.093-3.524l1.214-5.092c.211-.814.246-1.141 0-1.141-.317 0-1.689.562-2.502 1.117l-.528-.88c2.572-2.186 5.531-3.467 6.801-3.467 1.057 0 1.233 1.273.705 3.23l-1.391 5.352c-.246.945-.141 1.271.106 1.271.317 0 1.357-.392 2.379-1.207l.6.814C12.098 19.02 9.365 20 8.309 20z"/&gt;&lt;/svg&gt;
  &lt;p&gt;{ $alert }&lt;/p&gt;
&lt;/div&gt;
{/if}</pre>
 </li>
</ol>

<p>Here we first create the prop <code>ms</code> with a default value of 3000 (milliseconds). Then we create an <code>onMessageChange()</code> function that will take care of controlling whether the Alert is visible or not. With <code>$: onMessageChange($alert, ms)</code> we tell Svelte to run this function whenever the <code>$alert</code> store or the <code>ms</code> prop changes.</p>

<p>Whenever the <code>$alert</code> store changes, we'll clean up any pending timeout. If <code>$alert</code> is empty, we set <code>visible</code> to <code>false</code> and the <code>Alert</code> will be removed from the DOM. If it is not empty, we set <code>visible</code> to <code>true</code> and use the <code>setTimeout()</code> function to clear the alert after <code>ms</code> milliseconds.</p>

<p>Finally, with the <code>onDestroy()</code> lifecycle function, we make sure to call the <code>clearTimeout()</code> function.</p>

<p>We also added an SVG icon above the alert paragraph, to make it look a bit nicer. Try it out again, and you should see the changes.</p>

<h2 id="Making_our_Alert_component_accessible">Making our Alert component accessible</h2>

<p>Our <code>Alert</code> component is working fine, but it's not very friendly to assistive technologies. The problem is elements that are dynamically added and removed from the page. While visually evident to users who can see the page, they may not be so obvious to users of assistive technologies, like screen readers. To handle those situations, we can take advantage of <a href="/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions">ARIA live regions</a>, which provide a way to programmatically expose dynamic content changes so that they can be detected and announced by assistive technologies.</p>

<p>We can declare a region that contains dynamic content that should be announced by assistive technologies with the <code>aria-live</code> property followed by the politeness setting, which is used to set the priority with which screen readers should handle updates to that regions. The possible settings are <code>off</code>, <code>polite</code>, or <code>assertive</code>.</p>

<p>For common situations, you also have several predefined specialized <code>role</code> values that can be used, like <code>log</code>, <code>status</code> and <code>alert</code>.</p>

<p>In our case, just adding a <code>role="alert"</code> to the <code>&lt;div&gt;</code> container will do the trick, like this:</p>

<pre class="brush: html">&lt;div role="alert" on:click={() =&gt; visible = false}&gt;</pre>

<p>In general, testing your applications using screen readers is a good idea, not only to discover accessibility issues but also to get used to how visually impaired people use the Web. You have several options, like <a href="https://www.nvaccess.org/">NVDA</a> for Windows, <a href="http://www.chromevox.com/">ChromeVox</a> for Chrome, <a href="https://wiki.gnome.org/Projects/Orca">Orca</a> on Linux, and <a href="https://www.apple.com/accessibility/osx/voiceover/">VoiceOver</a> for Mac OS X and iOS, among other options.</p>

<p>To learn more about detecting and fixing accessibility issues check out our <a href="/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility">Handling common accessibility problems</a> article.</p>

<h2 id="Using_the_store_contract_to_persist_our_todos">Using the store contract to persist our todos</h2>

<p>Our little app lets us manage our todos quite easily, but is rather useless if we always get the same list of hardcoded todos when we reload it. To make it truly useful, we have to find out how to persist our todos.</p>

<p>First we need some way for our <code>Todos</code> component to give back the updated todos to its parent. We could emit an updated event with the list of todos, but it's easier just to bind the <code>todos</code> variable. Let's open <code>App.svelte</code> and try it.</p>

<ol>
 <li>
  <p>First of all, add the following line below your <code>todos</code> array:</p>

  <pre class="brush: js">$: console.log('todos', todos)</pre>
 </li>
 <li>
  <p>Next, update your <code>Todos</code> component call as follows:</p>

  <pre class="brush: html">&lt;Todos bind:todos /&gt;</pre>

  <div class="notecard note">
  <p><strong>Note:</strong> <code>&lt;Todos bind:todos /&gt;</code> is just a shortcut for <code>&lt;Todos bind:todos={todos} /&gt;</code>.</p>
  </div>
 </li>
 <li>
  <p>Go back to your app, try adding some todos, then go to your developer tools web console. You'll see that every modification we make to our todos is reflected in the <code>todos</code> array defined in <code>App.svelte</code> thanks to the <code>bind</code> directive.</p>
 </li>
</ol>

<p>Now we have to find a way to persist these todos. We could implement some code in our <code>App.svelte</code> component to read and save our todos to <a href="/en-US/docs/Web/API/Web_Storage_API">web storage</a> or to a web service.<br>
 But wouldn't it be better if we could develop some generic store that allows us to persist its content? This would allow us to use it just like any other store, and abstract away the persistence mechanism. We could create a store that syncs its content to web storage, and later develop another one that syncs against a web service. Switching between them would be trivial and we wouldn't have to touch <code>App.svelte</code> at all.</p>

<h3 id="Saving_our_todos">Saving our todos</h3>

<p>So let's start by using a regular writable store to save our todos.</p>

<ol>
 <li>
  <p>Open the file <code>stores.js</code> and add the following store below the existing one:</p>

  <pre class="brush: js">export const todos = writable([])</pre>
 </li>
 <li>
  <p>That was easy. Now we need to import the store and use it in <code>App.svelte</code>. Just remember that to access the todos now we have to use the <code>$todos</code> reactive <code>$store</code> syntax.</p>

  <p>Update your <code>App.svelte</code> file like this:</p>

  <pre class="brush: html">&lt;script&gt;
  import Todos from './components/Todos.svelte'
  import Alert from './components/Alert.svelte'

  import { todos } from './stores.js'

  $todos = [
    { id: 1, name: 'Create a Svelte starter app', completed: true },
    { id: 2, name: 'Create your first component', completed: true },
    { id: 3, name: 'Complete the rest of the tutorial', completed: false }
  ]

&lt;/script&gt;

&lt;Alert /&gt;
&lt;Todos bind:todos={$todos} /&gt;</pre>
 </li>
 <li>
  <p>Try it out; everything should work. Next we'll see how to define our own custom stores.</p>
 </li>
</ol>

<h3 id="How_to_implement_a_store_contract_The_theory">How to implement a store contract: The theory</h3>

<p>You can create your own stores without relying on <code>svelte/store</code> by implementing the store contract. Its features must work like so:</p>

<ol>
 <li>A store must contain a <code>subscribe()</code> method, which must accept as its argument a subscription function. All of a store's active subscription functions must be called whenever the store's value changes.</li>
 <li>The <code>subscribe()</code> method must return an <code>unsubscribe()</code> function, which when called must stop its subscription.</li>
 <li>A store may optionally contain a <code>set()</code> method, which must accept as its argument a new value for the store, and which synchronously calls all of the store's active subscription functions. A store with a <code>set()</code> method is called a writable store.</li>
</ol>

<p>First of all, let's add the following <code>console.log()</code> statements to our <code>App.svelte</code> component to see the <code>todos</code> store and its content in action. Add these lines below the <code>todos</code> array:</p>

<pre class="brush: js">console.log('todos store - todos:', todos)
console.log('todos store content - $todos:', $todos)</pre>

<p>When you run the app now, you'll see something like this in your web console:</p>

<p><img alt="web console showing the functions and contents of the todos store" src="02-svelte-store-in-action.png"></p>

<p>As you can see, our store is just an object containing <code>subscribe()</code>, <code>set()</code>, and <code>update()</code> methods, and <code>$todos</code> is our array of todos.</p>

<p>Just for reference, here's a basic working store implemented from scratch:</p>

<pre class="brush: js">export const writable = (initial_value = 0) =&gt; {

  let value = initial_value         // content of the store
  let subs = []                     // subscriber's handlers

  const subscribe = (handler) =&gt; {
    subs = [...subs, handler]                                 // add handler to the array of subscribers
    handler(value)                                            // call handler with current value
    return () =&gt; subs = subs.filter(sub =&gt; sub !== handler)   // return unsubscribe function
  }

  const set = (new_value) =&gt; {
    if (value === new_value) return         // same value, exit
    value = new_value                       // update value
    subs.forEach(sub =&gt; sub(value))         // update subscribers
  }

  const update = (update_fn) =&gt; set(update_fn(value))   // update function

  return { subscribe, set, update }       // store contract
}</pre>

<p>Here we declare <code>subs</code>, which is an array of subscribers. In the <code>subscribe()</code> method we add the handler to the <code>subs</code> array and return a function that, when executed, will remove the handler from the array.</p>

<p>When we call <code>set()</code>, we update the value of the store, and call each handler — passing the new value as a parameter.</p>

<p>Anyway, usually you don't implement stores from scratch; instead you'd use the writable store to create <a href="https://svelte.dev/tutorial/custom-stores">custom stores</a> with domain-specific logic. In the following example we create a counter store, which will only allow us to add one to the counter or reset its value:</p>

<pre class="brush: js">import { writable } from 'svelte/store';
function myStore() {
  const { subscribe, set, update } = writable(0);

  return {
    subscribe,
    addOne: () =&gt; update(n =&gt; n + 1),
    reset: () =&gt; set(0)
  };
}</pre>

<p>If our To-do list app gets too complex, we could let our todos store handle every state modification. We could move all the methods that modify the <code>todo</code> array (like <code>addTodo()</code>, <code>removeTodo()</code>, etc) from our <code>Todos</code> component to the store. If you have a central place where all the state modification is applied, components could just call those methods to modify the app's state and reactively display the info exposed by the store. Having a unique place to handle state modifications makes it easier to reason about the state flow and spot issues.</p>

<p>Svelte won't force you to organize your state management in a specific way, it just provides the tools for you to choose how to handle it.</p>

<h3 id="Implementing_our_custom_todos_store">Implementing our custom todos store</h3>

<p>Our To-do list app is not particularly complex, so we won't move all our modification methods into a central place. We'll just leave them as they are, and instead concentrate on persisting our todos.</p>

<div class="notecard note">
<p><strong>Note:</strong> If you are following this guide working from the Svelte REPL you won't be able to complete this step. For security reasons the Svelte REPL works in a sandboxed environment which will not let you access web storage, and you will get a "The operation is insecure" error. In order to follow this section you'll have to clone the repo and go to the <code>mdn-svelte-tutorial/06-stores</code> folder or you can directly download the folder's content with <code>npx degit opensas/mdn-svelte-tutorial/06-stores</code>.</p>
</div>

<p>So, to implement a custom store that saves its content to web storage, we will need a writable store that:</p>

<ul>
 <li>Initially reads the value from web storage, and if it's not present, initializes it with a default value.</li>
 <li>Whenever the value is modified, updates the store itself and also the data in local storage.</li>
</ul>

<p>Moreover, because web storage only supports saving string values, we will have to convert from object to string when saving, and vice versa when we are loading the value from local storage.</p>

<ol>
 <li>
  <p>Create a new file called <code>localStore.js</code>, in your <code>src</code> directory.</p>
 </li>
 <li>
  <p>Give it the following content:</p>

  <pre class="brush: js">import { writable } from 'svelte/store';

export const localStore = (key, initial) =&gt; {                 // receives the key of the local storage and an initial value

  const toString = (value) =&gt; JSON.stringify(value, null, 2)  // helper function
  const toObj = JSON.parse                                    // helper function

  if (localStorage.getItem(key) === null) {                   // item not present in local storage
    localStorage.setItem(key, toString(initial))              // initialize local storage with initial value
  }

  const saved = toObj(localStorage.getItem(key))              // convert to object

  const { subscribe, set, update } = writable(saved)          // create the underlying writable store

  return {
    subscribe,
    set: (value) =&gt; {
      localStorage.setItem(key, toString(value))              // save also to local storage as a string
      return set(value)
    },
    update
  }
}</pre>

  <ul>
   <li>Our <code>localStore</code> will be a function that when executed initially reads its content from web storage, and returns an object with three methods: <code>subscribe()</code>, <code>set()</code>, and <code>update()</code>.</li>
   <li>When we create a new <code>localStore</code>, we'll have to specify the key of the web storage and an initial value. We then check if the value exists in web storage and, if not, we create it.</li>
   <li>We use the <code><a href="/en-US/docs/Web/API/Storage/getItem">localStorage.getItem(key)</a></code> and <code><a href="/en-US/docs/Web/API/Storage/setItem">localStorage.setItem(key, value)</a></code> methods to read and write information to web storage, and the <code><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString">toString()</a></code> and <code>toObj()</code> (which uses <code><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse">JSON.parse()</a></code>) helper functions to convert the values.</li>
   <li>Next, we convert the string content received from the web storage to an object, and save that object in our store.</li>
   <li>Finally, every time we update the contents of the store, we also update the web storage, with the value converted to a string.</li>
  </ul>

  <p>Notice that we only had to redefine the <code>set()</code> method, adding the operation to save the value to web storage. The rest of the code is mostly initializing and converting stuff.</p>
 </li>
 <li>
  <p>Now we will use our local store from <code>stores.js</code> to create our locally persisted todos store.</p>

  <p>Update <code>stores.js</code> like so:</p>

  <pre class="brush: js">import { writable } from 'svelte/store'
import { localStore } from './localStore.js'

export const alert = writable('Welcome to the To-Do list app!')

const initialTodos = [
  { id: 1, name: 'Visit MDN web docs', completed: true },
  { id: 2, name: 'Complete the Svelte Tutorial', completed: false },
]

export const todos = localStore('mdn-svelte-todo', initialTodos)</pre>

  <p>Using <code>localStore('mdn-svelte-todo', initialTodos)</code>, we are configuring the store to save the data in web storage under the key <code>mdn-svelte-todo</code>. We also set a couple of todos as initial values.</p>
 </li>
 <li>
  <p>Now let's get rid of the hardcoded todos in <code>App.svelte</code>. Update its contents like this — we are basically just deleting the <code>$todos</code> array and the <code>console.log()</code> statements:</p>

  <pre class="brush: html">&lt;script&gt;
  import Todos from './components/Todos.svelte'
  import Alert from './components/Alert.svelte'

  import { todos } from './stores.js'
&lt;/script&gt;

&lt;Alert /&gt;
&lt;Todos bind:todos={$todos} /&gt;</pre>

  <div class="notecard note">
  <p><strong>Note:</strong> This is the only change we have to make in order to use our custom store. <code>App.svelte</code> is completely transparent in terms of what kind of store we are using.</p>
  </div>
 </li>
 <li>
  <p>Go ahead and try your app again. Create a few todos and then close the browser. You may even stop the Svelte server and restart it. Upon revisiting the URL, your todos will still be there.</p>
 </li>
 <li>
  <p>You can also inspect it in the DevTools console. In the web console, enter the command <code>localStorage.getItem('mdn-svelte-todo')</code>. Make some changes to your app, like pressing the <em>Uncheck All</em> button, and check the web storage content once more. You will get something like this:</p>

  <p><img alt="todo app with web console view alongside it, showing that when a todo is changed in the app, the corresponding entry is changed in web storage" src="03-persisting-todos-to-local-storage.png"></p>
 </li>
</ol>

<p>Svelte stores provide a very simple and lightweight, but extremely powerful, way to handle complex app state from a global data store in a reactive way. And because Svelte compiles our code, it can provide the <a href="https://svelte.dev/docs#4_Prefix_stores_with_%24_to_access_their_values"><code>$store</code> auto-subscription syntax</a> that allows us to work with stores in the same way as local variables. Because stores has a minimal API, it's very simple to create our custom stores to abstract away the inner workings of the store itself.</p>

<h2 id="Bonus_track_Transitions">Bonus track: Transitions</h2>

<p>Let's change the subject now, and do something fun and different — let's add an animation to our alerts. Svelte provides a whole module to define <a href="https://svelte.dev/tutorial/transition">transitions</a> and <a href="https://svelte.dev/tutorial/animate">animations</a> so we can make our user interfaces more appealing.</p>

<p>A transition is applied with the <a href="https://svelte.dev/docs#transition_fn">transition:fn</a> directive, and is triggered by an element entering or leaving the DOM as a result of a state change. The svelte/transition module exports seven functions: <code>fade</code>, <code>blur</code>, <code>fly</code>, <code>slide</code>, <code>scale</code>, <code>draw</code>, and <code>crossfade</code>.</p>

<p>Let's give our <code>Alert</code> component a fly <code>transition</code>. We'll open the <code>Alert.svelte</code> file and import the <code>fly</code> function from the <code>svelte/transition</code> module.</p>

<ol>
 <li>
  <p>Put the following <code>import</code> statement below the existing ones:</p>

  <pre class="brush: js">import { fly } from 'svelte/transition'</pre>
 </li>
 <li>
  <p>To use it, update your opening <code>&lt;div&gt;</code> tag like so:</p>

  <pre class="brush: html">&lt;div role="alert" on:click={() =&gt; visible = false}
  transition:fly
&gt;</pre>

  <p>Transitions can also receive parameters, like this:</p>

  <pre class="brush: html">&lt;div role="alert" on:click={() =&gt; visible = false}
  transition:fly="\{{delay: 250, duration: 300, x: 0, y: -100, opacity: 0.5}}"
&gt;</pre>

  <div class="notecard note">
  <p><strong>Note:</strong> The double curly braces are not special Svelte syntax. It's just a literal JavaScript object being passed as a parameter to the fly transition.</p>
  </div>
 </li>
 <li>
  <p>Try your app out again — you'll see that the notifications now look a bit more appealing.</p>
 </li>
</ol>

<div class="notecard note">
<p><strong>Note:</strong> Being a compiler allows Svelte to optimize the size of our bundle by excluding features that are not used. In this case, if we compile our app for production with <code>npm run build</code>, our <code>public/build/bundle.js</code> file will weight a little less than 22KB. If we remove the <code>transitions:fly</code> directive Svelte is smart enough to realize the fly function is not being used and the <code>bundle.js</code> file size will drop down to just 18KB.</p>
</div>

<p>This is just the tip of the iceberg. Svelte has lots of options for dealing with animations and transitions. Svelte also supports specifying different transitions to apply when the element is added or removed from the DOM with the <code>in:fn</code>/<code>out:fn</code> directives, and it also allows you to define your <a href="https://svelte.dev/tutorial/custom-css-transitions">custom CSS</a> and <a href="https://svelte.dev/tutorial/custom-js-transitions">JavaScript</a> transitions. It also has several easing functions to specify the rate of change over time. Have a look at the <a href="https://svelte.dev/examples#easing">ease visualizer</a> to explore the various ease functions available.</p>

<h2 id="The_code_so_far">The code so far</h2>

<h3 id="Git_2">Git</h3>

<p>To see the state of the code as it should be at the end of this article, access your copy of our repo like this:</p>

<pre class="brush: bash">cd mdn-svelte-tutorial/07-next-steps</pre>

<p>Or directly download the folder's content:</p>

<pre class="brush: bash">npx degit opensas/mdn-svelte-tutorial/07-next-steps</pre>

<p>Remember to run <code>npm install &amp;&amp; npm run dev</code> to start your app in development mode.</p>

<h3 id="REPL_2">REPL</h3>

<p>To see the current state of the code in a REPL, visit:</p>

<p><a href="https://svelte.dev/repl/378dd79e0dfe4486a8f10823f3813190?version=3.23.2">https://svelte.dev/repl/378dd79e0dfe4486a8f10823f3813190?version=3.23.2</a></p>

<h2 id="Summary">Summary</h2>

<p>In this article we added two new features: an <code>Alert</code> component and persisting <code>todos</code> to web storage.</p>

<ul>
 <li>This allowed us to showcase some advanced Svelte techniques. We developed the <code>Alert</code> component to show how to implement cross-component state management using stores. We also saw how to auto-subscribe to stores to seamlessly integrate them with the Svelte reactivity system.</li>
 <li>Then we saw how to implement our own store from scratch, and also how to extend Svelte's writable store to persist data to web storage.</li>
 <li>At the end we had a look at using the Svelte <code>transition</code> directive to implement animations on DOM elements.</li>
</ul>

<p>In the next article we will learn how add TypeScript support to our Svelte application. To take advantage of all its features, we will also port our entire application to TypeScript.</p>

<p>{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_reactivity_lifecycle_accessibility","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_TypeScript", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}</p>

<h2 id="In_this_module">In this module</h2>

<ul>
 <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Introduction">Introduction to client-side frameworks</a></li>
 <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Main_features">Framework main features</a></li>
 <li>React
  <ul>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started">Getting started with React</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_todo_list_beginning">Beginning our React todo list</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_components">Componentizing our React app</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_interactivity_events_state">React interactivity: Events and state</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_interactivity_filtering_conditional_rendering">React interactivity: Editing, filtering, conditional rendering</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_accessibility">Accessibility in React</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_resources">React resources</a></li>
  </ul>
 </li>
 <li>Ember
  <ul>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Ember_getting_started">Getting started with Ember</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Ember_structure_componentization">Ember app structure and componentization</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Ember_interactivity_events_state">Ember interactivity: Events, classes and state</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Ember_conditional_footer">Ember Interactivity: Footer functionality, conditional rendering</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Ember_routing">Routing in Ember</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Ember_resources">Ember resources and troubleshooting</a></li>
  </ul>
 </li>
 <li>Vue
  <ul>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_getting_started">Getting started with Vue</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_first_component">Creating our first Vue component</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_rendering_lists">Rendering a list of Vue components</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_methods_events_models">Adding a new todo form: Vue events, methods, and models</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_styling">Styling Vue components with CSS</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_computed_properties">Using Vue computed properties</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_conditional_rendering">Vue conditional rendering: editing existing todos</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_refs_focus_management">Focus management with Vue refs</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_resources">Vue resources</a></li>
  </ul>
 </li>
 <li>Svelte
  <ul>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_getting_started">Getting started with Svelte</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_Todo_list_beginning">Starting our Svelte Todo list app</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_variables_props">Dynamic behavior in Svelte: working with variables and props</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_components">Componentizing our Svelte app</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_reactivity_lifecycle_accessibility">Advanced Svelte: Reactivity, lifecycle, accessibility</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_stores">Working with Svelte stores</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_TypeScript">TypeScript support in Svelte</a></li>
   <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_deployment_next">Deployment and next steps</a></li>
  </ul>
 </li>
 <li>Angular
   <ul>
    <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_getting_started">Getting started with Angular</a></li>
    <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_todo_list_beginning">Beginning our Angular todo list app</a></li>
    <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_styling">Styling our Angular app</a></li>
    <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_item_component">Creating an item component</a></li>
    <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_filtering">Filtering our to-do items</a></li>
    <li><a href="/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_building">Building Angular applications and further resources</a></li>
   </ul>
 </li>
</ul>