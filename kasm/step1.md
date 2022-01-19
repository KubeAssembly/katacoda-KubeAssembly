

`kind create cluster --image ghcr.io/liquid-reply/kind-crun-wasm:v1.23.0`{{execute}}

`kind load docker-image hydai/wasm-wasi-example:with-wasm-annotation`{{execute}}

`kubectl run -it --rm --restart=Never wasi-demo --image=hydai/wasm-wasi-example:with-wasm-annotation --annotations="module.wasm.image/variant=compat" /wasi_example_main.wasm 50000000
`{{execute}}