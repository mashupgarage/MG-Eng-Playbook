# Money Guidelines

In this age, handling money has become a common use case for most software such as e-commerce, banking or financial applications. Whatever application you're making you'll eventually have to handle money in some form. How should we represent money in software? There are many approaches to do so but some are more effective than others. Here are our recommendations on representing money:

## ❌ strings

Typically we know something is money by seeing a currency symbol and an amount formatted in a particular way (P1,234.56). However, much as this is familiar with how we usually read money, it's a bad way to represent money in our code and database. This is because money values will tend to be used for computation which strings are not designed for. If we represent it as such in database we would always need to convert it to a number when querying sums or deriving amounts which is a hassle. Money should be represented as numbers in code and db and the only time a money value should be represented as a string is when displaying to UI.

## ❌ float

When viewing money from a number perspective we know most money systems have a unit amount and a sub-unit amount usually called cents (199.75). We know these aren't integer values so we would tend to think about floating point numbers or decimals but this is a newbie mistake because floats are unreliable. When adding floats together we can run into rounding errors such as these:

```
0.1 + 0.2
0.30000000000000004

0.1 + 0.7
0.7999999999999999
```

We know the saying that *every cent counts* so unexpectedly losing or gaining even a slight amount due to rounding is unacceptable. This is more critical for banking and financial apps where computations have to be precise. So do not use floats for money values in your code and db it will only cause problems down the line.
