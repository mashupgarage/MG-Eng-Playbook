# React Guidelines

This is the MG way to write react code. Generally we want react components to be simple to understand and easy to reuse.

## Prefer functional components over class components

Previously the practice was to use functional components for stateless components and use class components for stateful components. However, with the arrival of React Hooks, we rarely use class components now. We prefer functional components for the following reasons:

1. It helps keep things consistent. Previously we would have to switch between two paradigms of functional and object oriented programming, which made refactors challenging and sometimes caused confusion (e.g. `this` in classes). By sticking with functional components we can have behavior that is consistent and in line with our JS standard of going functional.
2. It makes components lighter. Class components would usually inherit all behaviors and apply the whole lifecycle immediately while functional components can start basic and get expanded with these behaviors progressively, through hooks.

## Keep reusable components stateless

Components with state tend to be coupled to specific behaviors and become less flexible to reuse. When creating new components we should start stateless and only add state when needed. For example say we have a modal component that looks like this:
  ```typescript
  const Modal = () => {
    const [isOpen, setIsOpen] = useState(false)

    const onClose = () => {
      setIsOpen(!isOpen)
    }

    if (isOpen) {
      return ReactDOM.createPortal(
        <div
          className={wrapperClass}
          aria-label='modal'
          data-testid={dataTestId}
        >
          <div className='body' aria-modal role='dialog' tabIndex={-1}>
            {children}
          </div>
          <div className='background' onClick={() => onClose()} />
        </div>,
        document.body
      )
    }

    return null
  }
  ```

On first look it looks alright and will probably work well enough for the given use case. However what if we want custom logic like an alternative button to close or a confirmation dialog or auto close it after an API action? What if closing the modal should trigger an update in another component but only for specific use cases? You may get tempted to add more logic to the modal to handle those behaviors but after a while that may get tricky. To simplify things we recommend to keep state outside and instead just pass as props:
  ```typescript
  type ModalProps = {
    isOpen: boolean
    onClose: () => void
  }

  const Modal = ({ isOpen, onClose }: ModalProps) => {
    if (isOpen) {
      return ReactDOM.createPortal(
        <div
          className={wrapperClass}
          aria-label='modal'
          data-testid={dataTestId}
        >
          <div className='body' aria-modal role='dialog' tabIndex={-1}>
            {children}
          </div>
          <div className='background' onClick={() => onClose()} />
        </div>,
        document.body
      )
    }

    return null
  }
  ```
This way we keep the modal flexible to adjust to any feature specific behavior (More details in the next section).

## Keep shared state and handlers in a container

We recommend react features to be composed of a single stateful parent component (we call this a container) and one or more stateless child components. This prevents state from being scattered all over the place and makes it easier to find the source of data. Moreover, when components need to interact with each other we will need to move their state to one place anyway so might as well design features in that way from the start. File structure wise we recommend something like this:
```
src/
  containers/
    SignUpContainer.tsx
  components/
    Modal.tsx
    UserInfoForm.tsx
    BusinessInfoForm.tsx
```

All state and handlers for this feature should live only in `SignUpContainer`, something like this:
```typescript
const SignUpContainer = () => {
  const [isModalOpen, setIsModalOpen] = useState(false)
  const [firstName, setFirstName] = useState('')
  const [lastName, setFirstName] = useState('')
  const [companyName, setCompanyName] = useState('')
  const [region, setRegion] = useState('')

  const handleOpen = () => {
    setIsModalOpen(true)
  }

  const handleClose = () => {
    setIsModalOpen(false)
  }

  const handleFirstNameChange = (event: FormEvent<HTMLInputElement>) => {
    setFirstName(event.currentTarget.value)
  }

  const handleLastNameChange = (event: FormEvent<HTMLInputElement>) => {
    setLastName(event.currentTarget.value)
  }

  const handleCompanyNameChange = (event: FormEvent<HTMLInputElement>) => {
    setCompanyName(event.currentTarget.value)
  }

  const handleRegionChange = (event: FormEvent<HTMLInputElement>) => {
    setRegion(event.currentTarget.value)
  }

  return(
    <div>
      <button>Sign Up</button>
      <Modal isOpen={isModalOpen} onClose={handleClose}>
        <UserInfoForm
          firstName={firstName}
          lastName={lastName}
          handleFirstNameChange={handleFirstNameChange}
          handleLastNameChange={handleLastNameChange}
        />
        <BusinessInfoForm
          companyName={companyName}
          region={region}
          handleCompanyNameChange={handleCompanyNameChange}
          handleRegionChange={handleRegionChange}
        />
      </Modal>
    </div>
  )
}
```

This way, if ever we would need another kind of sign up (e.g.separate admin sign up) we can just create a new container with its own state and handlers then reuse the modal or relevant forms.

## Extract non UI logic out of components

Code in react components should primarily be concerned with rendering JSX, updating state or anything that impacts the UI. Anything that does otherwise is better off in dedicated files. This also improves testing as we can focus on only those behaviors without being tied to UI changes. Some examples include:
- Validations
  ```typescript
  export const validateFileSize = (file: File, sizeLimit = 20000000) => {
    return file.size <= sizeLimit
  }
  ```
- Helpers
  ```typescript
  export const fileNameFromUrl = (url: string) => {
    return url
      .split('/')
      .reverse()[0]
      .split('?')[0]
  }

  ```
