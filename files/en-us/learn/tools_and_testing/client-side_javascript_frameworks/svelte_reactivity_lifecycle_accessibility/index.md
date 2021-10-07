---
title: 'Advanced Svelte: Reactivity, lifecycle, accessibility'
slug: >-
  Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_reactivity_lifecycle_accessibility
tags:
  - Accessibility
  - Beginner
  - Components
  - Frameworks
  - JavaScript
  - Learn
  - Lifecycle
  - Svelte
  - client-side
  - reactivity
---
<div>{{LearnSidebar}}<br>
{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_components","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_stores", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}</div>

<p>In the last article we added more features to our To-Do list and started to organize our app into components. In this article we will add the app's final features and further componentize our app. We will learn how to deal with reactivity issues related to updating objects and arrays. To avoid common pitfalls, we'll have to dig a little deeper into Svelte's reactivity system. We'll also look at solving some accessibility focus issues, and more besides.</p>

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
			<td>Learn some advanced Svelte techniques involving solving reactivity issues, keyboard accessibility problems to do with component lifecycle, and more.</td>
		</tr>
	</tbody>
</table>

<p>We'll focus on some accessibility issues involving focus management. To do so, we'll utilize some techniques for accessing DOM nodes and executing methods like <code><a href="/en-US/docs/Web/API/HTMLElement/focus">focus()</a></code> and <code><a href="/en-US/docs/Web/API/HTMLInputElement/select">select()</a></code>. We will also see how to declare and clean-up event listeners on DOM elements.</p>

<p>We also need to learn a bit about component lifecycle, to understand when these DOM nodes get mounted and unmounted from the DOM and how we can access them. We will also learn about the <code>action</code> directive, which will allow us to extend the functionality of HTML elements in a reusable and declarative way.</p>

<p>Finally, we will learn a bit more about components. So far, we've seen how components can share data using props, and communicate with their parents using events and two-way data binding. Now we will see how components can also expose methods and variables.</p>

<p>The following new components will be developed throughout the course of this article:</p>

<ul>
	<li><code>MoreActions</code>: Displays the <em>Check All</em> and <em>Remove Completed</em> buttons, and emits the corresponding events required to handle their functionality.</li>
	<li><code>NewTodo</code>: Displays the <code>&lt;input&gt;</code> field and <em>Add</em> button for adding a new todo.</li>
	<li><code>TodosStatus</code>: Displays the "x out of y items completed" status heading.</li>
</ul>

<h2 id="Code_along_with_us">Code along with us</h2>

<h3 id="Git">Git</h3>

<p>Clone the github repo (if you haven't already done it) with:</p>

<pre class="brush: bash">git clone https://github.com/opensas/mdn-svelte-tutorial.git</pre>

<p>Then to get to the current app state, run</p>

<pre class="brush: bash">cd mdn-svelte-tutorial/05-advanced-concepts</pre>

<p>Or directly download the folder's content:</p>

<pre class="brush: bash">npx degit opensas/mdn-svelte-tutorial/05-advanced-concepts</pre>

<p>Remember to run <code>npm install &amp;&amp; npm run dev</code> to start your app in development mode.</p>

<h3 id="REPL">REPL</h3>

<p>To code along with us using the REPL, start at</p>

<p><a href="https://svelte.dev/repl/76cc90c43a37452e8c7f70521f88b698?version=3.23.2">https://svelte.dev/repl/76cc90c43a37452e8c7f70521f88b698?version=3.23.2</a></p>

<h2 id="Working_on_the_MoreActions_component">Working on the MoreActions component</h2>

<p>Now we'll tackle the <em>Check All</em> and <em>Remove Completed</em> buttons. Let's create a component that will be in charge of displaying the buttons and emitting the corresponding events.</p>

<ol>
	<li>
	<p>Create a new file — <code>components/MoreActions.svelte</code>.</p>
	</li>
	<li>
	<p>When the first button is clicked, we'll emit a <code>checkAll</code> event to signal that all the todos should be checked/unchecked. When the second button is clicked, we'll emit a <code>removeCompleted</code> event to signal that all of the completed todos should be removed. Put the following content into your <code>MoreActions.svelte</code> file:</p>

	<pre class="brush: html">&lt;script&gt;
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  let completed = true

  const checkAll = () =&gt; {
    dispatch('checkAll', completed)
    completed = !completed
  }

  const removeCompleted = () =&gt; dispatch('removeCompleted')

&lt;/script&gt;

&lt;div class="btn-group"&gt;
  &lt;button type="button" class="btn btn__primary" on:click={checkAll}&gt;{completed ? 'Check' : 'Uncheck'} all&lt;/button&gt;
  &lt;button type="button" class="btn btn__primary" on:click={removeCompleted}&gt;Remove completed&lt;/button&gt;
&lt;/div&gt;</pre>

	<p>We've also included a <code>completed</code> variable to toggle between checking and unchecking all tasks.</p>
	</li>
	<li>
	<p>Back over in <code>Todos.svelte</code>, we are going to import our <code>MoreActions</code> component and create two functions to handle the events emitted by the <code>MoreActions</code> component.</p>

	<p>Add the following import statement below the existing ones:</p>

	<pre class="brush: js">import MoreActions from './MoreActions.svelte'</pre>
	</li>
	<li>
	<p>Then add the described functions at the end of the <code>&lt;script&gt;</code> section:</p>

	<pre class="brush: js">const checkAllTodos = (completed) =&gt; todos.forEach(t =&gt; t.completed = completed)

const removeCompletedTodos = () =&gt; todos = todos.filter(t =&gt; !t.completed)</pre>
	</li>
	<li>
	<p>Now go to the bottom of the <code>Todos.svelte</code> markup section and replace the <code>btn-group</code> <code>&lt;div&gt;</code> that we copied into <code>MoreActions.svelte</code> with a call to the <code>MoreActions</code> component, like so:</p>

	<pre class="brush: html">&lt;!-- MoreActions --&gt;
&lt;MoreActions
  on:checkAll={e =&gt; checkAllTodos(e.detail)}
  on:removeCompleted={removeCompletedTodos}
/&gt;</pre>
	</li>
	<li>
	<p>OK, let's go back into the app and try it out! You'll find that the <em>Remove Completed</em> button works fine, but the <em>Check All</em>/<em>Uncheck All</em> button just silently fails.</p>
	</li>
</ol>

<p>To find out what is happening here, we'll have to dig a little deeper into Svelte reactivity.</p>

<h2 id="Reactivity_gotchas_updating_objects_and_arrays">Reactivity gotchas: updating objects and arrays</h2>

<p>To see what's happening we can log the <code>todos</code> array from the <code>checkAllTodos()</code> function to the console.</p>

<ol>
	<li>
	<p>Update your existing <code>checkAllTodos()</code> function to the following:</p>

	<pre class="brush: js">const checkAllTodos = (completed) =&gt; {
  todos.forEach(t =&gt; t.completed = completed)
  console.log('todos', todos)
}</pre>
	</li>
	<li>
	<p>Go back to your browser, open your DevTools console, and click <em>Check All</em>/<em>Uncheck All</em> a few times.</p>
	</li>
</ol>

<p>You'll notice that the array is successfully updated every time you press the button (the <code>todo</code> objects' <code>completed</code> properties are toggled between <code>true</code> and <code>false</code>), but Svelte is not aware of that. This also means that in this case, a reactive statement like <code>$: console.log('todos', todos)</code> won't be very useful.</p>

<p>To find out why this is happening, we need to understand how reactivity works in Svelte when updating arrays and objects.</p>

<p>Many web frameworks use the virtual DOM technique to update the page. Basically, the virtual DOM is an in-memory copy of the contents of the web page. The framework updates this virtual representation which is then synced with the "real" DOM. This is much faster than directly updating the DOM and allows the framework to apply many optimization techniques.</p>

<p>These frameworks, by default, basically re-run all our JavaScript on every change against this virtual DOM, and apply different methods to cache expensive calculations and optimize execution. They make little to no attempt to understand what our JavaScript code is doing.</p>

<p>Svelte doesn't use a virtual DOM representation. Instead, it parses and analyzes our code, creates a dependency tree, and then generates the required JavaScript to update only the parts of the DOM that need to be updated. This approach usually generates optimal JavaScript code with minimal overhead, but it also has its limitations.</p>

<p>Sometimes Svelte cannot detect changes to variables being watched. Remember that to tell Svelte that a variable has changed, you have to assign it a new value. A simple rule of thumb is that <strong>The name of the updated variable must appear on the left hand side of the assignment.</strong></p>

<p>For example, in the following piece of code:</p>

<pre class="brush: js">const foo = obj.foo
foo.bar = 'baz'</pre>

<p>Svelte won't update references to <code>obj.foo.bar</code>, unless you follow it up with <code>obj = obj</code>. That's because Svelte can't track object references, so we have to explicitly tell it that <code>obj</code> has changed by issuing an assignment.</p>

<div class="notecard note">
<p><strong>Note:</strong> if <code>foo</code> is a top level variable, you can easily tell Svelte to update <code>obj</code> whenever <code>foo</code> is changed with the following reactive statement: <code>$: foo, obj = obj</code>. With this we are defining <code>foo</code> as a dependency, and whenever it changes Svelte will run <code>obj = obj</code>.</p>
</div>

<p>In our <code>checkAllTodos()</code> function, when we run:</p>

<pre class="brush: js">todos.forEach(t =&gt; t.completed = completed)</pre>

<p>Svelte will not mark <code>todos</code> as changed because it does not know that when we update our <code>t</code> variable inside the <code>forEach()</code> method, we are also modifying the <code>todos</code> array. And that makes sense, because otherwise Svelte would be aware of the inner workings of the <code>forEach()</code> method; the same would therefore be true for any method attached to any object or array.</p>

<p>Nevertheless, there are different techniques that we can apply to solve this problem, and all of them involve assigning a new value to the variable being watched.</p>

<p>Like we already saw, we could just tell Svelte to update the variable with a self-assignment, like this:</p>

<pre class="brush: js">const checkAllTodos = (completed) =&gt; {
  todos.forEach(t =&gt; t.completed = completed)
  todos = todos
}</pre>

<p>This will solve the problem. Internally Svelte will flag <code>todos</code> as changed and remove the apparently redundant self-assignment. Apart from the fact that it looks weird, it's perfectly ok to use this technique, and sometimes it's the most concise way to do it.</p>

<p>We could also access the <code>todos</code> array by index, like this:</p>

<pre class="brush: js">const checkAllTodos = (completed) =&gt; {
  todos.forEach( (t,i) =&gt; todos[i].completed = completed)
}</pre>

<p>Assignments to properties of arrays and objects — e.g. <code>obj.foo += 1</code> or <code>array[i] = x</code> — work the same way as assignments to the values themselves. When Svelte analyzes this code, it can detect that the <code>todos</code> array is being modified.</p>

<p>Another solution is to assign a new array to <code>todos</code> containing a copy of all the todos with the <code>completed</code> property updated accordingly, like this:</p>

<pre class="brush: js">const checkAllTodos = (completed) =&gt; {
  todos = todos.map(t =&gt; {                  // shorter version: todos = todos.map(t =&gt; ({...t, completed}))
    return {...t, completed: completed}
  })
}</pre>

<p>In this case we are using the <code><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map">map()</a></code> method, which returns a new array with the results of executing the provided function for each item. The function returns a copy of each todo using <a href="/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax">spread syntax</a> and overwrites the property of the completed value accordingly. This solution has the added benefit of returning a new array with new objects, completely avoiding mutating the original <code>todos</code> array.</p>

<div class="notecard note">
<p><strong>Note:</strong> Svelte allows us to specify different options that affect how the compiler works. The <code>&lt;svelte:options immutable={true}/&gt;</code> option tells the compiler that you promise not to mutate any objects. This allows it to be less conservative about checking whether values have changed and generate simpler and more performant code. For more information on <code>&lt;svelte:options...&gt;</code>, check the <a href="https://svelte.dev/docs#svelte_options">Svelte options documentation</a>.</p>
</div>

<p>All of these solutions involve an assignment in which the updated variable is on the left side of the equation. Any of this techniques will allow Svelte to notice that our <code>todos</code> array has been modified.</p>

<p><strong>Choose one, and update your <code>checkAllTodos()</code> function as required. Now you should be able to check and uncheck all your todos at once. Try it!</strong></p>

<h2 id="Finishing_our_MoreActions_component">Finishing our MoreActions component</h2>

<p>We will add one usability detail to our component. We'll disable the buttons when there are no tasks to be processed. To create this we'll receive the <code>todos</code> array as a prop, and set the <code>disabled</code> property of each button accordingly.</p>

<ol>
	<li>
	<p>Update your <code>MoreActions.svelte</code> component like this:</p>

	<pre class="brush: html">&lt;script&gt;
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  export let todos

  let completed = true

  const checkAll = () =&gt; {
    dispatch('checkAll', completed)
    completed = !completed
  }

  const removeCompleted = () =&gt; dispatch('removeCompleted')

  $: completedTodos = todos.filter(t =&gt; t.completed).length
&lt;/script&gt;

&lt;div class="btn-group"&gt;
  &lt;button type="button" class="btn btn__primary"
    disabled={todos.length === 0} on:click={checkAll}&gt;{completed ? 'Check' : 'Uncheck'} all&lt;/button&gt;
  &lt;button type="button" class="btn btn__primary"
    disabled={completedTodos === 0} on:click={removeCompleted}&gt;Remove completed&lt;/button&gt;
&lt;/div&gt;</pre>

	<p>We've also declared a reactive <code>completedTodos</code> variable to enable or disable the <em>Remove Completed</em> button.</p>
	</li>
	<li>
	<p>Don't forget to pass the prop into <code>MoreActions</code> from inside <code>Todos.svelte</code>, where the component is called:</p>

	<pre class="brush: js">&lt;MoreActions {todos}
    on:checkAll={e =&gt; checkAllTodos(e.detail)}
    on:removeCompleted={removeCompletedTodos}
  /&gt;</pre>
	</li>
</ol>

<h2 id="Working_with_the_DOM_focusing_on_the_details">Working with the DOM: focusing on the details</h2>

<p>Now that we have completed all of the app's required functionality, we'll concentrate on some accessibility features that will improve the usability of our app for both keyboard-only and screenreader users.</p>

<p>In its current state our app has a couple of keyboard accessibility problems involving focus management. Let's have a look at these issues.</p>

<h2 id="Exploring_keyboard_accessibility_issues_in_our_todo_app">Exploring keyboard accessibility issues in our todo app</h2>

<p>Right now, keyboard users will find out that the focus flow of our app is not very predictable or coherent.</p>

<p>If you click on the input at the top of our app, you'll see a thick, dashed outline around that input. This outline is your visual indicator that the browser is currently focused on this element.</p>

<p>If you are a mouse user, you might have skipped this visual hint. But if you are working exclusively with the keyboard, knowing which control has focus is of vital importance. It tells us which control is going to receive our keystrokes.</p>

<p>If you press the <kbd>Tab</kbd> key repeatedly, you'll see the dashed focus indicator cycling between all the focusable elements on the page. If you move the focus to the <em>Edit</em> button and press <kbd>Enter</kbd>, suddenly the focus disappears, you can no longer tell which control will receive our keystrokes.</p>

<p>Moreover, if you press the <kbd>Escape</kbd> or <kbd>Enter</kbd> key, nothing happens. And if you click on <em>Cancel</em> or <em>Save</em>, the focus disappears again. For a user working with the keyboard, this behavior will be confusing at best.</p>

<p>We'd also like to add some usability features, like disabling the <em>Save</em> button when required fields are empty, giving focus to certain HTML elements or auto-selecting contents when a text input receives focus.</p>

<p>To implement all these features we'll need programmatic access to DOM nodes to run functions like <code><a href="/en-US/docs/Web/API/HTMLElement/focus">focus()</a></code> and <code><a href="/en-US/docs/Web/API/HTMLInputElement/select">select()</a></code>. We will also have to use <code><a href="/en-US/docs/Web/API/EventTarget/addEventListener">addEventListener()</a></code> and <code><a href="/en-US/docs/Web/API/EventTarget/removeEventListener">removeEventListener()</a></code> to run specific tasks when the control receives focus.</p>

<p>The problem is that all these DOM nodes are dynamically created by Svelte at runtime. So we'll have to wait for them to be created and added to the DOM in order to use them. To do so, we'll have to learn about the <a href="https://svelte.dev/tutorial/onmount">component lifecycle</a> to understand when we can access them — more on this later.</p>

<h2 id="Creating_a_NewTodo_component">Creating a NewTodo component</h2>

<p>Let's begin by extracting our new todo form out to its own component. With what we know so far we can create a new component file and adjust the code to emit an <code>addTodo</code> event, passing the name of the new todo in with the additional details.</p>

<ol>
	<li>
	<p>Create a new file — <code>components/NewTodo.svelte</code>.</p>
	</li>
	<li>
	<p>Put the following contents inside it:</p>

	<pre class="brush: js">&lt;script&gt;
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  let name = ''

  const addTodo = () =&gt; {
    dispatch('addTodo', name)
    name = ''
  }

  const onCancel = () =&gt; name = ''

&lt;/script&gt;

&lt;form on:submit|preventDefault={addTodo} on:keydown={e =&gt; e.key === 'Escape' &amp;&amp; onCancel()}&gt;
  &lt;h2 class="label-wrapper"&gt;
    &lt;label for="todo-0" class="label__lg"&gt;What needs to be done?&lt;/label&gt;
  &lt;/h2&gt;
  &lt;input bind:value={name} type="text" id="todo-0" autoComplete="off" class="input input__lg" /&gt;
  &lt;button type="submit" disabled={!name} class="btn btn__primary btn__lg"&gt;Add&lt;/button&gt;
&lt;/form&gt;</pre>

	<p>Here we are binding the <code>&lt;input&gt;</code> to the <code>name</code> variable with <code>bind:value={name}</code> and disabling the <em>Add</em> button when it is empty (i.e. no text content) using <code>disabled={!name}</code>. We are also taking care of the <kbd>Escape</kbd> key with <code>on:keydown={e =&gt; e.key === 'Escape' &amp;&amp; onCancel()}</code>. Whenever the <kbd>Escape</kbd> key is pressed we run <code>onCancel()</code>, which just clears up the <code>name</code> variable.</p>
	</li>
	<li>
	<p>Now we have to <code>import</code> and use it from inside the <code>Todos</code> component, and update the <code>addTodo()</code> function to receive the name of the new todo.</p>

	<p>Add the following <code>import</code> statement below the others inside <code>Todos.svelte</code>:</p>

	<pre class="brush: js">import NewTodo from './NewTodo.svelte'</pre>
	</li>
	<li>
	<p>And update the <code>addTodo()</code> function like so:</p>

	<pre class="brush: js">function addTodo(name) {
  todos = [...todos, { id: newTodoId, name, completed: false }]
}</pre>

	<p><code>addTodo()</code> now receives the name of the new todo directly, so we no longer need the <code>newTodoName</code> variable to give it its value. Our <code>NewTodo</code> component takes care of that.</p>

	<div class="notecard note">
	<p><strong>Note:</strong> the <code>{ name }</code> syntax is just a shorthand for <code>{ name: name }</code>. This one comes from JavaScript itself and has nothing to do with Svelte, besides providing some inspiration for Svelte's own shorthands.</p>
	</div>
	</li>
	<li>
	<p>Finally for this section, replace the NewTodo form markup with a call to <code>NewTodo</code> component, like so:</p>

	<pre class="brush: html">&lt;!-- NewTodo --&gt;
&lt;NewTodo on:addTodo={e =&gt; addTodo(e.detail)} /&gt;</pre>
	</li>
</ol>

<h2 id="Working_with_DOM_nodes_using_the_bindthisdom_node_directive">Working with DOM nodes using the <code>bind:this={dom_node}</code> directive</h2>

<p>Now we want the <code>NewTodo</code> <code>&lt;input&gt;</code> to re-gain focus every time the <em>Add</em> button is pressed. For that we'll need a reference to the DOM node of the input. Svelte provides a way to do this with the <code>bind:this={dom_node}</code> directive. When specified, as soon as the component is mounted and the DOM node is created Svelte assigns a reference to the DOM node to the specified variable.</p>

<p>We'll create a <code>nameEl</code> variable and bind it to the input it using <code>bind:this={nameEl}</code>. Then inside <code>addTodo()</code>, after adding the new todo we will call <code>nameEl.focus()</code> to refocus the <code>&lt;input&gt;</code> again. We will do the same when the user presses the <kbd>Escape</kbd> key, with the <code>onCancel()</code> function.</p>

<p>Update the contents of <code>NewTodo.svelte</code> like so:</p>

<pre class="brush: js">&lt;script&gt;
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  let name = ''
  let nameEl                  // reference to the name input DOM node

  const addTodo = () =&gt; {
    dispatch('addTodo', name)
    name = ''
    nameEl.focus()            // give focus to the name input
  }

  const onCancel = () =&gt; {
    name = ''
    nameEl.focus()            // give focus to the name input
  }

&lt;/script&gt;

&lt;form on:submit|preventDefault={addTodo} on:keydown={e =&gt; e.key === 'Escape' &amp;&amp; onCancel()}&gt;
  &lt;h2 class="label-wrapper"&gt;
    &lt;label for="todo-0" class="label__lg"&gt;What needs to be done?&lt;/label&gt;
  &lt;/h2&gt;
  &lt;input bind:value={name} bind:this={nameEl} type="text" id="todo-0" autoComplete="off" class="input input__lg" /&gt;
  &lt;button type="submit" disabled={!name} class="btn btn__primary btn__lg"&gt;Add&lt;/button&gt;
&lt;/form&gt;</pre>

<p>Try the app out — type a new todo name in to the <code>&lt;input&gt;</code> field, press <kbd>tab</kbd> to give focus to the <em>Add</em> button, and then hit <kbd>Enter</kbd> or <kbd>Escape</kbd> to see how the input recovers focus.</p>

<h3 id="Autofocusing_our_input">Autofocusing our input</h3>

<p>The next feature will add to our <code>NewTodo</code> component will be an <code>autofocus</code> prop, which will allow us to specify that we want the <code>&lt;input&gt;</code> field to be focused on page load.</p>

<ol>
	<li>
	<p>Our first attempt is as follows — let's try adding the <code>autofocus</code> prop and just call <code>nameEl.focus()</code> from the <code>&lt;script&gt;</code> block. Update the first part of the <code>NewTodo.svelte</code> <code>&lt;script&gt;</code> section (the first four lines) to look like this:</p>

	<pre class="brush: js">&lt;script&gt;
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  export let autofocus = false

  let name = ''
  let nameEl                  // reference to the name input DOM node

  if (autofocus) nameEl.focus()
</pre>
	</li>
	<li>
	<p>Now go back to the <code>Todos</code> component, and pass the <code>autofocus</code> prop into the <code>&lt;NewTodo&gt;</code> component call, like so:</p>

	<pre class="brush: html">&lt;!-- NewTodo --&gt;
&lt;NewTodo autofocus on:addTodo={e =&gt; addTodo(e.detail)} /&gt;</pre>
	</li>
	<li>
	<p>If you try your app out now, you'll see that the page is now blank, and in your DevTools web console you'll see an error along the lines of: <code>TypeError: nameEl is undefined</code>.</p>
	</li>
</ol>

<p>To understand what's happening here, let's talk some more about that <a href="https://svelte.dev/tutorial/onmount">component lifecycle</a> we mentioned earlier.</p>

<h2 id="Component_lifecycle_and_the_onMount_function">Component lifecycle, and the <code>onMount()</code> function</h2>

<p>When a component is instantiated, Svelte runs the initialization code (that is, the <code>&lt;script&gt;</code> section of the component). But at that moment, all the nodes that comprise the component are not attached to the DOM, in fact, they don't even exist.</p>

<p>So, how can you know when the component has already been created and mounted on the DOM? The answer is that every component has a lifecycle that starts when it is created, and ends when it is destroyed. There are a handful of functions that allow you to run code at key moments during that lifecycle.</p>

<p>The one you'll use most frequently is <code>onMount()</code>, which lets us run a callback as soon as the component has been mounted on the DOM. Let's give it a try and see what happens to the <code>nameEl</code> variable.</p>

<ol>
	<li>
	<p>To start with, add the following line at the beginning of the <code>NewTodo.svelte</code> <code>&lt;script&gt;</code> section:</p>

	<pre class="brush: js"> import { onMount } from 'svelte'</pre>
	</li>
	<li>
	<p>And these lines at the end of it:</p>

	<pre class="brush: js">console.log('initializing:', nameEl)
onMount( () =&gt; {
  console.log('mounted:', nameEl)
})</pre>
	</li>
	<li>
	<p>Now remove the <code>if (autofocus) nameEl.focus()</code> line to avoid throwing the error we were seeing before.</p>
	</li>
	<li>
	<p>The app will now work again, and you'll see the following in your console:</p>

	<pre>initializing: undefined
mounted: &lt;input id="todo-0" class="input input__lg" type="text" autocomplete="off"&gt;</pre>

	<p>As you can see, while the component is initializing <code>nameEl</code> is undefined, which makes sense because the node input doesn't even exist yet. After the component has been mounted, Svelte assigned a reference to the <code>&lt;input&gt;</code> DOM node to the <code>nameEl</code> variable, thanks to the <code>bind:this={nameEl} directive</code>.</p>
	</li>
	<li>
	<p>To get the autofocus functionality working, replace the previous <code>console.log()</code>/<code>onMount()</code> block you added with this:</p>

	<pre class="brush: js">onMount(() =&gt; autofocus &amp;&amp; nameEl.focus())    // if autofocus is true, we run nameEl.focus()</pre>
	</li>
	<li>
	<p>Go to your app again, and you'll now see the <code>&lt;input&gt;</code> field is focused on page load.</p>
	</li>
</ol>

<div class="notecard note">
<p><strong>Note:</strong> You can have a look at the other <a href="https://svelte.dev/docs#svelte">lifecycle functions in the Svelte docs</a>, and you can see them in action in the <a href="https://svelte.dev/tutorial/onmount">interactive tutorial</a>.</p>
</div>

<h2 id="Waiting_for_the_DOM_to_be_updated_with_the_tick_function">Waiting for the DOM to be updated with the <code>tick()</code> function</h2>

<p>Now we will take care of the <code>Todo</code> component's focus management details. First of all, we want a <code>Todo</code> component's edit <code>&lt;input&gt;</code> to receive focus when we enter editing mode by pressing its <em>Edit</em> button. In the same fashion as we saw earlier, we'll create a <code>nameEl</code> variable inside <code>Todo.svelte</code> and call <code>nameEl.focus()</code> after setting the <code>editing</code> variable to <code>true</code>.</p>

<ol>
	<li>
	<p>Open the file <code>components/Todo.svelte</code> and add a <code>nameEl</code> variable declaration, just below your editing and name declarations:</p>

	<pre class="brush: js">let nameEl                              // reference to the name input DOM node</pre>
	</li>
	<li>
	<p>Now update your <code>onEdit()</code> function like so:</p>

	<pre class="brush: js">function onEdit() {
  editing = true                        // enter editing mode
  nameEl.focus()                        // set focus to name input
}</pre>
	</li>
	<li>
	<p>And finally, bind <code>nameEl</code> to the <code>&lt;input&gt;</code> field, by updating it like so:</p>

	<pre class="brush: html">&lt;input bind:value={name} bind:this={nameEl} type="text" id="todo-{todo.id}" autoComplete="off" class="todo-text" /&gt;</pre>
	</li>
	<li>
	<p>However, when you try the updated app you'll get an error along the lines of "TypeError: nameEl is undefined" in the console when you press a todo's <em>Edit</em> button.</p>
	</li>
</ol>

<p>So, what is happening here? When you update a component's state in Svelte, it doesn't update the DOM immediately. Instead, it waits until the next microtask to see if there are any other changes that need to be applied, including in other components. Doing so avoids unnecessary work and allows the browser to batch things more effectively.</p>

<p>In this case, when <code>editing</code> is <code>false</code>, the edit <code>&lt;input&gt;</code> is not visible because it does not exist in the DOM. Inside the <code>onEdit()</code> function we set <code>editing = true</code> and immediately afterwards try to access the <code>nameEl</code> variable and execute <code>nameEl.focus()</code>. The problem here is that Svelte hasn't yet updated the DOM.</p>

<p>One way to solve this problem is to use <code><a href="/en-US/docs/Web/API/setTimeout">setTimeout()</a></code> to delay the call to <code>nameEl.focus()</code> until the next event cycle, and give Svelte the opportunity to update the DOM.</p>

<p>Try this now:</p>

<pre class="brush: js">function onEdit() {
  editing = true                        // enter editing mode
  setTimeout(() =&gt; nameEl.focus(), 0)   // asynchronous call to set focus to name input
}</pre>

<p>The above solution works, but it is rather inelegant. Svelte provides a better way to handle these cases. The <a href="https://svelte.dev/tutorial/tick"><code>tick()</code> function</a> returns a promise that resolves as soon as any pending state changes have been applied to the DOM (or immediately, if there are no pending state changes). Let's try it now.</p>

<ol>
	<li>
	<p>First of all, import <code>tick</code> at the top of the <code>&lt;script&gt;</code> section alongside your existing import:</p>

	<pre class="brush: js">import { tick } from 'svelte'</pre>
	</li>
	<li>
	<p>Next, call <code>tick()</code> with <code><a href="/en-US/docs/Web/JavaScript/Reference/Operators/await">await</a></code> from an <a href="/en-US/docs/Web/JavaScript/Reference/Statements/async_function">async function</a>; update <code>onEdit()</code> like so:</p>

	<pre class="brush: js">async function onEdit() {
  editing = true                        // enter editing mode
  await tick()
  nameEl.focus()
}</pre>
	</li>
	<li>
	<p>If you try it now you'll see that everything works as expected.</p>
	</li>
</ol>

<div class="notecard note">
<p><strong>Note:</strong> To see another example using <code>tick()</code>, visit the <a href="https://svelte.dev/tutorial/tick">Svelte tutorial</a>.</p>
</div>

<h2 id="Adding_functionality_to_HTML_elements_with_the_useaction_directive">Adding functionality to HTML elements with the <code>use:action</code> directive</h2>

<p>Next up, we want the name <code>&lt;input&gt;</code> to automatically select all text on focus. Moreover, we want to develop this in such a way that it could be easily reused on any HTML <code>&lt;input&gt;</code> and applied in a declarative way. We will use this requirement as an excuse to show a very powerful feature that Svelte provides us to add functionality to regular HTML elements: <a href="https://svelte.dev/docs#use_action">actions</a>.</p>

<p>To select the text of a DOM input node we have to call <code><a href="/en-US/docs/Web/API/HTMLInputElement/select">select()</a></code>. To get this function called whenever the node gets focused, we need an event listener along these lines:</p>

<pre class="brush: js">node.addEventListener('focus', event =&gt; node.select()).</pre>

<p>And, in order to avoid memory leaks, we should also call the <code><a href="/en-US/docs/Web/API/EventTarget/removeEventListener">removeEventListener() </a></code>function when the node is destroyed.</p>

<div class="notecard note">
<p><strong>Note:</strong> All this is just standard WebAPI functionality; nothing here is specific to Svelte.</p>
</div>

<p>We could achieve all this in our <code>Todo</code> component whenever we add or remove the <code>&lt;input&gt;</code> from the DOM, but we would have to be very careful to add the event listener after the node has been added to the DOM, and remove the listener before the node is removed from the DOM. In addition, our solution would not be very reusable.</p>

<p>That's where Svelte actions come into play. Basically they let us run a function whenever an element has been added to the DOM, and after removal from the DOM.</p>

<p>In our immediate use case, we will define a function called <code>selectOnFocus()</code> that will receive a node as parameter. The function will add an event listener to that node, so that whenever it gets focused it will select the text. Then it will return an object with a <code>destroy</code> property. The <code>destroy</code> property is what Svelte will execute after removing the node from the DOM. Here we will remove the listener to make sure we don't leave any memory leak behind.</p>

<ol>
	<li>
	<p>Let's create the function <code>selectOnFocus()</code>. Add the following to the bottom of the <code>Todo.svelte</code> <code>&lt;script&gt;</code> section:</p>

	<pre class="brush: js">function selectOnFocus(node) {
  if (node &amp;&amp; typeof node.select === 'function' ) {               // make sure node is defined and has a select() method
    const onFocus = event =&gt; node.select()                        // event handler
    node.addEventListener('focus', onFocus)                       // when node gets focus call onFocus()
    return {
      destroy: () =&gt; node.removeEventListener('focus', onFocus)   // this will be executed when the node is removed from the DOM
    }
  }
}</pre>
	</li>
	<li>
	<p>Now we need to tell the <code>&lt;input&gt;</code> to use that function with the <code><a href="https://svelte.dev/docs#use_action">use:action</a></code> directive:</p>

	<pre class="brush: html">&lt;input use:selectOnFocus /&gt;</pre>

	<p>With this directive we are telling Svelte to run this function, passing the DOM node of the <code>&lt;input&gt;</code> as a parameter, as soon as the component is mounted on the DOM. It will also be in charge of executing the <code>destroy</code> function when the component is removed from DOM. So, with the <code>use</code> directive, Svelte takes care of the component's lifecycle for us.</p>

	<p>In our case, our <code>&lt;input&gt;</code> would end up like so — update the component's first label/input pair (inside the edit template) like so:</p>

	<pre class="brush: html">&lt;label for="todo-{todo.id}" class="todo-label"&gt;New name for '{todo.name}'&lt;/label&gt;
&lt;input bind:value={name} bind:this={nameEl} use:selectOnFocus type="text" id="todo-{todo.id}" autoComplete="off" class="todo-text"
/&gt;</pre>
	</li>
	<li>
	<p>Let's try it out. Go to your app, press a todo's <em>Edit</em> button, then <kbd>Tab</kbd> to take focus away from the <code>&lt;input&gt;</code>. Now click on the <code>&lt;input&gt;</code> — you'll see that the entire input text is selected.</p>
	</li>
</ol>

<h3 id="Making_the_action_reusable">Making the action reusable</h3>

<p>Now let's make this function truly reusable across components. <code>selectOnFocus()</code> is just a function without any dependency on the <code>Todo.svelte</code> component, so we can just extract it to a file and use it from there.</p>

<ol>
	<li>
	<p>Create a new file, <code>actions.js</code>, inside the <code>src</code> folder.</p>
	</li>
	<li>
	<p>Give it the following content:</p>

	<pre class="brush: js">export function selectOnFocus(node) {
  if (node &amp;&amp; typeof node.select === 'function' ) {               // make sure node is defined and has a select() method
    const onFocus = event =&gt; node.select()                        // event handler
    node.addEventListener('focus', onFocus)                       // when node gets focus call onFocus()
    return {
      destroy: () =&gt; node.removeEventListener('focus', onFocus)   // this will be executed when the node is removed from the DOM
    }
  }
}</pre>
	</li>
	<li>
	<p>Now import it from inside <code>Todo.svelte</code>; add the following import statement just below the others:</p>

	<pre class="brush: js">import { selectOnFocus } from '../actions.js'</pre>
	</li>
	<li>
	<p>And remove the <code>selectOnFocus()</code> definition from <code>Todo.svelte</code> — we no longer need it there.</p>
	</li>
</ol>

<h3 id="Reusing_our_action">Reusing our action</h3>

<p>To demonstrate our action's reusability, let's make use of it in <code>NewTodo.svelte</code>.</p>

<ol>
	<li>
	<p>Import <code>selectOnFocus()</code> from <code>actions.js</code> in this file too, as before:</p>

	<pre class="brush: js">import { selectOnFocus } from '../actions.js'</pre>
	</li>
	<li>
	<p>Add the <code>use:selectOnFocus</code> directive to the <code>&lt;input&gt;</code>, like this:</p>

	<pre class="brush: html">&lt;input bind:value={name} bind:this={nameEl} use:selectOnFocus
  type="text" id="todo-0" autoComplete="off" class="input input__lg"
/&gt;</pre>
	</li>
</ol>

<p>With a few lines of code we can add functionality to regular HTML elements, in a very reusable and declarative way. It just takes an <code>import</code> and a short directive like <code>use:selectOnFocus</code> that clearly depicts its purpose. And we can achieve this without the need to create a custom wrapper element like <code>TextInput</code>, <code>MyInput</code> or similar. Moreover, you can add as many <code>use:action</code> directives as you want to an element.</p>

<p>Also, we didn't have to struggle with <code>onMount()</code>, <code>onDestroy()</code> or <code>tick()</code> — the <code>use</code> directive takes care of the component lifecycle for us.</p>

<h3 id="Other_actions_improvements">Other actions improvements</h3>

<p>In the previous section, while working with the <code>Todo</code> components, we had to deal with <code>bind:this</code>, <code>tick()</code>, and <code>async</code> functions just to give focus to our <code>&lt;input&gt;</code> as soon as it was added to the DOM.</p>

<ol>
	<li>
	<p>This is how we can implement it with actions instead:</p>

	<pre class="brush: js">const focusOnInit = (node) =&gt; node &amp;&amp; typeof node.focus === 'function' &amp;&amp; node.focus()</pre>
	</li>
	<li>
	<p>And then in our markup we just need to add another <code>use:</code> directive:</p>

	<pre class="brush: html">&lt;input bind:value={name} use:selectOnFocus use:focusOnInit ...</pre>
	</li>
	<li>
	<p>Our <code>onEdit()</code> function can now be much simpler:</p>

	<pre class="brush: js">function onEdit() {
  editing = true                        // enter editing mode
}</pre>
	</li>
</ol>

<p>As a last example before we move on, let's go back to our <code>Todo.svelte</code> component and give focus to the <em>Edit</em> button after the user presses <em>Save</em> or <em>Cancel</em>.</p>

<p>We could try just reusing our <code>focusOnInit</code> action again, adding <code>use:focusOnInit</code> to the <em>Edit</em> button. But we'd be introducing a subtle bug. When you add a new todo, the focus will be put on the <em>Edit</em> button of the recently added todo. That's because the <code>focusOnInit</code> action is running when the component is created.</p>

<p>That's not what we want — we want the <em>Edit</em> button to receive focus only when the user has pressed <em>Save</em> or <em>Cancel</em>.</p>

<ol>
	<li>
	<p>So, go back to your <code>Todo.svelte</code> file.</p>
	</li>
	<li>
	<p>First of all we'll create a flag named <code>editButtonPressed</code> and initialize it to <code>false</code>. Add this just below your other variable definitions:</p>

	<pre class="brush: js">let editButtonPressed = false           // track if edit button has been pressed, to give focus to it after cancel or save</pre>
	</li>
	<li>
	<p>Next, we'll modify the <em>Edit</em> button's functionality to save this flag, and create the action for it. Update the <code>onEdit()</code> function like so:</p>

	<pre class="brush: js">function onEdit() {
  editButtonPressed = true              // user pressed the Edit button, focus will come back to the Edit button
  editing = true                        // enter editing mode
}</pre>
	</li>
	<li>
	<p>Below it, add the following definition for <code>focusEditButton()</code>:</p>

	<pre class="brush: js">const focusEditButton = (node) =&gt; editButtonPressed &amp;&amp; node.focus()</pre>
	</li>
	<li>
	<p>Finally, we <code>use</code> the <code>focusEditButton</code> action on the <em>Edit</em> button, like so:</p>

	<pre class="brush: html">&lt;button type="button" class="btn" on:click={onEdit} use:focusEditButton&gt;
  Edit&lt;span class="visually-hidden"&gt; {todo.name}&lt;/span&gt;
&lt;/button&gt;</pre>
	</li>
	<li>
	<p>Go back and try your app again. At this point, every time the <em>Edit</em> button is added to the DOM, the <code>focusEditButton</code> action is executed, but it will only give focus to the button if the <code>editButtonPressed</code> flag is <code>true</code>.</p>
	</li>
</ol>

<div class="notecard note">
<p><strong>Note:</strong> We have barely scratched the surface of actions here. Actions can also have reactive parameters, and Svelte lets us detect when any of those parameters change. So we can add functionality that integrates nicely with the Svelte reactive system. Have a look at the relevant Svelte School article for a more <a href="https://svelte.school/tutorials/introduction-to-actions">detailed introduction to actions</a>. Actions are also very useful for seamlessly <a href="https://svelte.school/tutorials/external-libraries-in-svelte-and-sapper-using-actions">integrating with third party libraries</a>.</p>
</div>

<h2 id="Component_binding_exposing_component_methods_and_variables_using_the_bindthiscomponent_directive">Component binding: exposing component methods and variables using the <code>bind:this={component}</code> directive</h2>

<p>There's still one accessibility annoyance left. When the user presses the <em>Delete</em> button, the focus vanishes.</p>

<p>So, the last feature we will be looking at in this article involves setting the focus on the status heading after a todo has been deleted.</p>

<p>Why the status heading? In this case, the element that had the focus has been deleted, so there's not a clear candidate to receive focus. We've picked the status heading because it's near the list of todos, and it's a way to give a visual feedback about the removal of the task, as well as indicating what's happened to screenreader users.</p>

<p>First we'll extract the status heading to its own component.</p>

<ol>
	<li>
	<p>Create a new file — <code>components/TodosStatus.svelte</code>.</p>
	</li>
	<li>
	<p>Add the following contents to it:</p>

	<pre class="brush: html">&lt;script&gt;
  export let todos

  $: totalTodos = todos.length
  $: completedTodos = todos.filter(todo =&gt; todo.completed).length
&lt;/script&gt;

&lt;h2 id="list-heading"&gt;{completedTodos} out of {totalTodos} items completed&lt;/h2&gt;</pre>
	</li>
	<li>
	<p>Import the file at the beginning of <code>Todos.svelte</code>, adding the following <code>import</code> statement below the others:</p>

	<pre class="brush: js">import TodosStatus from './TodosStatus.svelte'</pre>
	</li>
	<li>
	<p>Replace the <code>&lt;h2&gt;</code> status heading inside <code>Todos.svelte</code> with a call to the <code>TodosStatus</code> component, passing <code>todos</code> to it as a prop, like so:</p>

	<pre class="brush: html">&lt;TodosStatus {todos} /&gt;</pre>
	</li>
	<li>
	<p>You can also do a bit of clean-up, removing the <code>totalTodos</code> and <code>completedTodos</code> variables from <code>Todos.svelte</code>. Just remove the <code>$: totalTodos = ...</code> and the <code>$: completedTodos = ...</code> lines, and also remove the reference to <code>totalTodos</code> when we calculate <code>newTodoId</code> and use <code>todos.length</code>, instead. To do this, replace the block that begins with <code>let newTodoId</code> with this:</p>

	<pre class="brush: js">$: newTodoId = todos.length ? Math.max(...todos.map(t =&gt; t.id)) + 1 : 1</pre>
	</li>
	<li>
	<p>Everything works as expected — we just extracted the last piece of markup to its own component.</p>
	</li>
</ol>

<p>Now we need to find a way to give focus to the <code>&lt;h2&gt;</code> status label after a todo has been removed.</p>

<p>So far we saw how to send information to a component via props, and how a component can communicate with its parent by emitting events or using two-way data binding. The child component could get a reference to the <code>&lt;h2&gt;</code> node <code>using bind:this={dom_node}</code> and expose it to the outside using two-way data binding. But doing so would break the component encapsulation; setting focus on it should be its own responsibility.</p>

<p>So we need the <code>TodosStatus</code> component to expose a method that its parent can call to give focus to it. It's a very common scenario that a component needs to expose some behavior or information to the consumer; let's see how to achieve it with Svelte.</p>

<p>We've already seen that Svelte uses <code>export let var = ...</code> to <a href="https://svelte.dev/docs#1_export_creates_a_component_prop">declare props</a>. But if instead of using <code>let</code> you export a <code>const</code>, <code>class</code> or <code>function</code>, it is read-only outside the component. Function expressions are valid props, however. In the following example, the first three declarations are props, and the rest are exported values:</p>

<pre class="brush: js">&lt;script&gt;
  export let bar = 'optional default initial value'       // prop
  export let baz = undefined                              // prop
  export let format = n =&gt; n.toFixed(2)                   // prop

  // these are readonly
  export const thisIs = 'readonly'                        // read-only export

  export function greet(name) {                           // read-only export
    alert(`hello ${name}!`)
  }

  export const greet = (name) =&gt; alert(`hello ${name}!`)  // read-only export
&lt;/script&gt;</pre>

<p>With this in mind, let's go back to our use case. We'll create a function called <code>focus()</code> that gives focus to the <code>&lt;h2&gt;</code> heading. For that we'll need a <code>headingEl</code> variable to hold the reference to the DOM node and we'll have to bind it to the <code>&lt;h2&gt;</code> element using <code>bind:this={headingEl}</code>. Our focus method will just run <code>headingEl.focus()</code>.</p>

<ol>
	<li>
	<p>Update the contents of <code>TodosStatus.svelte</code> like so:</p>

	<pre class="brush: js">&lt;script&gt;
  export let todos

  $: totalTodos = todos.length
  $: completedTodos = todos.filter(todo =&gt; todo.completed).length

  let headingEl

  export function focus() {   // shorter version: export const focus = () =&gt; headingEl.focus()
    headingEl.focus()
  }
&lt;/script&gt;

&lt;h2 id="list-heading" bind:this={headingEl} tabindex="-1"&gt;{completedTodos} out of {totalTodos} items completed&lt;/h2&gt;</pre>

	<p>Note that we've added a <code>tabindex</code> attribute to the <code>&lt;h2&gt;</code> to allow the element to receive focus programmatically.</p>

	<p>As we saw earlier, using the <code>bind:this={headingEl}</code> directive gives us a reference to the DOM node in the variable <code>headingEl</code>. Then we use <code>export function focus()</code> to expose a function that gives focus to the <code>&lt;h2&gt;</code> heading.</p>

	<p>How can we access those exported values from the parent? Just as you can bind to DOM elements with the <code>bind:this={dom_node}</code> directive, you can also bind to component instances themselves with <code>bind:this={component}</code>. So, when you use <code>bind:this</code> on an HTML element, you get a reference to the DOM node, and when you do it on a Svelte component, you get a reference to the instance of that component.</p>
	</li>
	<li>
	<p>So to bind to the instance of <code>TodosStatus</code> we'll first create a <code>todosStatus</code> variable in <code>Todos.svelte</code>. Add the following line below your <code>import</code> statements:</p>

	<pre class="brush: js">let todosStatus                   // reference to TodosStatus instance</pre>
	</li>
	<li>
	<p>Next, add a <code>bind:this={todosStatus}</code> directive to the call, as follows:</p>

	<pre class="brush: html">&lt;!-- TodosStatus --&gt;
&lt;TodosStatus bind:this={todosStatus} {todos} /&gt;
</pre>
	</li>
	<li>
	<p>Now we can call the <code>exported focus()</code> method from our <code>removeTodo()</code> function:</p>

	<pre class="brush: js">function removeTodo(todo) {
  todos = todos.filter(t =&gt; t.id !== todo.id)
  todosStatus.focus()             // give focus to status heading
}</pre>
	</li>
	<li>
	<p>Go back to your app — now if you delete any todo, the status heading will be focussed — this is useful to highlight the change in numbers of todos, both to sighted users and screenreader users.</p>
	</li>
</ol>

<div class="notecard note">
<p><strong>Note:</strong> You might be wondering why we need to declare a new variable for component binding — why can't we just call <code>TodosStatus.focus()</code>? You might have multiple <code>TodosStatus</code> instances active, so you need a way to reference each particular instance. That's why you have to specify a variable to bind each specific instance to.</p>
</div>

<h2 id="The_code_so_far">The code so far</h2>

<h3 id="Git_2">Git</h3>

<p>To see the state of the code as it should be at the end of this article, access your copy of our repo like this:</p>

<pre class="brush: bash">cd mdn-svelte-tutorial/06-stores</pre>

<p>Or directly download the folder's content:</p>

<pre class="brush: bash">npx degit opensas/mdn-svelte-tutorial/06-stores</pre>

<p>Remember to run <code>npm install &amp;&amp; npm run dev</code> to start your app in development mode.</p>

<h3 id="REPL_2">REPL</h3>

<p>To see the current state of the code in a REPL, visit:</p>

<p><a href="https://svelte.dev/repl/d1fa84a5a4494366b179c87395940039?version=3.23.2">https://svelte.dev/repl/d1fa84a5a4494366b179c87395940039?version=3.23.2</a></p>

<h2 id="Summary">Summary</h2>

<p>In this article we have finished adding all the required functionality to our app, plus we've taken care of a number of accessibility and usability issues. We also finished splitting our app into manageable components, each one with a unique responsibility.</p>

<p>In the meantime, we saw a few advanced Svelte techniques, like:</p>

<ul>
	<li>Dealing with reactivity gotchas when updating objects and arrays.</li>
	<li>Working with DOM nodes using <code>bind:this={dom_node}</code> (binding DOM elements).</li>
	<li>Using the component lifecycle <code>onMount()</code> function.</li>
	<li>Forcing Svelte to resolve pending state changes with the <code>tick()</code> function.</li>
	<li>Adding functionality to HTML elements in a reusable and declarative way with the <code>use:action</code> directive.</li>
	<li>Accessing component methods using <code>bind:this={component}</code> (binding components).</li>
</ul>

<p>In the next article we will see how to use stores to communicate between components, and add animations to our components.</p>

<p>{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_components","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_stores", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}</p>

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