# React Testing Guidelines

Testing React code has a bit of learning curve and can be confusing at times. This is a collection of practices and techniques we adopted through our years of experience working with React JS.

## Test the application like how a user would

We follow the philosophy of [testing library](https://testing-library.com/), which states that tests that are written close to how the application is actually used give more confidence. As developers, our first tendency when testing code is to test it based on internal details we wrote (e.g. variable names, state). However, when users use your application they don't think of these things. They test based on what they see on the screen (e.g. labels, element visibility, number of elements). This discrepancy in approach may potentially cause some test cases to be missed, which we can mitigate by testing in a similar fashion. Additionally, avoiding internal details in tests also make components easier to refactor, which is a characteristic of an effective automated test.

## Apply dependency injection
In [General Testing Guidelines](/standards/tests/general-testing-guidelines.md), we mentioned that we should mock external dependencies to make things more predictable. Say we have a component like this:
```Typescript
import { fetchPosts, deletePosts } from '../api/posts'

const Controls = () => {
  return(
    <>
      <button onClick={() => fetchPosts()}>Fetch Posts</button>
      <button onClick={() => deletePosts()}>Delete Posts</button>
    </>
  )
}
```
On button click it will call either a fetch API or a delete API. These can call external APIs which can slow down test runtime or do anything unpredictable. To mock these can change our imported items into props that we can change as needed:
```Typescript
import {
  fetchPosts as defaultFetchPosts,
  deletePosts as defaultDeletePosts
} from '../api/posts'

type ControlsProps = {
  fetchPosts?: () => Promise<Post[]>
  deletePosts?: () => Promise<Post[]>
}

const Controls = ({
  fetchPosts = defaultFetchPosts,
  deletePosts = defaultDeletePosts
}: ControlsProps) => {
  return(
    <>
      <button onClick={() => fetchPosts()}>Fetch Posts</button>
      <button onClick={() => deletePosts()}>Delete Posts</button>
    </>
  )
}
```
We import the API functions with a different name (we recommend prepending 'default') to differentiate it from the props which is what everything else will interact with. We then set the props as optional so we can omit it when we don't need to mock. Component can then be called like so:
```Typescript
// in calling component it defaults and works like usual
<Button />

// when testing we can mock them into something we can control
<Button
  fetchPosts={jest.fn().mockResolvedValue([])}
  deletePosts={jest.fn().mockResolvedValue([])}
/>
```

## Write your components with accessibility in mind

When we talk about testing how a user would use application, that should include users that use accessibility technology such as screen readers. In its core, the goal of a screen reader is to find content and read them to user which interects with the goal of react testing. Hence, following the best practices for accessibility helps testability as well.

### Apply proper labels

Users tend to identify form elements like input fields by the text associated with them. To write our components in a way consistent with this behavior, it's important to apply proper labelling using label tags:

- ❌ labels that aren't linked
  ```Typescript
  <label>Name</label>
  <input type='text' />
  ```

- ✅ linking label with htmlFor
  ```Typescript
  <label htmlFor='name'>Name</label>
  <input type='text' id='name' />
  <label htmlFor='age'>Age</label>
  <input type='number' id='age' />
  ```

- ✅ linking non labels with aria-labelledby
  ```Typescript
  <div id='name-label'>
  <input type='text' aria-labelledby='name-label' />
  ```

- ✅ nesting element in label tag
  ```Typescript
  <label>
    <input type='text' />
    Name
  </label>
  ```

We can then get these using the label text queries:

```Typescript
expect(screen.getByLabelText('Name')).toBe('Test Name')
```

### Use clearly defined roles

Aside from labels, a user would tend to identify UI elements by what they do (e.g. a button to click, a menu to navigate, a cell in a table). Assistive technology aims to do the same thing but unlike a person it needs more data to identify what each UI element does. That's where the aria role comes in. Most common html tags such as button have [implicit roles](https://rafaelcamargo.com/blog/using-testing-library-with-implicit-aria-roles/) already but if we use alternative tags (e.g. div tag for button) we need to explicitly add it. Hence, it's also a good practice for accessibility to use the html tags that make the most semantic sense.

- ❌ redundant role
  ```Typescript
  <button role='button' onClick={handleClick}>Click here</button>
  ```

- ❌ not specifying role for alternative tags
  ```Typescript
  <div onClick={handleClick}>Click here</div>
  ```

- ✅ using implicit role
  ```Typescript
  <button onClick={handleClick}>Click here</button>
  ```

- ✅ explicit role
  ```Typescript
  <div role='button' onClick={handleClick}>Click here</div>
  ```

We can then get the button using role queries:

```Typescript
const button = screen.getByRole('button', { name: /click here/i })
```

## data-testid should be a last resort

When testing react components the usual tendency is to attach test ids to the elements to look for them. The test id, while it provides straightforward access of specific elements, slightly detracts from the philosophy of testing like a user does because user isn't aware of these. Always start with queries that resemble how users (or assistive technology) find things in the UI then use data-testid only when none can apply. For more info check out the [documentation](https://testing-library.com/docs/queries/about#priority).

## Add visible loading states

For components that load data asynchronously, there are times when the test needs to wait for the loading to complete before proceeding with assertions. To know that data is still loading we should add a visual cue of the progress such as text, a progress bar or spinner. For example we have a component like this:

```Typescript
{isLoading ? (
  <div data-testid='loading'>Loading...</div>
): (
  <div>Content</div>
)}
```

When the component is still loading it displays the text `Loading...` (In other implementations it can be a spinner or progress bar). At the moment of writing there isn't a clear standard yet for accessibility of loading indicators so for simplicity we just use a test id for now. We then use the `waitForElementToBeRemoved` function from testing library to wait for the loading to end:

```Typescript
await waitForElementToBeRemoved(() => screen.getByTestId('loading'))
```

## Use react-select-event to test react-select elements

In react projects, it's common to use [react-select](https://react-select.com/home) to have an easy way to create a select menu. However, as it is 3rd party code, we don't have control over its structure which can make tests sensitive to failures when the library is updated. To be able to test these better, we recommend to use [react-select-event](https://testing-library.com/docs/ecosystem-react-select-event/).

## References
- <https://www.carlrippon.com/accessible-react-forms/>
