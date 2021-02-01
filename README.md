# nextjs-chiffre

[![NPM](https://img.shields.io/npm/v/nextjs-chiffre?color=red)](https://www.npmjs.com/package/nextjs-chiffre)
[![MIT License](https://img.shields.io/github/license/chiffre-io/nextjs-chiffre.svg?color=blue)](https://github.com/chiffre-io/nextjs-chiffre/blob/next/LICENSE)
[![Continuous Integration](https://github.com/chiffre-io/nextjs-chiffre/workflows/Continuous%20Integration/badge.svg?branch=next)](https://github.com/chiffre-io/nextjs-chiffre/actions)
[![Coverage Status](https://coveralls.io/repos/github/chiffre-io/nextjs-chiffre/badge.svg?branch=next)](https://coveralls.io/github/chiffre-io/nextjs-chiffre?branch=next)
[![Dependabot Status](https://api.dependabot.com/badges/status?host=github&repo=chiffre-io/nextjs-chiffre)](https://dependabot.com)

Chiffre analytics integration for Next.js

## Installation

```shell
$ yarn add nextjs-chiffre
or
$ npm install nextjs-chiffre
```

## Usage

In your `_document.(jsx|tsx)`, add the `<ChiffreAnalytics>` component at the end
of `<body>`:

```tsx
import Document, { Html, Main, NextScript } from 'next/document'
import { ChiffreAnalytics } from 'next-chiffre-analytics'

export default class MyDocument extends Document {
  static async getInitialProps(ctx: any) {
    const initialProps = await Document.getInitialProps(ctx)
    return { ...initialProps }
  }

  render() {
    return (
      <Html lang="en">
        <body>
          <Main />
          <NextScript />
          {/* ------------------------------------*/}
          <ChiffreAnalytics
            projectID="yourProjectID"
            publicKey="pk.yourProjectPublicKey"
          />
          {/* ----------------------------------- */}
        </body>
      </Html>
    )
  }
}
```

If you wish to use environment variables to pass the project ID and public key,
you must prefix them with `NEXT_PUBLIC_` to make them available to the front-end
code:

```tsx
<ChiffreAnalytics
  projectID={process.env.NEXT_PUBLIC_CHIFFRE_PROJECT_ID}
  publicKey={process.env.NEXT_PUBLIC_CHIFFRE_PUBLIC_KEY}
/>
```

## Configuration

The only two arguments required are:

- `projectID`: Your project ID can be found in the project url. Eg: `https://chiffre.io/projects/yourProjectID`.
- `publicKey`: Your public key can be found in the project settings, and looks like `pk.{43 base64 characters}`

### Optional props

You can disable the `<noscript>` behaviour, that logs anonymous visits for users
with JavaScript disabled:

```tsx
<ChiffreAnalytics projectID="..." publicKey="..." disableNoJSAnonymousVisits />
```

You can declare the allowed domains where analytics can be sent from, using
an array of strings or regexes:

```tsx
<ChiffreAnalytics
  projectID="..."
  publicKey="..."
  allowedDomains={[
    'my-project.io', // Production domain
    /^my-project-.+\.vercel\.app$/ // Preview deployments on Vercel
  ]}
/>
```

You can set paths to be ignored by page tracking (eg: private pages):

```tsx
<ChiffreAnalytics
  projectID="..."
  publicKey="..."
  ignorePaths={['/admin/', '/private/']}
/>
```

If the path of the URL starts with one of the values listed, no events will be
sent.

## License

[MIT](https://github.com/chiffre-io/nextjs-chiffre/blob/next/LICENSE) - Made with ❤️ by [François Best](https://francoisbest.com).
