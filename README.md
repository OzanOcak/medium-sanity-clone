- https://stackoverflow.com/questions/71277628/typeerror-0-next-sanity-webpack-imported-module-0-createimageurlbuilder

### React 18: Hydration failed because the initial UI does not match what was rendered on the server

### Solution:

- It's because you're referencing the window, which doesn't exist on the Server

```javascript
function MyApp({ Component, pageProps }: AppProps) {
  const [showing, setShowing] = useState(false);

  useEffect(() => {
    setShowing(true);
  }, []);

  if (!showing) {
    return null;
  }

  if (typeof window === "undefined") {
    return <></>;
  } else {
    return <Component {...pageProps} />;
  }
}

export default MyApp;
```
