

`kind create cluster --image ghcr.io/liquid-reply/kind-crun-wasm:v1.23.0`{{execute}}

> ⚠️ This can take up to 10 minutes

The output should look like the following:

```
Creating cluster "kind" ...
 ✓ Ensuring node image (ghcr.io/liquid-reply/kind-crun-wasm:v1.23.0) 🖼 
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind
```
<!-- // If you get an imagePullError you can download the image via docker and load it to kind.
`docker pull hydai/wasm-wasi-example:with-wasm-annotation && kind load docker-image hydai/wasm-wasi-example:with-wasm-annotation`{{execute}}-->

Finally you can run an example wasm container to test the setup.

`kubectl run -it --rm --restart=Never wasi-demo --image=hydai/wasm-wasi-example:with-wasm-annotation --annotations="module.wasm.image/variant=compat" /wasi_example_main.wasm 50000000
`{{execute}}

The output should look like the following:

```
Random number: -1635205073
Random bytes: [67, 66, 102, 194, 182, 41, 237, 194, 245, 243, 251, 129, 157, 68, 19, 230, 66, 143, 15, 69, 211, 15, 221, 23, 200, 188, 29, 122, 74, 9, 157, 115, 81, 66, 200, 217, 194, 239, 23, 249, 243, 165, 93, 65, 51, 51, 241, 114, 151, 46, 10, 37, 170, 117, 50, 212, 102, 44, 232, 220, 221, 251, 97, 236, 45, 83, 228, 136, 18, 232, 210, 72, 120, 26, 208, 71, 219, 250, 248, 251, 130, 169, 52, 149, 21, 45, 238, 42, 94, 253, 34, 107, 159, 164, 145, 222, 163, 253, 205, 252, 215, 45, 254, 105, 81, 25, 199, 230, 192, 255, 221, 128, 38, 123, 159, 194, 103, 84, 204, 89, 223, 147, 183, 82, 25, 94, 30, 206]
Printed from wasi: This is from a main function
This is from a main function
The env vars are as follows.
The args are as follows.
/wasi_example_main.wasm
50000000
File content is This is in a file
pod "wasi-demo" deleted
```