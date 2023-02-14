# garrettsparks tap

## What formulae are available?

* [node@16](https://formulae.brew.sh/formula/node@16)
* [node@18](https://formulae.brew.sh/formula/node@18)

## Why not open a PR to homebrew-core?

Options are [no longer accepted](https://github.com/Homebrew/homebrew-core/issues/31510) in [homebrew-core](https://github.com/Homebrew/homebrew-core).

## Why would I use these?

The [default behavior](https://nodejs.org/api/intl.html#embed-the-entire-icu-full-icu) for Node binaries is to build with full internationalization support statically linked (`--with-intl=full-icu`).

However, the brew formulae for Node build with system ICU (`--with-intl=system-icu`). In some scenarios, the system ICU may be incompatible with older versions of Node.

One example of this is ICU 72.1 upgrades to CLDR 42 which introduces a new whitespace unicode character (`U+202F`) in date strings which breaks Javascript code like this

```js
new Date((new Date()).toLocaleString('en-US')) 
```

That code (anit-pattern or not) is used in libraries like [dayjs](https://day.js.org/) for [timezone support](https://github.com/iamkun/dayjs/blob/dev/src/plugin/timezone/index.js#L99).

Node released a [fix](https://github.com/nodejs/node/pull/45573) for this in v19 and v18, but if you're using an older version of Node, you won't get the fix.

Building with `-with-intl=full-icu` ensures that your Node binary has the properly supported version of ICU statically linked.

These formulae add an option `--with-full-icu` to the default `node@16` and `node@18` formulae to help avoid incompatibilities in the future.

## How do I install these formulae?

`brew install garrettsparks/tap/<formula>`

Or `brew tap garrettsparks/tap` and then `brew install <formula>`.

E.g.

```
brew install garrettsparks/tap/node@16
```

or

```
brew tap garrettsparks/tap
brew install node@16
```

## With full ICU

```
brew install garrettsparks/tap/node@16 --with-full-icu
```

or

```
brew tap garrettsparks/tap
brew install node@16 --with-full-icu
```


## Documentation

`brew help`, `man brew` or check [Homebrew's documentation](https://docs.brew.sh).
