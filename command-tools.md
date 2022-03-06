# Useful commands

## Kill process on windows

- Get the process:
```js
netstat -ano | findstr :8080
```
- Stop the process from the output from the previous command:
```js
stop-process 82932
```