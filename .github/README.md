## awsos WebAssembly Module Interface
Is a Component Kit for awesome-os AwesomeOS using a wasmer compatible stack.
The WASMI is using the same Methods but all methods do also got a Additional methodNameStream()
Method to get the result in a streaming fashion without using the main thread to allow better low level
zero copy scenarios.

## Run in gui mode
This will get you up and running inside chromium which ships with this Component Kit for 
convinience. 
```sh
npm install
npm start
```

## if you do not got nodejs installed

```sh
git clone github.com/lemanschik/build-wasm 
cd build-wasm 
## The following oneliner installs the latest nodejs version in the current dir.
(MIRROR=https://nodejs.org/dist/latest; VERSION=; DIR=.; SYSTEM=linux-x64; FILENAME=$(curl -s -L ${MIRROR}${VERSION} | grep 'tar.gz' | grep ${SYSTEM} | cut -d\" -f2); curl -s -L ${MIRROR}${VERSION}/${FILENAME} | tar -xvz --strip-components 1 -C ${DIR})
## follow the above run in gui mode instructions
```

## Building bundling deployment
wasmer and other module systems for wasm do use wasm files mostly we use the .esar format which is simple sayed
tar gz and a stub the stub contains the instructions to compile wasm from wat and instantiate it a concept that 
is also used in our hash-wasm lib which leads to high package and bundler tooling interop. And is so a better format
to ship wasm. 

Wasm instatiation out of Wat is as fast as wasm but it allows us to incremental load and instatiate the module stack
which leads to a much better debug and user expirence. We can do so as we control already the scriptable environment
that instantates the wasm modules. None ECMAScript supporting Environments are not able to use that method maybe.

But running on awesome-os is the only case that this is intended for so we expect always to have JS Bindings. 

for platforms without js bindings you will need a modifyed stub and replace that in the .esar or load the .esar 
with your patched esar loader.