# Javascript Testing Guidelines

It's one thing to know how to write tests for javascript code but another to write effective tests. Here are some of our recommended practices when testing javascript code.

## Use fixtures for test data

When writing tests, it's common to have data to set up which can look like this:

```typescript
describe('displayName()', () => {
  it('returns name and username for standard user', () => {
    const user: User = {
      id: 1,
      name: 'Leanne Graham',
      username: 'Bret',
      userType: 'standard',
      email: 'Sincere@april.biz',
      address: {
        street: 'Kulas Light',
        suite: 'Apt. 556',
        city: 'Gwenborough',
        zipcode: '92998-3874',
        geo: {
          lat: '-37.3159',
          lng: '81.1496',
        },
      },
      phone: '1-770-736-8031 x56442',
      website: 'hildegard.org',
      company: {
        name: 'Romaguera-Crona',
        catchPhrase: 'Multi-layered client-server neural-net',
        bs: 'harness real-time e-markets',
      }
    }

    const name = displayName(user)
    expect(name).toBe('Leanne Grahan (Bret)')
  })

  it('returns name and admin indicator for admin user', () => {
    const user: User = {
      id: 3,
      name: 'Clementine Bauch',
      username: 'Samantha',
      userType: 'admin',
      email: 'Nathan@yesenia.net',
      address: {
        street: 'Douglas Extension',
        suite: 'Suite 847',
        city: 'McKenziehaven',
        zipcode: '59590-4157',
        geo: {
          lat: '-68.6102',
          lng: '-47.0653',
        },
      },
      phone: '1-463-123-4447',
      website: 'ramiro.info',
      company: {
        name: 'Romaguera-Jacobson',
        catchPhrase: 'Face to face bifurcated interface',
        bs: 'e-enable strategic applications',
      }
    }

    const name = displayName(user)
    expect(name).toBe('Clementine Bauch (Admin)')
  })
})
```
This can cause test files to be long and repetitive (more apparent as number of scenarios increase) so we recommend to extract them into separate files:

```typescript
// userFixture.ts
export const standardUserFixture: User = {
  id: 1,
  name: 'Leanne Graham',
  username: 'Bret',
  userType: 'standard',
  email: 'Sincere@april.biz',
  address: {
    street: 'Kulas Light',
    suite: 'Apt. 556',
    city: 'Gwenborough',
    zipcode: '92998-3874',
    geo: {
      lat: '-37.3159',
      lng: '81.1496',
    },
  },
  phone: '1-770-736-8031 x56442',
  website: 'hildegard.org',
  company: {
    name: 'Romaguera-Crona',
    catchPhrase: 'Multi-layered client-server neural-net',
    bs: 'harness real-time e-markets',
  }
}

export const adminUserFixture: User = {
  id: 3,
  name: 'Clementine Bauch',
  username: 'Samantha',
  userType: 'admin',
  email: 'Nathan@yesenia.net',
  address: {
    street: 'Douglas Extension',
    suite: 'Suite 847',
    city: 'McKenziehaven',
    zipcode: '59590-4157',
    geo: {
      lat: '-68.6102',
      lng: '-47.0653',
    },
  },
  phone: '1-463-123-4447',
  website: 'ramiro.info',
  company: {
    name: 'Romaguera-Jacobson',
    catchPhrase: 'Face to face bifurcated interface',
    bs: 'e-enable strategic applications',
  }
}
```

Then we can update our tests to import these fixtures:

```typescript
import {
  standardUserFixture,
  adminUserFixture
} from '../fixtures/userFixture'

describe('displayName()', () => {
  it('returns name and username for standard user', () => {
    const user: User = { ...standardUserFixture }

    const name = displayName(user)
    expect(name).toBe('Leanne Grahan (Bret)')
  })

  it('returns name and admin indicator for admin user', () => {
    const user: User = { ...adminUserFixture }

    const name = displayName(user)
    expect(name).toBe('Clementine Bauch (Admin)')
  })
})
```

This way we have much shorter and readable tests. It also helps DRY the data so that we can reuse it in other tests as well.
