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

## ⚠️  big decimal

While it may vary between programming languages, usually there is a big decimal number representation which allows us to represent numbers more precisely. Usually we see these numbers in scientific notation (0.9975e2) and don't have the overflow problems that floats have:

```
BigDecimal("0.1") + BigDecimal("0.2")
0.3

BigDecimal("0.1") + BigDecimal("0.7")
0.8
```

This is better for money amounts to be exact but they can be expensive to represent for most cases since most money values just have 2 decimal places for cents. Only use when more precise amounts beyond 2 decimal places is needed. One major use case for this is when computing interest where we want to store exact computations per period (e.g. daily) then only round to cents when computation is complete.

## ✅ integers

As mentioned earlier, most money systems have a unit amount and fractional amount that's why we would typically think of floats. We know floats have problems with rounding and aren't recommended but what if we can remove the fractional amount? We can by scaling the values. We know that 199.75 pesos is actually 19975 centavos which can now be expressed as integers. By using integers we remove the need to round off and approximate because we're always dealing with exact values. We recommend to represent money in their smallest most atomic unit (mostly cents) in code and db then, similar to formatting, only scale into unit form in display. However, take note that there are some currency systems that don't do subunits such as Japanese Yen and some that use 3 decimal places instead such as Bahraini Dinar so scaling needs to be adjusted accordingly if dealing with these currencies.

## ✅ money pattern

Using integers is already a step in the right direction but given our last point of different scaling per currency how will we know which scaling to use? This is not much of a problem when dealing with only a single currency in the whole system but when we have to deal with multiple currencies we may need to use the money pattern. The money pattern (Defined by Martin Fowler in Patterns of Enterprise Application Architecture) is designed to attach some context to integer money values by also specifying the currency. We usually represent this in some hash or object form:

```
{
  amount_cents: 19975,
  amount_currency: "PHP"
}

{
  amount_cents: 599,
  amount_currency: "USD"
}

{
  amount_cents: 1500,
  amount_currency: "JPY"
}
```
