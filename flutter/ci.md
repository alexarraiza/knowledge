# Continuous Integration

## 1 - Codemagic.io

### How to generate files on build run

- Add an environment variable with the file content as a base64 string. To generate the string run:

  ```bash
  openssl base64 -in [path to the file]
  ```

- Add this line for every file to generate on `Pre-build script` / `Pre-test script` depending where you need it

  ```bash
  echo $[variable name]| base64 --decode > $FCI_BUILD_DIR/[path to the file from the root folder of the project]
  ```
